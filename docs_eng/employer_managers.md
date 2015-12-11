# Employer's manager directory

To learn the list of employer's managers, one should send the `GET` request to
`/employers/{employer_id}/managers`.

This directory is available only for employers.

If the request is performed successfully, the status `HTTP 200 OK` will be
returned. Employer's manager list will be returned in the response body, for
example:

```json
{
    "items": [
        {
            "id": "1507922",
            "email": "employer@example.com",
            "name": "Ivanov Ivan Ivanovich",
            "vacancies_count": 0
        }
    ]
}
```

The `items` element will contain the list of employer's managers.
Each element from `items` has the following fields:

| Name             | Type   | Description                                                |
|------------------|--------|------------------------------------------------------------|
| id               | string | Manager's identifier                                       |
| email            | string | Manager's e-mail                                           |
| name             | string | Manager's full name                                        |
| vacancies_count  | number | the number of (active) vacancies published by this manager |

In case the current user is not allowed to view the employer's managers, the
`HTTP 403 Forbidden` code will be returned.
