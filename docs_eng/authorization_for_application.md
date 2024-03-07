# Application authorization

The application token must be generated once.
If the token was compromised, it must be requested again. In this case, the previously issued token is revoked.
The application owner can view the valid `access_token` for the application on the website [https://dev.hh.ru/admin](https://dev.hh.ru/admin). If you have never [received an application token](#get-client-auth), it will not be displayed.

<a name="get-client-auth"></a>
## Getting an application token

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/#tag/Application-authorization)