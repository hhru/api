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

`GET /vacancy_conditions`

Each end field is described by a rules object. If a field consists of
an object with several fields, these fields are described in `fields`.

Only employers have access to conditions for vacancy fields, otherwise
the system will return a response code `403 Forbidden`.

For all fields and their parts it is indicated if they are mandatory (`required`).


### Response

A successful response contains the `200 OK` response code and a body:

```json
{
    "accept_handicapped": {
        "required": false
    },
    "accept_kids": {
            "required": false
    },
    "address": {
        "fields": {
            "show_metro_only": {
                "required": false
            }
        },
        "required": false
    },
    "allow_messages": {
        "required": false
    },
    "area": {
        "required": true
    },
    "billing_type": {
        "required": true
    },
    "code": {
        "max_length": 50,
        "min_length": 0,
        "required": false
    },
    "contacts": {
        "fields": {
            "email": {
                "max_length": 255,
                "min_length": 0,
                "required": false
            },
            "name": {
                "max_length": 255,
                "min_length": 0,
                "required": true
            },
            "phones": {
                "fields": {
                    "city": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\d{0,6}$",
                        "required": true
                    },
                    "comment": {
                        "max_length": 255,
                        "min_length": 0,
                        "required": false
                    },
                    "country": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\+?\\d{0,5}$",
                        "required": true
                    },
                    "number": {
                        "max_length": 32,
                        "min_length": 4,
                        "regexp": "^[\\d -]{4,32}$",
                        "required": true
                    },
                    "formatted": {
                        "max_length": 43,
                        "min_length": 6,
                        "regexp": "^\\d{6,43}$",
                        "required": false
                  }
                },
                "max_count": 2,
                "min_count": 0,
                "required": true
            }
        },
        "required": false
    },
    "custom_employer_name": {
        "max_length": 150,
        "min_length": 0,
        "required": false
    },
    "department": {
        "max_length": 32,
        "min_length": 0,
        "required": false
    },
    "description": {
        "max_length": 10000,
        "min_length": 200,
        "required": true
    },
    "employment": {
        "required": false
    },
    "experience": {
        "required": false
    },
    "key_skills": {
        "max_count": 30,
        "min_count": 0,
        "required": false
    },
    "manager": {
        "required": false
    },
    "name": {
        "max_length": 220,
        "min_length": 0,
        "required": true
    },
    "response_letter_required": {
        "required": false
    },
    "response_notifications": {
        "required": false
    },
    "response_url": {
        "max_length": 511,
        "min_length": 0,
        "regexp": "^(http|https)://.+$",
        "required": false
    },
    "salary": {
        "fields": {
            "currency": {
                "required": false
            },
            "from": {
                "required": false
            },
            "to": {
                "required": false
            }
        },
        "required": false
    },
    "schedule": {
        "required": false
    },
    "test": {
        "fields": {
            "required": {
                "required": false
            }
        },
        "required": false
    },
    "type": {
        "required": true
    },
	"working_days": {
		"min_count": 0,
		"max_count": null,
		"required": false
	},
	"working_time_intervals": {
		"min_count": 0,
		"max_count": null,
		"required": false
	},
	"working_time_modes": {
		"min_count": 0,
		"max_count": null,
		"required": false
	},
	"accept_temporary": {
		"required": false
	}
}
```

### Rules

Name | Type | Description
--- | --- | --------
required | boolean | Is the vacancy field or object field necessary?
min_length | numeric | Minimum length for text fields.
max_length | numeric | Maximum length for text fields.
min_count | numeric | Minimum number of objects for fields with lists.
max_count | numeric or `null` | Maximum number of objects for fields with lists. `null` if the number is not limited.

### Errors

`403 Forbidden` – The conditions for filling vacancy fields are not available to this user.

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

`GET /employers/{employer_id}/vacancies/active`

By default, the system returns vacancies from the current user. If you need
vacancies from another manager, send an additional argument `manager_id={manager_id}`.
You can send only 1 `manager_id`, if you pass several, the last one will be used.

