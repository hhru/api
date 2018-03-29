# Employer's branded vacancy templates

Branded templates are available for those employers who paid for
and activated the respective service.
See more details on the [hh.ru website](https://hh.ru/article/2069).

Branded templates can be used for
[vacancy posting and editing](employer_vacancies.md#branded-template-field).


<a name="list"></a>
## List

List of all templates available from the employer.


<a name="list-request"></a>
### Request

`GET /employers/{employer_id}/vacancy_branded_templates`

where `employer_id` – company ID available
[from the information on current user](me.md#employer-info).

### Errors

* `403 Forbidden` – authorization is failed.


<a name="list-response"></a>
### Response

Successful server response is returned with `200 OK` code and contains the list
of templates with template ID and name.

```json
{
    "items": [
        {
            "id": "marketing",
            "name": "Marketing"
        },
        {
            "id": "tech",
            "name": "Technical department"
        }
    ]
}
```

<a name="list-errors"></a>
### Errors

* `404 Not Found` – templates for this company are not available or
  the company doesn't exist.
* `403 Forbidden` – current user is not authorized or is not
  an employer.
