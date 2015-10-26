# Errors and response codes

API extensively uses informing through HTTP response codes. The application must
process them correctly.

When an error occurs, the response body, besides the response code, will have an
additional information that helps the developer to learn the cause of the error.

All errors are displayed in the format:

```json
{
    "errors": [
        {
            "type": "...",
            "value": "..."
        }
    ]
}
```

Several errors can be returned at the same time. The `type` key is present in
each `errors` array object and contains a text identifier of the error class.
The `value` key is optional and provides more detail on the error.

> Apart from the `errors` described above, API can optionally return other keys
> left for backward compatibility. **It is not recommended to use them.**


<a name="general-errors" />
## General errors

If the requested resource can't be found, the
`404 Not Found` response will be returned and the `errors` array will have
the object:

```json
{
    "type": "not_found"
}
```

If there is an error in request parameters (e.g.
`GET https://api.hh.ru/vacancies/?employer_id=foo`) the
`400 Bad Request` response will be returned, and the error array will have
the object:

```json
{
    "type": "bad_argument",
    "value": "employer_id"
}
```

<a name="system-errors" />
## System error

If the service can't process the request at the moment, but understood it
correctly, the `503 Service Unavailable` response will be returned and `type`
will contain `service_unavailable`.

In case of unforeseen situation, API will return 500.

In rare cases errors with 5** codes can be returned with the body that doesn't
contain the valid json. In such a case the application should rely only on the
response code.


## General request errors

<a name="user-agent" />
### Incorrect User-Agent

More detail on the [User-Agent title](general.md#request-requirements).

| HTTP code | type             | value       | description                         |
|-----------|------------------|-------------|-------------------------------------|
| 400       | bad_user_agent   | unset       | User-Agent title is not transferred |
| 400       | bad_user_agent   | blacklisted | User-Agent value in the black list  |


## Authorization errors

More detail on [authorization](authorization.md).


<a name="oauth" />
### Authorization use errors

In case you [make an authorized request](authorization.md#check-access_token) in
api and your authorization is not valid for any reason, an error with `type`
`oauth`, and, possibly, with one of the listed `values`, will be returned.

| HTTP code | type  | value                   | description  |
|-----------|-------|-------------------------|--------------|
| 403       | oauth | bad_authorization      | authorization token doesn't exist or is not valid |
| 403       | oauth | token_expired          | access_token validity period has expired, it is necessary to [refresh the access_token](authorization.md#refresh_token)  authorization.md#refresh_token |
| 403       | oauth | token_revoked          | the token is revoked by the user, the application should [request a new authorization](authorization.md) |
| 403       | oauth | application_not_found  | your application has been deleted


<a name="service-errors" />
## Errors of separate resources

If the service can return more detailed information on the
error, it will be given in the response body. In this case the response code
will likely be 400, 403, 409, 429, but other codes are also possible.

At the least, the application should process HTTP response statuses correctly.
To facilitate the work with the application, it is recommended to also process
the response type that has come. The tables listed below contain an incomplete
error list; it can be extended.


<a name="artifacts"/>
### Artifacts

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/errors.md.html#artifacts)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).



<a name="negotiations"/>
### Messaging (applications/invitations)

Apart from [general errors](#general-errors), the following errors may be
returned:

| HTTP code | type         | value                        | description  |
|-----------|--------------|------------------------------|--------------|
| 400       | negotiations | vacancy_not_found            | the vacancy has not been found  |
| 403       | negotiations | invalid_vacancy              | the vacancy has been archived or hidden |
| 400 / 403 | negotiations | resume_not_found             | the CV has not been found or hidden or deleted |
| 403       | negotiations | already_applied              | the indicated resume_id+vacancy_id pair already has an application/invitation |
| 403       | negotiations | test_required                | a test must be passed to apply (at the moment, application for such vacancies in not available via API) |
| 403       | negotiations | resume_visibility_conflict   | it is impossible to apply for an anonymous vacancy with a CV that has a "white list" visibility |
| 403       | negotiations | edit_forbidden               | message editing is not permitted |
| 403       | negotiations | application_denied           | a general application denial error in case when additional information is not available |
| 400       | negotiations | limit_exceeded               | the application number limit is exceeded |


Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/errors.md.html#negotiations)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="vacancies_favorited"/>
### Favorited vacancies

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/errors.md.html#vacancies_favorited)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="vacancies-create-n-edit"/>
### Vacancy posting & editing

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/errors.md.html#vacancies-create-n-edit)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).

