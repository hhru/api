# Авторизация

Для выполнения большинства запросов к API необходимо передавать access-токен.
Авторизация осуществляется по протоколу [OAuth 2.0](#links).

API поддерживает следующие уровни авторизации:
* [авторизация приложения](authorization_application.md)
* [авторизация пользователя](authorization_user.md)

---

До 1 апреля 2015 года основной домен API был m.hh.ru. Авторизация через m.hh.ru
будет доступна, однако теперь рекомендуется использовать домен hh.ru.
Документация была обновлена в соответствии с новым адресом.

---

* [Получение access-токена](#get-access_token)
* [Использование access-токена](#use-access_token)
* [Проверка access-токена](#check-access_token)
* [Полезные ссылки](#links)

<a name="get-access_token"></a>
## Получение access-токена

* Получение [токена приложения](authorization_application.md#get-client-auth)
* Получение [токена пользователя](authorization_user.md#get-auth)

<a name="use-access_token"></a>
## Использование access-токена

Приложение должно использовать полученный `access_token` для авторизации,
передавая его в заголовке в формате:

```Authorization: Bearer ACCESS_TOKEN```

[Описание ошибок авторизации](errors.md#oauth).

<a name="check-access_token"></a>
## Проверка access-токена

Для тестирования токена, удобно использовать метод `/me`

Пример запроса:

```http
GET /me HTTP/1.1
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
Host: api.hh.ru
Accept: */*
Authorization: Bearer access_token
```

Более подробное описание метода `/me` в соответствующих разделах:
* [для авторизованного приложения](me.md#application-info)
* [для авторизованного пользователя](me.md#user-info)

<a name="links"></a>
## Полезные ссылки

* Подробная документация по протоколу: [RFC 6749](http://tools.ietf.org/html/rfc6749)
* Библиотека [ScribeJava](https://github.com/scribejava/scribejava),
  поддерживающая авторизацию в API HeadHunter.
  * [Habrahabr: ScribeJava — даже ваша бабушка сможет работать с OAuth](https://habrahabr.ru/company/hh/blog/278957/)
