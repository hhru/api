<a name="accept-kids"></a>
# Indication that the vacancy is available for applicants from 14 years 

Post of vacancies for applicants from 14 years old is allowed only on the territory of Russian Federation.

By default, only confirmed Russian employers have permissions to post such vacancies. 
To obtain permission to post vacancy for applicants from 14 years old, contact your personal manager.

## Vacancy posting

To post vacancy for applicants from 14 years old, add field to request body
```json
{
    "accept_kids": true
}
```
[Main article about vacancy posting](employer_vacancies.md#creation)

## Vacancy editing

`PUT /vacancies/{vacancy_id}` 

Request body:
```json
{
    "accept_kids": true
}
```
[Main article about vacancy editing](employer_vacancies.md#edit)

<a name="edit-results"></a>
## Error and HTTP response code

In addition to an HTTP code `400 Bad Request`, the server will return error reason
```json
{
    "errors": [
        {
            "type": "vacancies",
            "value": "can_not_accept_kids"
        }
    ]
}
```

## Additional information

[https://hh.ru/article/20732](https://hh.ru/article/20732)
