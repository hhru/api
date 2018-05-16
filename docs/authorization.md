# Авторизация

* [Получение авторизации](#get-auth)
  * [Правила формирования специального redirect_uri](#redirect_uri)
  * [Процесс авторизации](#get-auth-process)
  * [Успешное получение временного `authorization_code`](#get-authorization_code)
  * [Получение access и refresh токенов](#get-tokens)
* [Обновление пары access и refresh токенов](#refresh_token)
* [Описание ошибок при получении/обновлении токенов](#errors)
* [Использование и проверка access-токена](#check-access_token)
* [Запрос авторизации под другим пользователем](#force-login)
* [Полезные ссылки](#links)


<a name="general"></a>
Авторизация осуществляется по протоколу OAuth 2.0. Подробная документация по
протоколу: [RFC 6749](http://tools.ietf.org/html/rfc6749).

Зарегистрированное приложение может запрашивать у пользователей hh.ru
разрешение доступа к их персональным данным, без получения и хранения их
логина и пароля.

---

До 1 апреля 2015 года основной домен API был m.hh.ru. Авторизация через m.hh.ru
будет доступна, однако теперь рекомендуется использовать домен hh.ru.
Документация была обновлена в соответствии с новым адресом.

---


<a name="get-auth"></a>
## Получение авторизации
В начале приложению необходимо направить пользователя (открыть страницу)
по адресу:

```
https://hh.ru/oauth/authorize?
  response_type=code&
  client_id={client_id}&
  state={state}&
  redirect_uri={redirect_uri}
```

Обязательные параметры:

* `response_type=code` — указание на способ получение авторизации, используя
  authorization code
* `client_id` — идентификатор, полученный при создании приложения


Необязательные параметры:

* `state` — в случае указания, будет включен в ответный редирект.
  Это позволяет исключить возможность взлома путём подделки межсайтовых
  запросов. Подробнее об этом:
  [RFC 6749. Section 10.12](http://tools.ietf.org/html/rfc6749#section-10.12)
* `redirect_uri` — uri для перенаправления пользователя после
  авторизации. Если не указать, используется из настроек приложения. При
  наличии происходит валидация значения. Вероятнее всего, потребуется сделать
  urlencode значения параметра.


<a name="redirect_uri"></a>
### Правила формирования специального redirect_uri

К примеру, если в настройках сохранен `http://example.com/oauth`, то разрешено
указывать:

* `http://www.example.com/oauth` — поддомен;
* `http://www.example.com/oauth/sub/path` — уточнение пути;
* `http://example.com/oauth?lang=RU` — дополнительный параметр;
* `http://www.example.com/oauth/sub/path?lang=RU` — всё вместе.

Запрещено:

* `https://example.com/oauth` — различные протоколы;
* `http://wwwexample.com/oauth` — различные домены;
* `http://wwwexample.com/` — другой путь;
* `http://example.com/oauths` — другой путь;
* `http://example.com:80/oauths` — указание изначально отсутствующего порта;


<a name="get-auth-process"></a>
### Процесс авторизации

Если пользователь не авторизован на сайте, ему будет показана форма
авторизации на сайте. После прохождения авторизации на сайте, пользователю
будет выведена форма с запросом разрешения доступа вашего приложения к его
персональным данным.

Если пользователь не разрешает доступ приложению, пользователь будет
перенаправлен на указанный `redirect_uri` с `?error=access_denied` и
`state={state}`, если таковой был указан при первом запросе.


<a name="get-authorization_code"></a>
### Успешное получение временного `authorization_code`

В случае разрешения прав, в редиректе будет указан
временный `authorization_code`:

```http
HTTP/1.1 302 FOUND
Location: {redirect_uri}?code={authorization_code}
```

Если пользователь авторизован на сайте и доступ данному приложению однажды
ранее выдан, ответом будет сразу вышеописанный редирект с `authorization_code`
(без показа формы логина и выдачи прав).


<a name="get-tokens"></a>
### Получение access и refresh токенов

После получения `authorization_code` приложению необходимо сделать сервер-сервер
POST-запрос на `https://hh.ru/oauth/token` для обмена полученного
`authorization_code` на `access_token`.

В запросе необходимо передать дополнительные параметры:

* `grant_type=authorization_code`
* `client_id` и `client_secret` - необходимо заполнить значениями, выданными при
  [регистрации приложения](https://dev.hh.ru/admin).
* `redirect_uri` - Необходимо передать то же, что было указано при
  [получении авторизации](#get-auth). В противном случае вернется ошибка.
* `code` – значение `authorization_code`, полученное при
  [перенаправлении пользователя](#get-authorization_code)

Тело запроса необходимо передавать в стандартном
`application/x-www-form-urlencoded` с указанием соответствующего заголовка
`Content-Type`.

В ответе вернётся JSON:

```json
{
    "access_token": "{access_token}",
    "token_type": "bearer",
    "expires_in": 1209600,
    "refresh_token": "{refresh_token}",
}
```

`authorization_code` имеет довольно короткий срок жизни, при его истечении
необходимо запросить новый.

Если обмен `authorization_code` произвести не удалось, то вернётся ответ
`400 Bad Request` с телом:

```json
{
    "error": "invalid_request",
    "error_description": "bad redirect url"
}
```

где:

Имя | Тип | Значение 
--- | --- | --------
error | строка | Одно из значений, [описанных в стандарте RFC 6749](http://tools.ietf.org/html/rfc6749#section-5.2). Например, `invalid_request`, если какой либо из обязательных параметров не был передан
error_description | строка | Дополнительное описание ошибки


<a name="refresh_token"></a>
## Обновление пары access и refresh токенов
`access_token` также имеет срок жизни (ключ `expires_in`, в секундах), при его
истечении приложение должно сделать запрос с `refresh_token` для получения
нового.

Запрос необходимо делать в `application/x-www-form-urlencoded`.

```
POST https://hh.ru/oauth/token
```

В запросе необходимо передать дополнительные параметры:
* `grant_type=refresh_token`
* `refresh_token` – refresh-токен, полученный ранее при
  [получении пары токенов](#get-tokens) или прошлом обновлении пары

Ответ будет идентичен ответу на получения токенов в первый раз:

```json
{
    "access_token": "{access_token}",
    "token_type": "bearer",
    "expires_in": 1209600,
    "refresh_token": "{refresh_token}",
}
```

`refresh_token` можно использовать только один раз и только по истечению
срока действия `access_token`.

После получения новой пары access и refresh токенов, их необходимо использовать
в дальнейших запросах в api и запросах на продление токена.

Если обновить токен не удалось, то вернётся ответ `400 Bad Request` с телом:

```json
{
    "error": "invalid_request",
    "error_description": "account not found"
}
```

где:

Имя | Тип | Значение 
--- | --- | --------
error | строка | Одно из значений, [описанных в стандарте RFC 6749](http://tools.ietf.org/html/rfc6749#section-5.2). Например, `invalid_request`, если какой либо из обязательных параметров не был передан
error_description | строка | Дополнительное описание ошибки

<a name="errors"></a>
## Описание ошибок при получении/обновлении токенов

Ниже приведены некоторые возможные ошибки с описанием.

<table>
<tr><th>error</th><th>error_description</th><th>описание</th></tr>

<tr>
    <td rowspan=5>invalid_request</td>
    <td>account not found</td>
    <td>Ошибка может возникнуть, если передана неправильная пара client_id и client_secret</td>
</tr>
<tr>
    <td>bad redirect url</td>
    <td>Передан неправильный redirect_url</td>
</tr>
<tr>
    <td>token is empty</td>
    <td>Не передан refresh_token</td>
</tr>
<tr>
    <td>token not found</td>
    <td>Передан не правильный refresh_token</td>
</tr>
<tr>
    <td>code not found</td>
    <td>Переданный authorization_code не найден</td>
</tr>

<tr>
    <td>invalid_client</td>
    <td>client_id or client_secret not found</td>
    <td>Ошибка может возникнуть в случае, если данный client_id не найден или был удален, передан неправильный client_secret</td>
</tr>

<tr>
    <td rowspan=8>invalid_grant</td>
    <td>token has already been refreshed</td>
    <td>Ошибка возникает при попытке воспользоваться refresh-токеном второй раз</td>
</tr>
<tr>
    <td>token not expired</td>
    <td>Ошибка возникает при попытке обновить действующий access-токен. access-токен можно обновлять только после того, как он истек</td>
</tr>
<tr>
    <td>token was revoked</td>
    <td>Токен был отозван. Например, токен отзывается, если время действия пароля истекло</td>
</tr>
<tr>
    <td>bad token</td>
    <td>Передано неправильное значение токена</td>
</tr>
<tr>
    <td>code has already been used</td>
    <td>authorization_code уже был использован (его можно использовать только один раз)</td>
</tr>
<tr>
    <td>code expired</td>
    <td>authorization_code истек</td>
</tr>
<tr>
    <td>code was revoke</td>
    <td>authorization_code был отозван (это происходит, если время действия пароля истекло)</td>
</tr>
<tr>
    <td>token deactivated</td>
    <td>Токен был деактивирован. Токен деактивируется после того, как пользователь сменил пароль</td>
</tr>

<tr>
    <td>unsupported_grant_type</td>
    <td>unsupported grant_type</td>
    <td>Возникает, если передать неправильное значение в поле grant_type</td>
</tr>

</table>

<a name="check-access_token"></a>
## Использование и проверка access-токена

Приложение должно использовать полученный `access_token` для авторизации,
передавая его в заголовке в формате:

```Authorization: Bearer ACCESS_TOKEN```

Для тестирования токена, удобно использовать метод `/me` (это необязательный
шаг).

```http
GET /me HTTP/1.1
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
Host: api.hh.ru
Accept: */*
Authorization: Bearer access_token
```

Документация по ответу от `/me` [в соответствующем разделе](me.md).

[Описание ошибок авторизации](errors.md#oauth).

<a name="force-login"></a>
## Запрос авторизации под другим пользователем

Возможен следующий сценарий:

1. Приложение перенаправляет пользователя на сайт с запросом авторизации.
2. Пользователь на сайте уже авторизован и данному приложение доступ уже был
   разрешен.
3. Пользователю будет предложена возможность продолжить работу под текущим аккаунтом,
   либо зайти под другим аккаунтом.

Если есть необходимость, чтобы на шаге 3 сразу происходило перенаправление (redirect) с временным токеном,
необходимо добавить к запросу `/oauth/authorize...` параметр `skip_choose_account=true`.
В этом случае автоматически выдаётся доступ пользователю авторизованному на сайте.

Если есть необходимость всегда показывать форму авторизации, приложение может
добавить к запросу `/oauth/authorize...` параметр `force_login=true`. В этом
случае, пользователю будет показана форма авторизации с логином и паролем
даже в случае, если пользователь уже авторизован.

Это может быть полезно приложениям, которые предоставляют сервис только для
соискателей. Если пришел пользователь-работодатель, приложение может предложить
пользователю повторно разрешить доступ на сайте, уже указав
другую учетную запись.

Также, после авторизации приложение может показать пользователю сообщение:

```
Вы вошли как %Имя_Фамилия%. Это не вы?
```
и предоставить ссылку с `force_login=true` для возможности захода под
другим логином.


<a name="links"></a>
## Полезные ссылки

* Подробная документация по протоколу: [RFC 6749](http://tools.ietf.org/html/rfc6749)
* Библиотека [ScribeJava](https://github.com/scribejava/scribejava),
  поддерживающая авторизацию в API HeadHunter.
  * [Habrahabr: ScribeJava — даже ваша бабушка сможет работать с OAuth](https://habrahabr.ru/company/hh/blog/278957/)
