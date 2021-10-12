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

See also:

* [Extra fields for the author of the vacancy](vacancies.md#author)

<a name="available_types"></a>
## Possible options available to current manager for publishing of vacancies

There is a need for a method to determine whether a manager can publish vacancies and what types of vacancies are available to the manager. It returns all possible types of publication.

### Request

```GET /employers/{employer_id}/managers/{manager_id}/vacancies/available_types```

where:
* `employer_id` is the employer ID, which can be found in [information on the current user](me.md#employer-info).
* `manager_id` is the manager ID. It can be found in [information on the current user](me.md#manager-info).

### Response

A successful response will return a status of `200 OK`.
The response body will contain information on options available for publishing a vacancy:

```json
{
    "items": [
        {
            "name": "Standard: without updates",
            "description": "it automatically rises in search results every 3 days; displays for 30 days. The vacancy is visible to invited applicants only. Applicants who have not been invited cannot view the vacancy nor find it using a search form",
            "available_publications_count": 21,
            "vacancy_billing_type": {
                "id": "standart"
            },
            "vacancy_types": [
                {
                    "id": "closed"
                },
                {
                    "id": "open"
                }
            ],
            "publications": [
                {
                    "name": "Moscow and the Moscow Oblast",
                    "count": 10,
                    "areas_url": "https://api.hh.ru/areas?price_region_id=1000224&vacancy_publication_flag=true"
                },
                {
                    "name": "In any region",
                    "count": 11,
                    "areas_url": "https://api.hh.ru/areas?vacancy_publication_flag=true"
                }
            ]
        },
        {
            "name": "Premium: one week in the top results",
            "description": "For the first 7 days, your publication will be highlighted, branded with your company logo, and remain in the top search results. The vacancy will be e-mailed to suitable candidates and it will be posted for 30 days.",
            "available_publications_count": 0,
            "vacancy_billing_type": {
                "id": "free"
            },
            "vacancy_types": [
                {
                    "id": "open"
                }
            ],
            "publications": []
        }
    ]
}
```

Each element in `items` may include the following fields:

Name | Type | Description
--- | --- | --------
name | string | Name of publication type
description | string | Description
available_publications_count | number | Total number of publications available to this manager. It is equal to the amount of `publications[].count` or the value indicated in the quotas if this value is lower than the above sum
vacancy_billing_type.id | string | Billing type [vacancy_billing_type directory](dictionaries.md).
vacancy_types | array | List of vacancy types
vacancy_types[].id | string | Vacancy type [vacancy_type directory](dictionaries.md)
publications | array | List of regions where the vacancy can be published and number of publications available to the employer 
publications[].name | string | Name of the region 
publications[].count | number | Number of publications in the region available to the employer
publications[].areas_url | string | URL for the list of regions where a vacancy of this type can be published. The list is returned in a tree-like structure and the vacancies are published only in the final (leaf) nodes of the tree. They are flagged as `can_publish=true`

When publishing a vacancy, `vacancy_billing_type.id` and `vacancy_type.id` values correspond to `billing_type` and `type` parameters 


### Errors

* `404 Not Found` - The current user is not an employer, the current user attempts to request data for another manager, or the manager does not have access to publish vacancies
* `404 Not Found` - Manager or company does not exist or is not available for the current user

<a name="creation"></a>
## Publishing job vacancies

`POST /vacancies`

you can additionally specify the following query-arguments:

* `ignore_duplicates=true` - force [adding duplicate](#creation-ignore-duplicates).
* `with_professional_roles=true` - force vacancy publication with professional roles instead of specializations

With argument `with_professional_roles=true` field `specializations` is not required and is ignored, field `professional_roles` is required.
Without this argument field `professional_roles` is not required and is ignored
### General information

As the response body, send
a [JSON](general.md#request-body) with the data of the job vacancy you are publishing,
the format of data is similar to [view vacancies](#item) but also contains
some additional fields.

> According to the [Federal Law of the Russian Federation No. 1032-1 dated April 19, 1991, as revised on July 2, 2013](https://hh.ru/article/13967)
> it is prohibited to place information restricting rights or providing advantages
> to certain candidates according to their gender, age, family status,
> and other qualities unrelated to their professional aptitudes.

* in case of a successful publication the cost of corresponding services will be withdrawn.
* all job vacancies are subject to manual moderation.
* within a few minutes after publication, the vacancy will become visible in search results.


### Useful links

* [conditions of publishing vacancies](https://hh.ru/article/341)
* [how to write a good vacancy description](https://hh.ru/article/16239)

<a name="creation-example"></a>
### Sample request body

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
    "specializations": [
        {
            "id": "17.324"
        },
        {
            "id": "3.148"
        }
    ],
    "professional_roles": [
        {
            "id": "59"
        }
    ],
    "response_letter_required": true,
    "salary": {
        "from": 100,
        "to": 500,
        "gross": true,
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
    "accept_incomplete_resumes": false,
    "working_days": [
        {
            "id": "only_saturday_and_sunday"
        }
    ],
    "working_time_intervals": [
        {
            "id": "from_four_to_six_hours_in_a_day"
        }
    ],
    "working_time_modes": [
        {
            "id": "start_after_sixteen"
        }
    ],
    "accept_temporary": true
}
```


<a name="creation_fields"></a>
### Request fields

* `[]` (for example, in the specialisation and contacts fields) signifies that the meaning of this key is an array of objects.

* `a.b` stands for object `a` with key `b` of the described type.

 Path                        | JSON type       | Description 
-----------------------------|-----------------|-------------
 name                        | string          | name 
 description                 | string          | html description, min. 200 characters
 key_skills                  | array           | list of key skills, max. 30
 key_skills[].name           | string          | name of key skill
 specializations             | array           | list of specialisations
 specializations[].id        | string          | specialisation [from directory](specializations.md)
 professional_roles          | array           | list of professional roles
 professional_roles[].id     | string          | professional role [from directory](https://api.hh.ru/openapi/redoc#tag/Spravochniki/paths/~1professional_roles/get)
 area.id                     | string          | city of publication [from directory](areas.md)
 type.id                     | string          | type from [vacancy_type directory](dictionaries.md)
 billing_type.id             | string          | billing type from [vacancy_billing_type directory](dictionaries.md)
 code                        | string or null  | internal vacancy code
 department.id               | string          | department [from directory](employer_departments.md) on whose behalf the vacancy is uploaded (if available for the company)
 salary                      | object or null  | salary
 salary.from                 | numeric or null | lower salary limit
 salary.to                   | numeric or null | upper salary limit
 salary.gross                | boolean         | indication that salary limits specified are before taxes
 salary.currency             | string          | currency code from [currency directory](dictionaries.md)
 address                     | object or null  | address
 address.id                  | string          | address from [list of employer's available addresses](employer_addresses.md)
 address.show_metro_only     | boolean         | show only the metro station for this address
 experience.id               | string or null  | required work experience from [experience directory](dictionaries.md)
 schedule.id                 | string or null  | working schedule from [schedule directory](dictionaries.md) |
 employment.id               | string          | employment type from [employment directory](dictionaries.md) |
 contacts                    | object or null  | contact info
 contacts.name               | string          | contact person
 contacts.email              | string          | email
 contacts.phones             | array           | list of contact phone numbers
 contacts.phones[].country   | string          | country code
 contacts.phones[].city      | string          | city code
 contacts.phones[].number    | string          | phone number
 contacts.phones[].comment   | string or null  | commentary (preferred time for calling this number)
 test                        | object or null  | vacancy test
 test.id                     | string          | [the test](employer_tests.md) that will be added to the vacancy
 test.required               | boolean         | the test is mandatory for an application
 response_url                | string          | application URL for direct vacancies (`type.id=direct`) |
 custom_employer_name        | string          | company name for anonymous vacancies (`type.id=anonymous`), for example "major bank of Russia"
 manager.id                  | string or null  | contact person (manager) for the published vacancy, by default — current user
 response_notifications      | boolean or null | notify about new applications
 allow_messages              | boolean or null | [message candidate](http://inboxemp.hh.ru/) option for this vacancy
 response_letter_required    | boolean or null | mandatory cover letter
 accept_handicapped          | boolean or null | indication that the job is available for applicants with disabilities
 accept_kids                 | boolean or null | indication that the job is available for applicants as young as 14 years old [details](employer_vacancies_accept_kids.md#accept-kids)|
 branded_template.id         | string or null  | <a name="branded-template-field"></a> branded vacancy description from [directory](employer_vacancy_branded_templates.md#list) |
 driver_license_types        | array or null   | list of required driver license categories
 driver_license_types[].id   | string          | driving license category. element of [driver_license_type](dictionaries.md) directory
 accept_incomplete_resumes   | boolean or null  | whether it is possible to apply with an incomplete resume
 working_days                | array or null   | list of working days
 working_days[].id           | string          | working days ID. element of [справочника working_days](dictionaries.md)
 working_time_intervals      | array or null   | list of working time intervals
 working_time_intervals[].id | string          | working time interval ID. element of [справочника working_time_intervals](dictionaries.md)
 working_time_modes          | array or null   | list of working time modes
 working_time_modes[].id     | string          | working time modes ID. element of [справочника working_time_modes](dictionaries.md)
 accept_temporary            | boolean or null | indication that the job is available for applicants with accept temporary employment

<a name="creation-results"></a>
### Response

Successful response is returned with `201 Created` code. 
The `Location` header will contain a link to the published vacancy:

```
HTTP/1.1 201 Created

Location: /vacancies/78789890
```

The response body will return the id of the published vacancy:

```json
{
    "id": "78789890"
}
```

### Errors

* `403 Forbidden` – current user cannot publish vacancies
* <a name="creation-ignore-duplicates"></a> `403 Forbidden` –
  the vacancy cannot be published because this employer has already published
    a vacancy with similar details. If you are sure that
    a duplicate is necessary, you can add
  `POST /vacancies?ignore_duplicates=true`.
* `400 Bad Request` – the field error argument to your request when publishing the vacancy.

In addition to the HTTP code, the server can return a description of the [error reason](errors.md#vacancies-create-n-edit).


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
Compound fields (such as `salary`, `contacts`, `specializations`) can be edited only as a whole; 
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
 specializations            | list of specialisations                                    
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
 branded_template.id        | <a name="branded-template-field"></a> branded vacancy description from [directory](employer_vacancy_branded_templates.md#list) |

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

**The cost of extending a vacancy is the same as publishing a new vacancy**

There are limits on extending vacancies, but they can change. At the moment
the following rules apply:

* standard vacancies can be extended if it has been at least 1 minute since the last extension.
* "Standard Plus" vacancies can be extended at least 7 days before the end of publication.


### Request

`POST /vacancies/{vacancy_id}/prolongate`

where `vacancy_id` – ID of the vacancy.


### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – current user is not an employer or extension is impossible.
* `404 Not Found` – current user does not have privileges to extend vacancies
* `404 Not Found` – the vacancy does not exist

In addition to an HTTP code, the server can return [error reason](errors.md#vacancies-prolongate).


<a name="prolongate-info"></a>
## Information about possible vacancy extension


### Request

`GET /vacancies/{vacancy_id}/prolongate`

where `vacancy_id` – ID of the vacancy.


### Response

Successful response is returned with `200 OK` code.

Sample response when extension is unavailable:

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
                "name": "A \"Standard Plus\" vacancy cannot be extended — it happens automatically once every three days."
            }
        }
    ]
}
```

Sample response when extension is available:

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

Where:

* `actions` – list of available actions to extend the vacancy. At the moment, the system only supports standard extension.
* `id` – vacancy ID.
* `expires_at` – publication end date and time.

The following data is available for the action:

* `id` – action ID,
* `enabled` – is the action possible,
* `disable_reason` – the reason why extension is unavailable.
  All possible reasons are listed [in the directory](dictionaries.md)
  `vacancy_not_prolonged_reason`.
* `url` and `method` – are the URL and HTTP method required to make a query for this action.

### Errors

* `403 Forbidden` – current user is not an employer.
* `404 Not Found` – the vacancy does not exist 
* `404 Not Found` – the current user cannot obtain details of this vacancy.

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
| counters.resumes_in_progress   | number  | number of resumes under revision for this vacancy                              |
| counters.invitations       | number  | number of invitations for a vacancy                                                             |
| expires_at                 | string  | expiration date for a vacancy posting                                                           |
| has_updates                | boolean | Whether there are updates calling for attention in the applications/invitations for the vacancy |
| billing_type               | object  | Vacancy billing type. [vacancy_billing_type](dictionaries.md) directory entry.         |
| billing_type.id            | string  | ID of the vacancy billing type                                                                |
| billing_type.name          | string  | Name of the vacancy billing type                                                    |
| can_upgrade_billing_type   | boolean | If the vacancy billing type can be upgraded                                          |


### Supported parameters

Apart from standard parameters for pagination `per_page` and `page`, the
collection supports:

* `text` – string for searching by vacancy name
* `area` – region id (see
  [the list of regions with active vacancies](employer_vacancy_areas_active.md))
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

Possible sorting options can be found in the [directory](dictionaries.md).

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

| key                | type   | description                          |
|--------------------|--------|--------------------------------------|
| counters.responses | number | number of applications for a vacancy |
| archived_at        | string | vacancy archivation date             |


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
