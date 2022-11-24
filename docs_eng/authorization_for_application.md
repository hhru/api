# Application authorization

The application token must be generated once.
If the token was compromised, it must be requested again. In this case, the previously issued token is revoked.
The application owner can view the valid `access_token` for the application on the website [https://dev.hh.ru/admin](https://dev.hh.ru/admin). If you have never [received an application token](#get-client-auth), it will not be displayed.

<a name="get-client-auth"></a>
## Getting an application token

### Request

To get an `access_token` you need to execute the following request:

```
POST https://hh.ru/oauth/token
```

Additional parameters should be transferred within the request body:

* `grant_type=client_credentials`
* `client_id` and `client_secret` - this must be filled in with the values obtained when [registering the application](https://dev.hh.ru/admin).

The request body should be transferred within the standard `application/x-www-form-urlencoded` along with the corresponding `Content-Type` header.

### Response
JSON will be returned in the response:

```json
{
    "access_token": "{access_token}",
    "token_type": "bearer"
}
```


This `access_token` has an **unlimited** lifetime. Upon repeated request, the previously issued token is revoked, and a new token is issued. `access_token` can be requested no more than once every 5 minutes.

> :warning: In the case of a compromised token, you must request it again!

### Errors

* `400 Bad Request` – error in the request parameters.
* `403 Forbidden` – the maximum frequency of requests for application tokens has been exceeded.

In addition to the HTTP code, the server can return a description of the [error cause](errors.md#oauth-get-errors).