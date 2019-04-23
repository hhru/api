# Employer's managers

* [Directory of manager types and privileges](#dict)
* [Adding a manager](#add)
* [Editing a manager](#edit)
* [Deleting a manager](#delete)
* [Directory of employer's managers](#list)
* [Getting information about a manager](#item)

You must be authorised as an employer to obtain information.
A response `403 Forbidden` will be returned if the user is unauthorised or incorrectly authorised.


<a name="dict"></a>
## Directory of manager types and privileges

> Attention! The values in the directories may change at any time. Do not address them directly.

### Request
`GET /employers/{employer_id}/manager_types`

where `employer_id` - employer id, you can find the employer's id in the [current user info](me.md#employer-info).

### Response

Successful response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "id": "manager",
            "name": "Manager",
            "available_permissions": [
                {
                    "id": "can_create_vacancy",
                    "name": "Creation and extension of vacancies"
                },
                {
                    "id": "can_view_resume_contacts",
                    "name": "View contacts of the applicant"
                }
            ]
        }
    ]
}
```

Each element of `items` has the following fields:

Name | Type | Description
--- | --- | ---
id | string | manager type ID
name | string | manager type name
available_permissions | array | list of privileges that can be granted to the selected manager type

Fields of the object from the list `available_permissions`:

Name | Type | Description
--- | --- | ---
id | string | privilege ID
name | string | privilege name

### Errors
* `404 Not found` - The employer was not found, or the user does not have the appropriate privileges


<a name="add"></a>
## Adding a manager

### Request

`POST /employers/{employer_id}/managers`

where `employer_id` - employer id, you can find the employer's id in the [current user info](me.md#employer-info).

JSON will be returned in the response:

```json
{
    "last_name": "Fedotov",
    "first_name": "Tim",
    "middle_name": "Illonovich",
    "manager_type": {
        "id": "manager"
    },
    "is_main_contact_person": false,
    "position": "Adaptation manager",
    "email": "employer@example.com",
    "area": {
        "id": "1"
    },
    "phone": {
        "country": "7",
        "city": "495",
        "number": "1568055",
        "comment": "с 9 до 17"
    },
    "additional_phone": {
         "country": "7",
         "city": "916",
         "number": "4555555",
         "comment": "personal"
    },
    "permissions": [
       {
           "id": "can_create_vacancy"
       },
       {
           "id": "can_view_resume_contacts"
       }
   ]
}
```

Name | Type | Description
--- | --- | ---
last_name | string | surname
first_name | string | name
middle_name | string or null | patronymic
manager_type.id | string | [manager type](#dict) ID
is_main_contact_person | boolean | is the manager the company's main contact person
position | string | manager's position
email | string | manager's email
area.id | number | region [from directory](areas.md)
phone | object | manager's phone number
additional_phone | object or null | manager's additional phone number
permissions | array | list of [manager's privileges](#dict)

Fields of objects `phone` and `additional_phone`:

Name | Type | Description
--- | --- | ---
country | string | country code
city | string | city code
number | string | phone number
comment | string or null | commentary

Fields of the object from the list `permissions`:

Name | Type | Description
--- | --- | ---
id | string | privilege ID
name | string | privilege name

All fields, except for phone comment and privileges, are mandatory

### Response

A successful response will return a status `201 Created`.
The ID of the created manager is sent as:

 * a response body similar to:
```
 {"id": "78789890"}
```

 * and also in the header `Location`:

```
 HTTP/1.1 201 Created

 Location: /employers/432/managers/78789890
```

### Errors

* `404 Not Found` – the employer you specified does not exist or the user does not have enough rights to add a manager
* `400 Bad Request` – parameters in the input JSON contain an error. The system will return the error description in the body.
                      Unknown parameters and parameters with errors in the names are ignored.
* `403 Forbidden`– incorrect authorisation or other reasons to cancel manager creation
                   In addition to the HTTP code, the server can return
                   a description of the [error reason](errors.md#employer_managers).


<a name="edit"></a>
## Editing a manager

### Request

`PUT /employers/{employer_id}/managers/{manager_id}`

where:

* `employer_id` - Employer ID that can be obtained from the [information on the current user](me.md#employer-info).
* `manager_id` - Manager ID.

The request body passes the following JSON:

```json
{
    "position": "Adaptation manager",
    "phone": {
        "country": "7",
        "city": "495",
        "number": "1568055",
        "comment": "с 9 до 17"
    },
    "additional_phone": {
         "country": "7",
         "city": "916",
         "number": "4555555",
         "comment": "personal"
    },
    "permissions": [
       {
           "id": "can_create_vacancy",
           "name": "Creation and extension of vacancies"
       },
       {
           "id": "can_view_resume_contacts",
           "name": "View contacts of the applicant"
       }
   ]
}
```

Can only be edited in the field from the JSON example given here. The description of fields can be found in the [creation request](#add).
During an update, you can resend all fields or only the fields that will be updated.

### Response

Successful response is returned with `200 OK`.

### Errors

* `404 Not Found` – the employer or manager you specified does not exist or the user does not have enough rights to edit a manager
* `400 Bad Request` – parameters in the input JSON contain an error. The system will return the error description in the body.
                      Unknown parameters and parameters with errors in the names are ignored.
* `403 Forbidden`– incorrect authorisation or other reasons to cancel manager editing
                   In addition to the HTTP code, the server can return
                   a description of the [error reason](errors.md#employer_managers).

<a name="delete"></a>
## Deleting a manager

Deleting a manager is not immediate and can take a while.
This is why if you request a list of managers **immediately** after successfully deleting a manager the response may include the deleted manager.

### Request

`DELETE /employers/{employer_id}/managers/{manager_id}`

where:

* `employer_id` - Employer ID that can be obtained from the [information on the current user](me.md#employer-info).
* `manager_id` - Manager ID.

As a mandatory parameter you must include: `successor_id` — ID of the manager who will receive all data related 
to the deleted manager, in particular: vacancies, applications, files with selected resumes, comments on candidates, automatic searches.

### Response

A successful response contains a code `204 No Content`.

### Errors

* `404 Not Found` – the employer or manager you specified does not exist or the user does not have enough rights to delete
                    this manager
* `400 Bad Request` – parameters in the input JSON contain an error. The system will return the error description in the body.
                      Unknown parameters and parameters with errors in the names are ignored.
* `403 Forbidden`– incorrect authorisation or other reasons to cancel manager deletion

<a name="list"></a>
## Directory of employer's managers

> Attention! The values in the directories may change at any time. Do not address them directly.

### Request

`GET /employers/{employer_id}/managers`

where:

* `employer_id` - Employer ID that can be obtained from the [information on the current user](me.md#employer-info).

request applies [standard pagination parameters](/docs_eng/general.md#pagination) page и per_page (per_page can't be more 200).
if `per_page` parameter is not received, it's default value equals 200

### Response

A successful response will return a status `200 OK`. The response body will contain a list
of employer's managers, for example:

```json
{
    "items": [
        {
            "id": "1507922",
            "email": "employer@example.com",
            "full_name": "Ivanov Ivan Ivanovich",
            "last_name": "Ivanov",
            "first_name": "Ivan",
            "middle_name": "Ivanovich",
            "vacancies_count": 0,
            "phone": {
                "country": "7",
                "city": "495",
                "number": "1568055",
                "comment": "from 9 to 17"
            },
            "additional_phone": {
                "country": "7",
                "city": "916",
                "number": "4555555",
                "comment": "personal"
            },
            "position": "HR manager",
            "area": {
                "id": "1",
                "name": "Moscow",
                "url": "https://api.hh.ru/areas/1"
            }
        }
    ],
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20
}
```
The response includes [standard pagination fields](general.md#pagination)

The `items` element will contain a list of the employer's managers.
Each element of `items` has fields described in
[adding a manager](#add), except for the fields `permission` and `manager_types`.

There are also the following fields:

<a name="fields"></a>

Name | Type | Description
--- | --- | ---
id | string | Manager ID
full_name | string | Manager's full name
vacancies_count | number | number of published (active) vacancies for this manager

### Errors
 * `403 Forbidden` - Current authorisation is not allowed to view this employer's managers

<a name="item"></a>
## Getting information about a manager

### Request

`GET /employers/{employer_id}/managers/{manager_id}`

where:

* `employer_id` - Employer ID that can be obtained from the [information on the current user](me.md#employer-info).
* `manager_id` - Manager ID.

### Response

A successful response will return a status `200 OK`.
The response body will contain manager info, for example:

```json
{
    "id": "1507922",
    "manager_type":{
        "id": "manager",
        "name": "Manager"
    },
    "email": "employer@example.com",
    "full_name": "Ivanov Ivan Ivanovich",
    "last_name": "Ivanov",
    "first_name": "Ivan",
    "middle_name": "Ivanovich",
    "vacancies_count": 0,
    "phone": {
        "country": "7",
        "city": "495",
        "number": "1568055",
        "comment": "с 9 до 17"
    },
    "additional_phone": {
        "country": "7",
        "city": "916",
        "number": "4555555",
        "comment": "personal"
    },
    "position": "HR Manager",
    "permissions": [
       {
           "id": "can_create_vacancy",
           "name": "Creation and extension of vacancies"
       },
       {
           "id": "can_view_resume_contacts",
           "name": "View contacts of the applicant"
       }
    ],
    "area": {
        "id": "1",
        "name": "Moscow",
        "url": "https://api.hh.ru/areas/1"
    }
}
```

Fields of the object are the same as the fields in the [directory of managers](#fields) and
there are also additional fields:

Name | Type | Description
--- | --- | --------
permissions | array | list of [manager's privileges](#dict)

### Errors

* `404 Not Found` - The employer or manager was not found, or the user does not have the appropriate privileges
