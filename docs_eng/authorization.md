# Authorization

<a name="general"></a>
To perform most API requests, an access token must be transferred.
Authorization is done via the [OAuth 2.0 protocol](#links).

Registered application can ask hh.ru users for permission to access their
personal data without getting and storing their user name and password.

The API supports the following authorisation levels:
* [application authorisation](authorization_for_application.md)
* [user authorisation](authorization_for_user.md)

---

m.hh.ru was the main API domain until April 1, 2015. It will be possible to
authorize through m.hh.ru, but from now on it is preferable to use the hh.ru
domain. Documentation has been updated in accordance with the new address.

---

* [Getting an access token](#get-access_token)
* [Using an access token](#use-access_token)
* [Checking an access token](#check-access_token)
* [Useful links](#links)

<a name="get-access_token"></a>
## Getting an access token
* Getting an [application token](authorization_for_application.md#get-client-auth)
* Getting a [user token](authorization_for_user.md#get-auth)

<a name="use-access_token"></a>
## Using an access token

The application must use the `access_token` for authorisation
by transferring it in the header in the following format:

```Authorization: Bearer ACCESS_TOKEN```

[Description of authorisation errors](errors.md#oauth).

<a name="check-access_token"></a>
## Checking an access token

It is convenient to use the `/me` method to test the token:

* [for the authorised application](me.md#application-info)
* [for the authorised user](me.md#user-info)

<a name="links"></a>
## Useful links

* Detailed documentation on the protocol: [RFC 6749](http://tools.ietf.org/html/rfc6749)
* Framework [ScribeJava](https://github.com/scribejava/scribejava)