The maximum value of `per_page` is 50.

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "salary": {
                "to": null,
                "from": 30000,
                "currency": "RUR"
            },
            "name": "Secretary",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Moscow"
            },
            "url": "https://api.hh.ru/vacancies/8331228",
            "published_at": "2013-07-08T16:17:21+0400",
            "relations": [],
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/289027.png",
                    "240": "https://hh.ru/employer-logo/289169.png",
                    "original": "https://hh.ru/file/2352807.png"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455"
            },
            "response_letter_required": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/8331228",
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
            "department": {
                "id": "18320489-18320489-dept1",
                "name": "DEPT1"
            },
            "premium": false,
            "type": {
                "id": "open",
                "name": "Open"
            },
            "id": "8331228",
            "archived": false,
            "counters": {
                "views": 100500,
                "responses": 5,
                "unread_responses": 3,
                "resumes_in_progress": 5,
                "invitations": 10,
                "invitations_and_responses": 14,
                "calls": 99,
                "new_missed_calls": 11
            },
            "expires_at": "2013-07-08T16:17:21+0400",
            "has_updates": false,
            "billing_type": {
                "id": "standard",
                "name": "Standard"
            },
            "can_upgrade_billing_type": true,
            "manager": {
              "first_name": "John",
              "last_name": "Smith",
              "id": "5032",
              "middle_name": null
            }
        }
    ]
}
```

In addition to [the standard vacancy fields](vacancies.md#nano), additional
fields will be returned:

| key                        | type    | description                                                                                     |
|----------------------------|---------|-------------------------------------------------------------------------------------------------|
| counters.views             | number  | number of vacancy views                                                                         |
| counters.responses         | number  | number of applications for a vacancy                                                            |
| counters.unread_responses  | number  | number of unread applications for a vacancy                                                     |
| counters.resumes_in_progress   | number  | number of resumes under revision for this vacancy                              |
| counters.invitations       | number  | number of invitations for a vacancy                                                             |
| counters.invitations_and_responses       | number  | number of invitations and responses for a vacancy
| counters.calls | number | total number of calls on vacancy
| counters.new_missed_calls | number | number of new missed calls on vacancy
| expires_at                 | string  | expiration date for a vacancy posting                                                           |
| has_updates                | boolean | Whether there are updates calling for attention in the applications/invitations for the vacancy |
| billing_type               | object  | Vacancy billing type. [vacancy_billing_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.         |
| billing_type.id            | string  | ID of the vacancy billing type                                                                |
| billing_type.name          | string  | Name of the vacancy billing type                                                    |
| can_upgrade_billing_type   | boolean | If the vacancy billing type can be upgraded                                          |


### Supported parameters

Apart from standard parameters for pagination `per_page` and `page`, the
collection supports:

* `text` – string for searching by vacancy name
* `area` – region id (see
  [the list of regions with active vacancies](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-employer-vacancy-areas))
* `resume_id` - to work with a specific resume
* `order_by` – sorting of vacancies, possible options are available in the
  `employer_active_vacancies_order` directory

### Errors

* `400 Bad Request` – error in the request parameters
* `403 Forbidden` – current user is not an employer
* `403 Forbidden` – provided employer ID is incorrect
* `404 Not Found` – current user does not have the appropriate privileges to view published vacancies
* `404 Not Found` – manager with the passed ID does not exist

<a name="archive"></a>
## Storing vacancies

To archive a vacancy, you should send a PUT request:

`PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}`

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – current user is not an employer
* `404 Not Found` – provided employer ID is incorrect
* `404 Not Found` – current user does not have the appropriate privileges to archive the vacancy
* `404 Not Found` – vacancy with the passed ID does not exist


<a name="archived"></a>
## Archived vacancy list


### Request

`GET /employers/{employer_id}/vacancies/archived?manager_id={manager_id}`

By default, the system returns vacancies from the current user. If you need
vacancies from another manager, send an additional argument `manager_id={manager_id}`.
You can send only 1 `manager_id`, if you pass several, the last one will be used.

The system supports pagination (`per_page` and `page`) and sorting (`order_by`).

The maximum value of `per_page` is 1000.

Possible sorting options can be found in the [directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).

Unlike the list of published vacancies, the collection does not support
search (parameters `text` and `area`).


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "salary": {
                "to": null,
                "from": 30000,
                "currency": "RUR"
            },
            "name": "Secretary",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Moscow"
            },
            "url": "https://api.hh.ru/vacancies/8331228",
            "published_at": "2013-07-08T16:17:21+0400",
            "relations": [],
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/289027.png",
                    "240": "https://hh.ru/employer-logo/289169.png",
                    "original": "https://hh.ru/file/2352807.png"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455"
            },
            "response_letter_required": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/8331228",
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
            "department": {
                "id": "18320489-18320489-dept1",
                "name": "DEPT1"
            },
            "premium": false,
            "type": {
                "id": "open",
                "name": "Open"
            },
            "id": "8331228",
            "archived": true,
            "counters": {
                "responses": 3,
                "invitations_and_responses": 5
            },
            "archived_at": "2013-08-08T16:17:21+0400"
        }
    ]
}
```

