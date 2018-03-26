# Current user

* [Obtaining info on the current user](#info)
* [Editing info on the current user](#edit)


<a name="info"></a>
## Obtaining info on the current user

`GET /me` returns info on current authorized user.

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
    "email": "contact@example.com",
    "employer": {
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
        "new_resume_views": 2
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
 middle_name | string | middle name
 is_admin | logical | user is site administrator
 is_applicant | logical | true, if the user is an applicant
 is_employer | logical | true, if the user is an employer
 email | string, null | email
 employer | object, null | [company info](#employer-info) if the current user is an employer, or null in other cases
 personal_manager | object, null | [personal manager info](#personal-manager-info) if the current user is an employer, or null in other cases
 manager | object, null | [info on a user who is company manager](#manager-info) if the current user is an employer, or null in other cases
 is_in_search | logical, null | flag "looking for a job yes/no" if the current user is an applicant
 resumes_url | string | reference to current user CV list api-service
 negotiations_url | string | reference to current user responses/invitations list api-service
 counters | object, unavailable | [count info](#counters-info) if the current user is an applicant


<a name="employer-info"></a>
#### Object `employer`

Name | Type | Description
--- | --- | ------
 id | string | company ID
 name | string | company name


<a name="manager-info"></a>
#### Object `manager`

Name | Type | Description
--- | --- | ------
id | string | manager ID
has_admin_rights | logical | current manager has administrator rights
is_main_contact_person | logical | current manager is main contact person of the company
manager_settings_url | string | url to send GET request to get [manager preferences](manager_settings.md)


<a name="personal-manager-info"></a>
#### Object `personal_manager`

Name | Type | Description
--- | --- | ---
 id | string | Personal manager ID
 email | string | Personal manager's email


<a name="counters-info"></a>
#### Object `counters`

All key values are numbers.

Name | Description
--- | ---
unread_negotiations | Number of unread negotiations (indicating `has_updates: true`)
new_resume_views | Total number of new views of all CVs of the current user

### Errors

* `403 Forbidden` – authorization is failed.

<a name="edit"></a>
## Editing info on the current user

Send POST request to `/me` in order to edit the last name, name, middle name or
enable/disable "looking for a job yes/no"  flag. Data can be edited only in
groups:

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

### Errors

* `400 Bad Request` – request contains parameters from different groups.
* `403 Forbidden` – authorization is failed. Applicant is expected.
