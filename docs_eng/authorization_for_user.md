# User authorisation

* [Obtaining user authorization](#get-auth)
  * [Special redirect_uri formation rules](#redirect_uri)
  * [Authorization process](#get-auth-process)
  * [УObtaining a temporary `authorization_code` successfully](#get-authorization_code)
  * [Obtaining access and refresh tokens](#get-tokens)
* [Refreshing the access and refresh token pair](#refresh_token)
* [Access token invalidation](#invalidate_token)
* [Authorization request for another user](#force_login)
* [Login to different work accounts](#implant)

<a name="get-auth"></a>
## Obtaining user authorization

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

<a name="get-tokens"></a>
### Obtaining access and refresh tokens

After obtaining the `authorization_code`, the application needs to send a
server-server POST request to`https://hh.ru/oauth/token` to change the
`authorization_code` obtained for an `access_token`.

The request body should contain the following information:

* `grant_type=authorization_code`
* `client_id={client_id}`
* `client_secret={client_secret}`
* `code={authorization_code}`

If, when obtaining the `authorization_code`, `redirect_uri` was indicated, then
this value must be sent in the request (strings are compared); otherwise this
parameter is optional. If `redirect_uri` is not indicated when requesting
`/oauth/authorize`, then, when indicating it in the second request
(`/oauth/token`), the server will return an error.

Request body must be sent in standard `application/x-www-form-urlencoded`
with the indication of a corresponding title `Content-Type`.

JSON will be returned in the response:

```json
{
  "access_token": "{access_token}",
  "token_type": "bearer",
  "expires_in": 1209600,
  "refresh_token": "{refresh_token}",
}
```

`authorization_code` has quite a short validity period; when it expires, a new
one must be requested.

If the `authorization_code` exchange fails, then the `400 Bad Request`
response returns with the body:

```json
{
    "error": "...",
    "error_description": "..."
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

<a name="invalidate_token"></a>
## Access token invalidation

To invalidate access token make the request:

```
DELETE https://api.hh.ru/oauth/token
```

[Passing active token like for any other authorized api request](authorization.md#use-access_token):

```Authorization: Bearer ACCESS_TOKEN```

Invalidation works only for active tokens.

After access token had been invalidated, it can't be refreshed with corresponding refresh token - new authorization is required for user to continue using api.

Only user token can be invalidated in same way.

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – If active user access token was not used for request.

<a name="force_login"></a>
### Authorization request for another user

The following scenario is possible:

1. The application redirects the user to the website with the authorization
   request.
2. The user is already authorized on the website, and the application has
   already been granted access.
3. The user will be asked if they want to continue using the current account or log in under a different account.

If a redirect is required with a temporary token in step 3,
add the `skip_choose_account=true` parameter to the `/oauth/authorize...` request.
In this case, access is automatically provided to the user authorised on the website.

If the authorisation form should always be shown, the application can
add the `force_login=true` parameter to the `/oauth/authorize...` request.
In this case the user will be showed an authorization form with the user name and
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

<a name="implant"></a>
## Login to different work accounts

It is necessary to read the documentation on Manager Work Accounts in order to get a list of the Manager Work Accounts and to work on different [Manager Work Accounts](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/operation/get-manager-accounts).
