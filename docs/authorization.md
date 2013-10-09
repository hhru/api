Авторизация
===========

Авторизация осуществляется по протоколу OAuth 2.0. Зарегистрированное приложение может запрашивать у пользователей 
HH.ru разрешение доступа к их персональным данным, без получения и хранения их логина и пароля.

1. Приложение направляет пользователя по адресу:
`https://m.hh.ru/oauth/authorize?response_type=code&client_id={CLIENT_ID}&state={STATE}`. Параметр `state` опционален, в случае
его указания, он будет включен в ответный редирект — это позволяет исключить возможность взлома путём подделки межсайтовых запросов. Подробнее об этом: 
[RFC 6749. Section 10.12](http://tools.ietf.org/html/rfc6749#section-10.12)

2. После прохождения авторизации на сайте, мы запрашиваем у пользователя разрешение доступа приложения к его 
персональным данным.

3. Если пользователь не разрешает доступ приложению, мы перенаправляем  пользователя на указанный `redirect_uri` с `?error=access_denied` и `state={STATE}`, если таковой был указан при первом запросе.
Иначе в редиректе мы указываем временный `authorization_code`:
```http
HTTP/1.1 302 FOUND
Location: {REDIRECT_URI}?code=...
```

4. Приложение делает сервер-сервер POST-запрос на `https://m.hh.ru/oauth/token` для обмена полученного `authorization_code` на `access_token`.
В запросе необходимо передать:
```
grant_type=authorization_code&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&code={CODE}
```
Тело запроса необходимо передавать в стандартном `application/x-www-form-urlencoded` с указанием соответствующего заголовка  `Content-Type`.
        
    Ответ:
  ```json
  {
      "access_token": "{ACCESS_TOKEN}",
      "token_type": "bearer",
      "refresh_token": "{REFRESH_TOKEN}",
      "expires_in": 1209600
  }
  ```

    `authorization_code` имеет довольно короткий срок жизни, при его истечении необходимо запросить новый.

5. Приложение использует полученный `access_token` для авторизации, передавая его в заголовке. Для тестирования 
токена, удобно использовать метод `/me`.
```http
GET /me HTTP/1.1
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
Host: api.hh.ru
Accept: */*
Authorization: Bearer ACCESS_TOKEN
```
JSON в ответе:
```json
{
  "id": "12345678",
  "first_name": "Имя",
  "last_name": "Фамилия",
  "is_admin": false,
  "is_applicant": true,
  "is_employer": false,
  "mid_name": "Отчество",
  "email": "contact@example.com",
  "employer": null
}
```
6. `access_token` имеет срок жизни, при его истечении приложение делает запрос с `refresh_token` для получения нового. Запрос необходимо делать в `application/x-www-form-urlencoded` по аналогии с п.4 

        POST https://m.hh.ru/oauth/token
        grant_type=refresh_token&refresh_token={REFRESH_TOKEN}



Примечания
----------

* Подробная документация по протоколу: [RFC 6749](http://tools.ietf.org/html/rfc6749)