In addition to [the standard vacancy fields](vacancies.md#nano), additional
fields will be returned:

| key                                | type   | description                                          |
|------------------------------------|--------|------------------------------------------------------|
| counters.responses                 | number | number of applications for a vacancy                 |
| counters.invitations_and_responses | number | number of applications and invitations for a vacancy |
| archived_at                        | string | vacancy archivation date                             |


### Errors

* `400 Bad Request` – error in the request parameters
* `403 Forbidden` – current user is not an employer.
* `403 Forbidden` – invalid employer id is specified.
* `404 Not Found` – the current user cannot obtain archive vacancies.

<a name="hide"></a>
## Deleting vacancies

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can delete only an archived vacancy.

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – current user is not an employer
* `403 Forbidden` – it is forbidden to delete a job that is not archived
* `404 Not Found` – provided employer ID is incorrect
* `404 Not Found` – current user does not have privileges to delete archived vacancies
* `404 Not Found` – vacancy with the passed ID does not exist


<a name="hidden"></a>
## Deleted vacancy list

### Request

`GET /employers/{employer_id}/vacancies/hidden?manager_id={manager_id}`

By default, the system returns vacancies from the current user. If you need
vacancies from another manager, send an additional argument `manager_id={manager_id}`.
You can send only 1 `manager_id`, if you pass several, the last one will be used.

Pagination (`per_page` and `page`) and sorting (`order_by`) are supported.

The maximum value of `per_page` is 1000.

Possible sorting values are available in the `employer_hidden_vacancies_order`
(`/dictionaries`) directory. As opposed to the list of published vacancies, this
collection does not support search (the parameters `text` and `area`).


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "salary": {
                "to": null,
                "from": 30000,
                "currency": "RUR"
            },
            "name": "Secretary",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Moscow"
            },
            "url": "https://api.hh.ru/vacancies/8331228",
            "published_at": "2013-07-08T16:17:21+0400",
            "relations": [],
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/289027.png",
                    "240": "https://hh.ru/employer-logo/289169.png",
                    "original": "https://hh.ru/file/2352807.png"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455"
            },
            "response_letter_required": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/8331228",
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
            "department": {
                "id": "18320489-18320489-dept1",
                "name": "DEPT1"
            },
            "premium": false,
            "type": {
                "id": "open",
                "name": "Open"
            },
            "id": "8331228",
            "archived": true
        }
    ]
}
```

Response with [the standard vacancy fields](vacancies.md#nano) will be returned.

### Ошибки

* `400 Bad Request` – error in the request parameters
* `403 Forbidden` – current user is not an employer
* `403 Forbidden` – provided employer ID is incorrect
* `404 Not Found` – current user does not have the appropriate privileges to view deleted vacancies

<a name="restore"></a>
## Restoring deleted vacancies

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can restore only a vacancy deleted from the archive.

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – current user is not an employer
* `403 Forbidden` – restoring a non-deleted vacancy is forbidden
* `404 Not Found` – provided employer ID is incorrect
* `404 Not Found` – current user does not have privileges to restore deleted vacancies
* `404 Not Found` – vacancy with the passed ID does not exist

<a name="stats"></a>
## Vacancy statistics

`GET /vacancies/{vacancy_id}/stats`

where `vacancy_id` - vacancy ID

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "date": "2017-01-10",
            "responses": 1,
            "views": 36
        },
        {
            "date": "2017-01-11",
            "responses": 4,
            "views": 35
        },
        {
            "date": "2017-01-12",
            "responses": 1,
            "views": 32
        },
        {
            "date": "2017-01-13",
            "responses": null,
            "views": null
        },
        {
            "date": "2017-01-14",
            "responses": null,
            "views": null
        }
    ]
}
```

Each element from `items` has the following fields:

Name | Type | Description
--- | --- | ---
date | string | Date in format `YYYY-MM-DD`
responses | number or null | Number of applications, `null` if the date is in the future or there is no data for this date
views | number or null | Number of views, `null` if the date is in the future or there is no data for this date

The system returns a window of the last 5 days of the publication life:

