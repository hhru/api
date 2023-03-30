# Vacancies for the employer

* [Possible options available to current manager for publishing of vacancies](employer_vacancies.md#available_types)
* [Publishing job vacancies](#creation)
* [Conditions for filling out fields when publishing and adding vacancies](#conditions)
* [Editing vacancies](#edit)
* [Editing billing type or vacancy manager](#edit_more)
* [Extending vacancies](#prolongate)
* [Information about possible vacancy extension](#prolongate-info)
* [Published vacancy list](#active)
* [Storing vacancies](#archive)
* [Archived vacancy list](#archived)
* [Deleting vacancies](#hide)
* [Deleted vacancy list](#hidden)
* [Restoring deleted vacancies](#restore)
* [Vacancy statistics](#stats)
* [Vacancy visitors](#visitors)

See also:

* [Extra fields for the author of the vacancy](vacancies.md#author)

<a name="available_types"></a>
## Possible options available to current manager for publishing of vacancies

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Manager-info/operation/get-available-vacancy-types)

<a name="creation"></a>
## Publishing job vacancies

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/publish-vacancy)

<a name="conditions"></a>
## Conditions for filling out fields when publishing and adding vacancies

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-vacancy-conditions)

<a name="edit"></a>
## Editing vacancies

`PUT /vacancies/{vacancy_id}`

* `ignore_duplicates=true` - ignore [duplicates](#edit-ignore-duplicates) after editing the vacancy.

Editing is similar to publishing a vacancy but with an option to send individual fields in an object for partial editing.
Compound fields (such as `salary`, `contacts`, `professional_roles`) can be edited only as a whole; 
the entire object will be sent. For example, to edit salary currency, you will also have to change the salary value;
to change the specialisation you will have to send a full list.

### Editable fields

 field                      | description                                                          
----------------------------|----------------------------------------------------------------------
 name                       | title                                                                
 description                | description                                                          
 key_skills                 | key skills                                                           
 schedule                   | work schedule                                                        
 experience                 | required work experience                                     
 employment                 | type of employment                                                   
 professional_roles         | list of professional roles
 salary                     | salary                                                               
 address                    | address                                                              
 test                       | test task                                                           
 department                 | department                                                           
 code                       | internal vacancy code                                          
 response_letter_required   | mandatory application cover letter              
 accept_handicapped         | indication that the job is available for applicants with disabilities   
 accept_kids                | indication that the job is available for applicants as young as 14 years old
 response_notifications     | notification about new applications                 
 allow_messages             | "message candidate" option for this vacancy
 contacts                   | contact info                     
 custom_employer_name       | company name for anonymous vacancies                                 
 response_url               | application URL for direct vacancies   
 accept_incomplete_resumes  | whether it is possible to apply with an incomplete resume   
 branded_template.id        | <a name="branded-template-field"></a> branded vacancy description from [directory](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-vacancy-branded-templates-list) |
 languages                  | list of languages
driver_license_types        | driver's license category. Item of the `driver_license_types` [dictionary](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
The remaining fields are read-only or can only be set during initial publication.

### Response

A successful response contains a code `204 No Content`.

### Errors

* `404 Not Found` – vacancy for editing not found.
* `403 Forbidden` – current user cannot edit vacancies.
* `400 Bad Request` – error found in a field when editing the vacancy.
* <a name="edit-ignore-duplicates"></a> `403 Forbidden` –
  the vacancy cannot be edited, because editing makes the vacancy
    similar to another vacancy from the same employer. If you are sure that
    a duplicate is necessary, you can add
  `PUT /vacancies/{vacancy_id}?ignore_duplicates=true`.

In addition to the HTTP code, the server can return a description of the [error reason](errors.md#vacancies-create-n-edit).


<a name="edit_more"></a>
### Editing billing type or vacancy manager

You can only improve the vacancy type.

Editing the billing type of a vacancy or passing the vacancy to another
manager in the company is similar to editing `PUT /vacancies/{vacancy_id}`. 
The only peculiarity is that the following fields (`billing_type` and `manager`) 
must be sent separately from the remaining fields of the vacancy.

```
PUT /vacancies/{vacancy_id}
```

```json
{
    "billing_type": {
        "id": "premium"
    }
}
```

and

```
PUT /vacancies/{vacancy_id}
```

```json
{
    "manager": {
        "id": "1337"
    }
}
```

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `404 Not Found` – vacancy for editing not found.
* `403 Forbidden` – current user cannot edit vacancies.
* `403 Forbidden` – `billing_type` and `manager` are passed along with others.

In addition to the HTTP code, the server can return a description of the [error reason](errors.md#vacancies-create-n-edit).

<a name="other-actions"></a>
### Other actions

* [archive](#archive)
* [delete](#hide)
* [restore from deleted](#restore)


<a name="prolongate"></a>
## Extending vacancies
> > !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/vacancy-prolongation) specification.

## Information about possible vacancy extension
> > !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-prolongation-vacancy-info) specification.

<a name="active"></a>
## Published vacancy list

> > !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancies/operation/get-active-vacancy-list)

<a name="archive"></a>
## Storing vacancies

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/add-vacancy-to-archive)

<a name="archived"></a>
## Archived vacancy list

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-archived-vacancies)

<a name="hide"></a>
## Deleting vacancies

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/add-vacancy-to-hidden)

<a name="hidden"></a>
## Deleted vacancy list

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-hidden-vacancies)

<a name="restore"></a>
## Restoring deleted vacancies

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/restore-vacancy-from-hidden)

<a name="stats"></a>
## Vacancy statistics

> > !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-vacancy-stats)

<a name="visitors"></a>

> > !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancies/operation/get-vacancy-visitors)
