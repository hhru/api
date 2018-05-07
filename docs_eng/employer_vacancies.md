# Vacancies for the employer

* [Vacancy posting](#creation)
* [Vacancy fields conditions](#conditions)
* [Vacancy editing](#edit)
* [Vacancy prolongation](#prolongate)
* [Published vacancy list](#active)
* [Storing vacancies](#archive)
* [Archived vacancy list](#archived)
* [Deleting vacancies](#hide)
* [Deleted vacancy list](#hidden)
* [Restoring deleted vacancies](#restore)

See also:

* [Extra fields for the author of the vacancy](vacancies.md#author)


<a name="creation"></a>
## Vacancy posting

`POST /vacancies`


### General information

The request body should be [JSON](general.md#request-body) with data on the
vacancy being posted. The format of the data is similar to the
[vacancy view](#item), but also contains some additional fields.

> In accordance with
> [RF law № 1032-1 dated 19.04.1991, as amended on 02.07.2013](https://hh.ru/article/13967)
> it is prohibited to post information limiting rights or providing privileges
> for applicants on the base of their gender, age, marital status as well as
> other circumstances that are not related to the qualifications of employees.

* if posted successfully, a corresponding service will be written off.
* all vacancies undergo manual moderation.
* in a few minutes after having been posted, the vacancy will become available
  for search.


### Useful links

* [rules for posting vacancies](https://hh.ru/article/341)
* [how do I formulate a good vacancy description](https://hh.ru/article/16239)

<a name="creation-example"></a>
### Request body example

```json
{
    "description": "<p>— Eh bien, mon prince. Gênes et Lucques ne sont plus que des apanages, des поместья, de la famille Buonaparte. Non, je vous préviens que si vous ne me dites pas que nous avons la guerre, si vous vous permettez encore de pallier toutes les infamies, toutes les atrocités de cet Antichrist (ma parole, j'y crois) — je ne vous connais plus, vous n'êtes plus mon ami, vous n'êtes plus мой верный раб, comme vous dites. Ну, здравствуйте, здравствуйте.</p><p><em>Je vois que je vous fais peur</em>, садитесь и рассказывайте.</p>",
    "key_skills": [
        {
            "name": "Cold calling"
        },
        {
            "name": "Sales promotion"
        }
    ],
    "schedule": {
        "id": "flyInFlyOut"
    },
    "experience": {
        "id": "moreThan6"
    },
    "employment": {
        "id": "full"
    },
    "name": "Sales manager",
    "area": {
        "id": "1"
    },
    "type": {
        "id": "open"
    },
    "employer": {
        "id": "1455"
    },
    "specializations": [
        {
            "id": "17.324"
        },
        {
            "id": "3.148"
        }
    ],
    "response_letter_required": true,
    "salary": {
        "from": 100,
        "to": 500,
        "currency": "USD"
    },
    "contacts": {
        "name": "Ivanov Ivan",
        "email": "i.ivanov@example.com",
        "phones": [
            {
                "country": "7",
                "city": "495",
                "number": "1234567",
                "comment": "from 10 to 20"
            }
        ]
    },
    "accept_handicapped": true,
    "accept_kids": false,
    "code": "code-1234",
    "response_notifications": true,
    "allow_messages": true,
    "billing_type": {
        "id": "standard"
    },
    "site": {
        "id": "hh"
    },
    "address": {
        "id": "123",
        "show_metro_only": true
    },
    "manager": {
        "id": "321"
    },
    "test": {
        "id": "42",
        "required": true
    },
    "branded_template": {
        "id": "marketing"
    },
    "driver_license_types": [
        {
            "id": "A"
        },
        {
            "id": "B"
        }
    ],
    "accept_incomplete_resumes": false
}
```


<a name="creation_fields"></a>
### Request body

* `[]` (e.g. in specialization fields and in contacts) means that the value of
  the key is an array of objects.

* `a.b` means an object `a` with a key `b` of the described type.

| Path                        | JSON type       | Description |
|-----------------------------|-----------------|-------------|
| name                        | string          | title |
| description                 | string          | description in html, at least 200 characters |
| key_skills                  | array           | key skills list, no more than 30 |
| key_skills[].name           | string          | key skill name |
| specializations             | array           | specialization list |
| specializations[].id        | string          | specialization from the [directory](specializations.md) |
| area.id                     | string          | posting region from the [directory](areas.md) |
| type.id                     | string          | type from the [vacancy_type directory](dictionaries.md) |
| billing_type.id             | string          | billing type from the [vacancy_billing_type directory](dictionaries.md) |
| site.id                     | string          | website for posting from the [vacancy_site directory](dictionaries.md) |
| code                        | string          | internal vacancy code |
| department.id               | string          | department from the [directory](employer_departments.md), on behalf of which the vacancy is being posted (if this feature is available for the company) |
| salary                      | object or null  | salary |
| salary.from                 | numeric or null | salary range minimum |
| salary.to                   | numeric or null | salary range maximum |
| salary.currency             | string          | currency code from the [currency directory](dictionaries.md) |
| address                     | object or null  | address |
| address.id                  | string          | address from the [list of employer's available addresses](employer_addresses.md) |
| address.show_metro_only     | boolean         | show only metro for the indicated address |
| experience.id               | string          | required work experience from the [experience directory](dictionaries.md) |
| schedule.id                 | string          | work schedule from the [schedule directory](dictionaries.md) |
| employment.id               | string          | employment type from the [employment directory](dictionaries.md) |
| contacts                    | object          | contact information (for trade vacancies) |
| contacts.name               | string          | contact person |
| contacts.email              | string          | email |
| contacts.phones             | array           | phone number list for communication |
| contacts.phones[].country   | string          | country code |
| contacts.phones[].city      | string          | city code |
| contacts.phones[].number    | string          | telephone |
| contacts.phones[].comment   | string or null  | comment (convenient time to call this number) |
| test                        | object          | vacancy test |
| test.id                     | string          | test that will be added to the vacancy |
| test.required               | boolean         | require to take a test to apply for the vacancy |
| response_url                | string          | application URL for direct vacancies (`type.id=direct`) |
| custom_employer_name        | string          | company name for anonymous vacancies (`type.id=anonymous`), e.g. "a large Russian bank" |
| employer.id                 | string          | employer who the vacancy is being posted for |
| manager.id                  | string          | contact person (a manager) for the vacancy being posted; by default it is the current user |
| response_notifications      | boolean         | whether to notify about new applications |
| allow_messages              | boolean         | ability to [message candidates](http://inboxemp.hh.ru/) on the subject of the vacancy |
| response_letter_required    | boolean         | demand a cover letter |
| accept_handicapped          | boolean         | indication that the vacancy is available for disabled applicants |
| accept_kids                 | boolean         | indication that the vacancy is available for applicants from 14 years [read more](employer_vacancies_accept_kids.md#accept-kids)|
| branded_template.id         | string          | <a name="branded-template-field"></a> branded template from the [directory](employer_vacancy_branded_templates.md#list) |
| driver_license_types        | array           | driver license types |
| driver_license_types[].id   | string          | driver license type from [driver_license_types dictionary](dictionaries.md) |
| accept_incomplete_resumes   | boolean         | indication that applicants are allowed to respond to the vacancy using incomplete resumes |


<a name="creation-results"></a>
### Request result

* `204 No Content` – added successfully. The `Location` header will contain a
  link to the added vacancy.
* `403 Forbidden` – addition of vacancies is not available for this user or
  is not available because a vacancy with similar data had already been posted
  by this employer. If you are sure that addition of the duplicate is necessary,
  you can add the `POST /vacancies?ignore_duplicates=true` parameter to
  your request.
* `400 Bad Request` – errors in fields when adding a vacancy.

In addition to an HTTP code, the server can return
[error reasons](errors.md#vacancies-create-n-edit).


<a name="conditions"></a>
## Field filling and vacancy editing conditions

`GET /vacancy_conditions`

Each end field is described by the rules object. If the field consists of the
object with a number of fields, these fields are described in the `fields`.

The vacancy fields conditions are available only to employers, otherwise `403
Forbidden` error code will be returned.

For all the fields and their parts it is specified whether they are required
(`required`).


### Response example

Successful response will include the `200 OK` response code and will have a
body:

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
    "site": {
        "required": true
    },
    "specializations": {
        "max_count": null,
        "min_count": 1,
        "required": true
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
    }
}
```



<a name="edit"></a>
## Vacancy editing

`PUT /vacancies/{vacancy_id}`

Vacancy editing is similar to vacancy creation, but there is also a possibility to transfer separate fields in the object for partial editing of the vacancy.
Composite fields (e.g. `salary`, `contacts`, `specializations`) can be edited only wholly, indicating the entire object. For example, to edit a salary currency, one must also state the currency values, and to edit a specialization, one should also specify the entire list.


### Fields available for editing

| field                      | description                                                          |
|----------------------------|----------------------------------------------------------------------|
| name                       | title                                                                |
| description                | description                                                          |
| key_skills                 | key skills                                                           |
| schedule                   | work schedule                                                        |
| experience                 | required work experience                                             |
| employment                 | employment type                                                      |
| specializations            | specialization list                                                  |
| salary                     | salary                                                               |
| address                    | address                                                              |
| test                       | test task                                                            |
| department                 | department                                                           |
| code                       | internal vacancy code                                                |
| response_letter_required   | requirement to enclose a cover letter when applying                  |
| accept_handicapped         | indication that the vacancy is available for disabled applicants     |
| accept_kids                | indication that the vacancy is available for applicants from 14 years|
| response_notifications     | tuning of the new application notifications                          |
| allow_messages             | ability to message candidates on the subject of the vacancy          |
| contacts                   | contact information (for trade vacancies)                            |
| custom_employer_name       | company name for anonymous vacancies                                 |
| response_url               | application URL for direct vacancies                                 |

Other fields are either read-only or can be set only when creating a vacancy.


### Request result

* `204 No Content` – updated successfully.
* `404 Not Found` – the edited vacancy is not found.
* `403 Forbidden` – vacancy editing is not available for this user.
* `400 Bad Request` – errors in fields when editing a vacancy.

In addition to an HTTP code, the server can return
[error reasons](errors.md#vacancies-create-n-edit).


<a name="edit_more"></a>
### Changing the billing type, vacancy manager

Changing the vacancy billing type as well as transferring the vacancy to another
company manager is similar to editing `POST /vacancies/{vacancy_id}`. The only
feature is that these fields (`billing_type` and `manager`) must be sent
separately from other vacancy fields.

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

If sent with any other fields, an error will be returned.


<a name="other-actions"></a>
### Other actions

* [archiving](#archive)
* [deleting](#hide)
* [restoring deleted vacancies](#restore)


<a name="prolongate"></a>
## Vacancy extension

**Extension of the vacancy costs the same as a new posting**

Vacancy extension has variable limits, and at the moment, the
following rules are applied:

* standard vacancies can be extended if no less than 3 days have passed since the last extension.
* "Standard Plus" vacancies can be extended no earlier than 5 days before the posting end date.


### Request

`POST /vacancies/{vacancy_id}/prolongate`

where `vacancy_id` – ID of the vacancy.


### Response

* `204 No Content` – vacancy was extended successfully
* `403 Forbidden` – current user is not an employer or
  extension is impossible.
* `404 Not Found` – vacancy doesn't exist or current user
  is not eligible for extension.

In addition to an HTTP code, the server can return
[error reason](errors.md#vacancies-prolongate).


<a name="prolongate-info"></a>
## Info on vacancy extension availability


### Request

`GET /vacancies/{vacancy_id}/prolongate`

where `vacancy_id` – ID of the vacancy.


### Response

Successful response is returned with `200 OK` code.

Example of the response if the extension is not possible:

```json
{
    "id": "123456789",
    "expires_at": "2015-11-19T17:10:48+0300",
    "actions": [
        {
            "id": "prolongate",
            "enabled": false,
            "disable_reason": {
                "id": "standard_plus_publication_is_updated_automatically",
                "name": "The \"Standard Plus\" vacancy cannot be updated: it is updated automatically every three days."
            }
        }
    ]
}
```

Example of the response if the extension is possible:

```json
{
    "id": "123456789",
    "expires_at": "2015-11-19T17:10:48+0300",
    "actions": [
        {
            "id": "prolongate",
            "enabled": true,
            "url": "https://api.hh.ru/vacancies/123456789/prolongate",
            "method": "POST"
        }
    ]
}
```

where:

* `actions` – list of actions available for vacancy
  extension. At the moment, only regular extension is possible.
* `id` – vacancy ID.
* `expires_at` – date and time of vacancy posting termination.

Data available for the action:

* `id` – action ID,
* `enabled` – action is possible,
* `disable_reason` – reason of action disable.
  Possible reasons are listed [in reference guide](dictionaries.md)
  `vacancy_not_prolonged_reason`.
* `url` and `method` – url and HTTP method for the request to
  perform an action.

### Errors

* `403 Forbidden` – current user is not an employer.
* `404 Not Found` – vacancy doesn't exist or current user
  is not eligible to get the vacancy info.


<a name="conditions"></a>
## Field filling and vacancy editing conditions

### Rules

Name | Type | Description
--- | --- | --------
required | logical | Is the vacancy field or object field mandatory?
min_length | integer | Min length of text field.
max_length | integer | Max length of text field.
min_count | integer | Min number of objects for the fields with list transferring.
max_count | integer or `null` | Max number of objects for the fields with list transferring. `null` – the number is not limited.


<a name="active"></a>
## Published vacancy list


### Request

`GET /employers/{employer_id}/vacancies/active?manager_id={manager_id}`

To view the list of published vacancies, you should indicate the manager ID even
if you need to make a request for the current manager (the value can be taken
from `/me`).

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
                "invitations": 10
            },
            "expires_at": "2013-07-08T16:17:21+0400",
            "has_updates": false,
            "billing_type": {
                "id": "standard",
                "name": "Standard"
            },
            "can_upgrade_billing_type": true
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
| counters.resumes_in_progress   | number  | number of resumes in progress for a vacancy                                                 |
| counters.invitations       | number  | number of invitations for a vacancy                                                             |
| expires_at                 | string  | expiration date for a vacancy posting                                                           |
| has_updates                | boolean | Whether there are updates calling for attention in the applications/invitations for the vacancy |
| billing_type               | object  | Vacancy billing type. An element of dictionary [vacancy_billing_type](dictionaries.md).         |
| billing_type.id            | string  | Vacancy billing type identifier                                                                 |
| billing_type.name          | string  | Vacancy billing type name                                                                       |
| can_upgrade_billing_type   | boolean | Whether it is possible to upgrade vacancy billing type                                          |

### Errors

* `403 Forbidden` – authorization is failed or current user has no permission.


### Supported parameters

Apart from standard parameters for pagination `per_page` and `page`, the
collection supports:

* `text` – string for searching by vacancy name
* `area` – region id (see
  [the list of regions with active vacancies](employer_vacancy_areas_active.md))
* `order_by` – sorting of vacancies, possible options are available in the
  `employer_active_vacancies_order` directory


<a name="archive"></a>
## Storing vacancies

To archive a vacancy, you should send a PUT request:

`PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}`

If archived successfully, `204 No Content` will be returned.

### Errors

* `403 Forbidden` – authorization is failed or current user has no permission.


<a name="archived"></a>
## Archived vacancy list


### Request

`GET /employers/{employer_id}/vacancies/archived?manager_id={manager_id}`

To view the list of archived vacancies, you also need to indicated manager id,
even if you need to make request for the current manager (the value can be taken
from `/me`). Pagination (`per_page` and `page`) and sorting (`order_by`) are
supported. Possible sorting values are available in the
`employer_archived_vacancies_order` (`/dictionaries`) directory. As opposed to
the list of published vacancies, this collection does not support search (the
parameters `text` and `area`).


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

| key                | type   | description                          |
|--------------------|--------|--------------------------------------|
| counters.responses | number | number of applications for a vacancy |
| archived_at        | string | vacancy archivation date             |

### Errors

* `403 Forbidden` – authorization is failed or current user has no permission.


<a name="hide"></a>
## Deleting vacancies

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can delete only an archived vacancy.
If performed successfully, `204 No Content` will be returned.

### Errors

* `403 Forbidden` – authorization is failed or current user has no permission.


<a name="hidden"></a>
## Deleted vacancy list

### Request

`GET /employers/{employer_id}/vacancies/hidden?manager_id={manager_id}`

Pagination (`per_page` and `page`) and sorting (`order_by`) are supported.
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

### Errors

* `403 Forbidden` – authorization is failed or current user has no permission.


<a name="restore"></a>
## Restoring deleted vacancies

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can restore only a vacancy deleted from the archive.
If performed successfully, `204 No Content` will be returned.
The vacancy will be returned to the archive.

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - vacancy is not found or current user has no permission.