* if the vacancy was created after the start of the window, the vacancy publication date will go first;
* if the vacancy is archived or deleted, the archiving date will go last.

### Errors

* `403 Forbidden` – current user is not an employer
* `404 Not Found` – vacancy with the passed ID does not exist


<a name="visitors"></a>
## Vacancy visitors

`GET /vacancies/{vacancy_id}/visitors`

Success response returns a list of CV of users who viewed the vacancy in the last week. List sorted by viewing date
descending. If the user has multiple CVs, then a CV with the latest update date will be returned.


Parameters:

Name | Required | Description
--- | ------------ | --------
vacancy_id| yes | Vacancy ID
page | no | Page number, default: 0
per_page | no | Number of items per page: default value is 20; the maximum value is 50

### Response

Successful server response is returned with `200 OK` code and contains:
```json
{
  "found": 12,
  "pages": 1,
  "page": 0,
  "per_page": 20,
  "hidden_on_page": 0,
  "items": [
    {
      "id": "0123456789abcdef",
      "title": "Young specialist",
      "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
      "first_name": "Ivan",
      "last_name": "Ivanov",
      "middle_name": "Ivanovich",
      "age": 19,
      "alternate_url": "https://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
      "created_at": "2015-02-06T12:00:00+0300",
      "updated_at": "2015-04-20T16:24:15+0300",
      "area": {
        "id": "1",
        "name": "Moscow",
        "url": "https://api.hh.ru/areas/1"
      },
      "certificate": [
        {
          "achieved_at": "2015-01-01",
          "owner": null,
          "title": "test",
          "type": "custom",
          "url": "http://example.com/"
        }
      ],
      "education": {
        "primary": [
          {
            "name": "Russian State Social University, Moscow",
            "name_id": "39420",
            "organization": "IT Department",
            "organization_id": null,
            "result": "",
            "result_id": null,
            "year": 2012
          }
        ],
        "level": {
          "id": "higher",
          "name": "Higher"
        }
      },
      "total_experience": {
        "months": 118
      },
      "experience": [
        {
          "area": {
            "id": "1",
            "name": "Moscow",
            "url": "https://api.hh.ru/areas/1"
          },
          "company": "Roga i Kopyta",
          "company_id": null,
          "company_url": "http://example.com/",
          "employer": null,
          "end": "1999-03-01",
          "industries": [
            {
              "id": "45.507",
              "name": "Mining and dressing of ferrous, non-ferrous, precious, noble and rare metals"
            }
          ],
          "industry": null,
          "start": "1998-01-01"
        }
      ],
      "gender": {
        "id": "male",
        "name": "Male"
      },
      "salary": {
        "amount": 1000000,
        "currency": "RUR"
      },
      "owner": {
        "id": "123456",
        "comments": {
          "url": "https://api.hh.ru/applicant_comments/123456",
          "counters": {
            "total": 7
          }
        }
      },
      "negotiations_history": {
        "url": "https://api.hh.ru/resumes/0123456789abcdef/negotiations_history"
      },
      "download": {
        "pdf": {
          "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.pdf?type=pdf"
        },
        "rtf": {
          "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.rtf?type=rtf"
        }
      }
    }
  ]
}
```
where:

Name | Type | Description
--- | --- | --------
found | number | Number of CVs found ( ≥ 0 )
pages | number | Number of pages with CVs ( ≥ 1 )
per_page | number | Number of elements per page ( > 0 )
page | number | Number of the current page ( ≥ 0 )
hidden_on_page | number | Number of deleted or hidden CVs on the page ( ≥ 0 )


The `items` entity contains list of [short CV's](resumes.md#resume-short).

If the applicant has deleted or hidden the resume from the employer, then in the list of `items` these CVs
will be skipped, but will be taken into account during pagination (`per_page`) and in the number of CVs found (`found`),
the field `hidden_on_page` indicates the number of such omitted CVs per page.

For example

```json
{
   "found": 12,
   "pages": 2,
   "page": 0,
   "per_page": 10,
   "hidden_on_page": 5,
   "items": [
     // ...
   ]
}
```

This response indicates that 12 CVs were found in total, the first page is requested with `per_page=10`.
`hidden_on_page=5` in the response indicates that there are only 5 items in the `items` list and 5 CVs are omitted.

### Errors

* `400 Bad Request` - error in the request parameters
* `404 Not Found` - if the vacancy of requested visitors doesn't exist or
  not available to the current user

