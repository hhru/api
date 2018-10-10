# Information on the authorised user or application

* [Obtaining information on the authorised user](#user-info)
* [Editing information on the authorised user](#user-edit)
* [Obtaining information on the authorised application](#application-info)

<a name="general"></a>
Note that responses depend on the type of token transferred. If it is an application token, the response will only contain some flags.

<a name="user-info"></a>
## Obtaining information on the authorised user

### Request

`GET /me` returns info on current authorized user.
Server returns `403 Forbidden` if authorization is failed.

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "id": "12345678",
    "last_name": "Last name",
    "first_name": "Name",
    "middle_name": "Middle name",
    "is_admin": false,
    "is_applicant": false,
    "is_employer": true,
    "is_application": false,
    "email": "contact@example.com",
    "phone": "79164555555",
    "employer": {
        "manager_id": "4062820",
        "id": "1455",
        "name": "HeadHunter"
    },
    "manager": {
        "id": "87654321",
        "has_admin_rights": true,
        "is_main_contact_person": true,
        "manager_settings_url": "https://api.hh.ru/employers/1455/managers/87654321/settings"
    },
    "personal_manager": {
        "id": "1234567",
        "first_name": "Ivan",
        "last_name": "Ivanov",
        "email": "ivanov@example.com",
        "photo_urls": {
            "big": "https://hhcdn.ru/file/big.jpg",
            "small": "https://hhcdn.ru/file/small.jpg"
        },
        "is_available": false,
        "unavailable": {
            "until": "2016-07-01T08:00:00+0400"
        }
    },
    "counters": {
        "unread_negotiations": 0,
        "new_resume_views": 2,
        "resumes_count": 5
    },
    "is_in_search": true,
    "resumes_url": "https://api.hh.ru/resumes/mine",
    "negotiations_url": "https://api.hh.ru/negotiations"
}
```


 Name | Type | Description
 --- | --- | ---
 id | string | user ID
 last_name | string | last name
 first_name | string | name
 middle_name | string, null | middle name or null if no middle name
 is_admin | logical | user is site administrator
 is_applicant | logical | true, if the user is an applicant
 is_employer | logical | true, if the user is an employer
 is_application | logical | true if an application is authorised
 email | string, null | email
 phone | string, null | phone number. It is only displayed for applicants if a phone number is specified
 employer | object, null | [company information](#employer-info) if the current user is an employer, or null in all other cases
 personal_manager | object, null | [information on the personal manager](#personal-manager-info) if the current user is an employer, or null in other cases 
 manager | object, null | [information on the user as a company manager](#manager-info) if the current user is an employer, or null in all other cases 
 is_in_search | logical, null | flag "looking for a job yes/no" if the current user is an applicant
 resumes_url | string | reference to current user CV list api-service
 negotiations_url | string | reference to current user responses/invitations list api-service
 counters | object, unavailable | [information on the counters](#counters-info) if the current user is an applicant 


<a name="employer-info"></a>
#### Object `employer`

Name | Type | Description
--- | --- | ------
 id | string | company ID
 manager_id | string | personal manager ID
 name | string | company name


<a name="manager-info"></a>
#### Object `manager`

Name | Type | Description
--- | --- | ------
id | string | manager ID
has_admin_rights | logical | does the current manager have administrative privileges
is_main_contact_person | logical | is the current manager the company's main contact person
manager_settings_url | string | The URL to perform a GET request to obtain the [manager preferences](manager_settings.md)


<a name="personal-manager-info"></a>
#### Object `personal_manager`

Information on the personal manager for the employer.

Name | Type | Description
--- | --- | ---
 id | string | personal manager ID
 email | string | email of the personal manager
 first_name | string | manager first name
 last_name | string | manager last name
 photo_urls | object, null | manager's photos or `null`
 photo_urls.big | string, null | URL of a large photo of the manager or `null`
 photo_urls.small | string, null | URL of a small photo of the manager or `null`
 is_available | logical | if the manager is currently available
 unavailable | object, null | information on the absence of the manager or `null` if the manager is available
 unavailable.until | string (date) | time until which the manager is unavailable


<a name="counters-info"></a>
#### Object `counters`

All key values are numbers.

Name | Description
--- | ---
unread_negotiations | number of new unread conversations (with `has_updates: true`)
new_resume_views | total number of new views of all resumes of the current user
resumes_count | total number of created resumes of the current user

### Errors

* `403 Forbidden` – user authorisation failed.

<a name="user-edit"></a>
## Editing information on the authorised user

To edit the surname, name or patronymic, or to change the value for the 'looking / not looking for a job' flag, a POST request must be sent to `/me`.
This method is only available to applicants. Data can only be edited in groups:

### Full name

 Name | Type | Description
 --- | --- | ---
 last_name | string | last name, the field can't be empty
 first_name | string | name, field can't be empty
 middle_name | string | middle name, field can be empty

All the group fields must be sent in the request, e.g.:

```
    POST /me
    last_name=Ivanov&first_name=Ivan&middle_name=
```

If not all fields are sent, `400 Bad Request` is returned.


### "looking for a job yes/no" flag

 Name | Type | Description
 --- | --- | ---
 is_in_search | string | true/false

Example:

```
 POST /me
 is_in_search=true
```

If the user is not an applicant, a response will be returned `403 Forbidden`.
If the request contains parameters from different groups, an error is generated `400 Bad Request`.

<a name="application-info"></a>
## Obtaining information on the authorised application

`GET / me` will return a response with a body similar to [getting information on the current user](#user-info), but it will only contain flags.

 ```json
{
    "is_admin": false,
    "is_applicant": false,
    "is_employer": false,
    "is_application": true
}
```

### Errors

 * `403 Forbidden` – application authorisation failed.