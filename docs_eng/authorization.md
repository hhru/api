# Authorization

* [Obtaining authorization](#get-auth)
  * [Special redirect_uri formation rules](#redirect_uri)
  * [Authorization process](#get-auth-process)
  * [Obtaining a temporary `authorization_code` successfully](#get-authorization_code)
  * [Obtaining access and refresh tokens](#get-tokens)
* [Refreshing the access and refresh token pair](#refresh_token)
* [Obtaining application authorization](#get-client-auth)
* [Using and testing access_token](#check-access_token)
* [Authorization request for another user](#force-login)
* [Useful links](#links)


<a name="general"></a>
Authorization is done via the OAuth 2.0 protocol. Detailed documentation on the
protocol: [RFC 6749](http://tools.ietf.org/html/rfc6749).

API supports the following authorization levels:
* [user authorization](#get-auth)
* [application authorization](#get-client-auth)

Registered application can ask hh.ru users for permission to access their
personal data without getting and storing their user name and password.

---

m.hh.ru was the main API domain until April 1, 2015. It will be possible to
authorize through m.hh.ru, but from now on it is preferable to use the hh.ru
domain. Documentation has been updated in accordance with the new address.

---


<a name="get-auth"></a>
## Obtaining authorization

First, the application needs to direct the user (open the page) to the address:

```
https://hh.ru/oauth/authorize?response_type=code&client_id={client_id}&state={state}&redirect_uri={redirect_uri}
```

Mandatory parameters:

* `response_type=code` – indicates the method of obtaining authorization,
  using authorization code;
* `client_id={client_id}` – identifier obtained when creating
  the application;


Optional parameters:

* `state={state}` – if indicated, will be included in the response redirect.
  This eliminates the possibility of cross-site request forgery.
  More information on this: [RFC 6749. Section 10.12](http://tools.ietf.org/html/rfc6749#section-10.12)

* `redirect_uri={redirect_uri}` – uri for redirecting the user after the
  authorization. If not indicated, used from the application settings. If
  present, the value is validated.



<a name="redirect_uri"></a>
### Special redirect_uri formation rules

For example, if `http://example.com/oauth` is saved in the application settings,
then it is permitted to indicate:

* `http://www.example.com/oauth` — subdomain;
* `http://www.example.com/oauth/sub/path` — path specification;
* `http://example.com/oauth?lang=RU` — extra parameter;
* `http://www.example.com/oauth/sub/path?lang=RU` — all at once.

It is not permitted to indicate:

* `https://example.com/oauth` — various protocols;
* `http://wwwexample.com/oauth` — various domains;
* `http://wwwexample.com/` — another path;
* `http://example.com/oauths` — another path;
* `http://example.com:80/oauths` — an originally absent port;


<a name="get-auth-process"></a>
### Authorization process

If the user is not authorized on the website, they will be showed the website
authorization form. After the user is authorized, they will be showed a form
requesting access for your application to their personal data.

If the user denies access for the application, the user will be redirected to
the indicated `redirect_uri` with `?error=access_denied` and
`state={state}`, if such was indicated in the first request.


<a name="get-authorization_code"></a>
### Obtaining a temporary `authorization_code` successfully

If access is allowed, a temporary `authorization_code` will be indicated in the
redirect:

```http
HTTP/1.1 302 FOUND
Location: {redirect_uri}?code={authorization_code}
```

If the user is authorized on the website and access has been granted to the
application once before, then there will be an immediate redirect with the
`authorization_code` described above (without showing the login form and giving
rights).


<a name="get-tokens"></a>
### Obtaining access and refresh tokens

After obtaining the `authorization_code`, the application needs to send a
server-server request `POST https://hh.ru/oauth/token` to change the
`authorization_code` obtained for an `access_token`.

The request body should contain the following information:

```
grant_type=authorization_code&client_id={client_id}&client_secret={client_secret}&code={authorization_code}&redirect_uri={redirect_uri}
```

If, when obtaining the `authorization_code`, `redirect_uri` was indicated, then
this value must be sent in the request (strings are compared); otherwise this
parameter is optional. If `redirect_uri` is not indicated when requesting
`/oauth/authorize`, then, when indicating it in the second request
(`/oauth/token`), the server will return an error.

Request body must be sent in standard `application/x-www-form-urlencoded`
with the indication of a corresponding header `Content-Type`.

JSON will be returned in the response:

```json
{
  "access_token": "{access_token}",
  "token_type": "bearer",
  "expires_in": 1209600,
  "refresh_token": "{refresh_token}"
}
```

`authorization_code` has quite a short validity period; when it expires, a new
one must be requested.

If the `authorization_code` exchange fails, then the `400 Bad Request`
response returns with the body:

```json
{
    "error": "invalid_request",
    "error_description": "account not found"
}
```

where:

* `error` will have one of the values
  [described in the RFC 6749 standard](http://tools.ietf.org/html/rfc6749#section-5.2).
  For instance, `invalid_request`, if one of the mandatory parameters has not
  been sent.
* `error_description` will contain an additional description of the error.


<a name="refresh_token"></a>
## Refreshing the access and refresh token pair

access_token also has a validity period (key `expires_in`, in seconds). When it
expires, the application must make a request with `refresh_token` to obtain
a new one.

The request must be made in `application/x-www-form-urlencoded`.

```
POST https://hh.ru/oauth/token
grant_type=refresh_token&refresh_token={refresh_token}
```

The response will be identical to the one received when obtaining tokens for the
first time:

```json
{
  "access_token": "{access_token}",
  "token_type": "bearer",
  "expires_in": 1209600,
  "refresh_token": "{refresh_token}",
}
```

`refresh_token` can be used only once and only when the `access_token` validity
period expires.

When a new access and refresh token pair is received, it should be used in
further api requests and token renewal requests.


<a name="get-client-auth"></a>
## Obtaining application authorization

For obtaining an `authorization_code`, the application needs to send a
server-server request `POST https://hh.ru/oauth/token`.

The request body should contain the following information:

```
grant_type=client_credentials&client_id={client_id}&client_secret={client_secret}
```

Request body must be sent in standard `application/x-www-form-urlencoded`
with the indication of a corresponding header `Content-Type`.

JSON will be returned in the response:

```json
{
  "access_token": "{access_token}",
  "token_type": "bearer"
}
```

The `access_token` has **unlimited** validity period. After repeated request, the previously obtained token is deactivated and a new one is obtained. The owner of the application can see the actual `access_token` for the application on the site [https://dev.hh.ru/admin](https://dev.hh.ru/admin).

> :warning: In case of compromising the token, you need to go through the procedure for obtaining an application access token again.

If the obtaining fails, then the `400 Bad Request` response returns with the body:

```json
{
    "error": "invalid_client",
    "error_description": "client_id or client_secret not found"
}
```

where:

* `error` will have one of the values
  [described in the RFC 6749 standard](http://tools.ietf.org/html/rfc6749#section-5.2).
  For instance, `invalid_request`, if one of the mandatory parameters has not
  been sent.
* `error_description` will contain an additional description of the error.


<a name="check-access_token"></a>
### Using and testing access_token

The application must use the obtained `access_token` for authorization, sending
it in the title in the format:

```Authorization: Bearer ACCESS_TOKEN```

To test the token, it is convenient to use the `/me` method (it is an optional
step).

```http
GET /me HTTP/1.1
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
Host: api.hh.ru
Accept: */*
Authorization: Bearer access_token
```

Documentation on the response from `/me` [in the corresponding section](me.md).

Documentation on the response from `/me` in the corresponding section:
* [authorized user](me.md#user-info)
* [authorized application](me.md#application-info)

[Authorization error description](errors.md#oauth).

<a name="force-login"></a>
### Authorization request for another user

The following scenario is possible:

1. The application redirects the user to the website with the authorization
   request.
2. The user is already authorized on the website, and the application has
   already been granted access.
3. Then the user is immediately redirected with a temporary token, and the
   application exchanges it for an `access_token`.

In this case the user authorized on the website is granted access automatically.
If it is necessary to request access for another user, the application can add
the `force_login=true` parameter to the `/oauth/authorize...` request. In
this case the user will be showed an authorization form with the user name and
password fields even if the user is already authorized.

This can be helpful for applications that provide service only for applicants.
If the user is an employer, then the application can offer the user to obtain
website access again by indicating another account.

Also, after the authorization the application can show the following message to
the user:

```
You have logged in as %Name_Surname%. Not you?
```

and give a link with `force_login=true` for the user to be able to log in using
a different account.


<a name="links"></a>
## Useful links

* Detailed documentation on the protocol:
  [RFC 6749](http://tools.ietf.org/html/rfc6749)
