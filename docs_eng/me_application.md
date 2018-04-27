# Authorized application

* [Obtaining info on the authorized application](#info)


<a name="info"></a>
## Obtaining info on the authorized application

`GET /me` returns info on current authorized user. Server returns `403 Forbidden` if authorization is failed.

> :warning: At the moment, only flags are present in the response. In the future, the response body can be expanded.

```json
{
    "is_admin": false,
    "is_applicant": false,
    "is_employer": false,
    "is_application": true
}
```


Name | Type | Description
--- | --- | ---
is_admin | logical | user is site administrator
is_applicant | logical | true, if the user is an applicant
is_employer | logical | true, if the user is an employer
is_application | logical | true, if it is authorized application
