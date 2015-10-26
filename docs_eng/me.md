# Current user

* [Obtaining information on the current user](#info)
* [Editing information on the current user](#edit)


<a name="info" />
## Obtaining information on the current user

`GET /me` will return information on the current authorized user. In case of
incorrect authorization, the server will return the `403 Forbidden` response.

```json
{
    "id": "12345678",
    "last_name": "Last name",
    "first_name": "First name",
    "middle_name": "Middle name",
    "is_admin": false,
    "is_applicant": false,
    "is_employer": true,
    "email": "contact@example.com",
    "employer": {
        "id": "1455",
        "name": "HeadHunter",
        "manager_id": "87654321"
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


| Name              | Type          | Description |
|-------------------|---------------|--------------|
| id                | string        | user identifier |
| last_name         | string        | last name |
| first_name        | string        | first name |
| middle_name       | string        | middle name |
| is_admin          | logical       | whether the user is the website administrator |
| is_applicant      | logical       | true, if the user is an applicant |
| is_employer       | logical       | true, if the user is an employer |
| email             | string        | email |
| employer          | object, null  | information on the company, if the current user is an employer |
| personal_manager  | object, null  | information on the personal manger, if the current user is an employer |
| is_in_search      | logical, null | checkbox "looking/not looking for a job", if the current user is an applicant |
| resumes_url       | string        | link to the api-service of the current user's resume list |
| negotiations_url  | string        | link to the api-service of the current user's application/invitation list |
| counters          | no object     | information on counters, if the current user is an applicant |


#### Object `employer`

| Name        | Type   | Description |
|-------------|--------|-------------|
| id          | string | company identifier |
| name        | string | company name |
| manager_id  | string | identifier of the current user as the company manager |


#### Object `personal_manager`

| Name  | Type   | Description |
|-------|--------|-------------------------------|
| id    | string | Personal manager's identifier |
| email | string | Personal manager's email |


#### Object `counters`

All key values are numbers.

| Name                 | Description |
|----------------------|-------------|
| unread_negotiations | The number of new unread messages (which have `has_updates: true`) |
| new_resume_views    | General number of new views of all the resumes of the current user |


<a name="edit" />
## Editing information on the current user

To edit the last name, first name or middle name, and also to check or uncheck
the check box "looking/not looking for a job", you should send a POST request to
`/me`. Data can be edited only in groups:


### Full name

| Name         | Type   | Description                           |
|--------------|--------|---------------------------------------|
| last_name    | string | last name, the field can't be empty   |
| first_name   | string | first name, the field can't be empty  |
| middle_name  | string | middle name, the field can't be empty |

All the group fields must be sent in the request, for example:

```
POST /me
last_name=Ivanov&first_name=Ivan&middle_name=
```

If not all the fields are indicated in the request, then the `400 Bad Request`
response will be returned.


### Checkbox "looking/not looking for a job"

| Name           | Type   | Description |
|----------------|--------|-------------|
| is_in_search   | string | true/false  |

Example:

```
POST /me
is_in_search=true
```

A request with parameters from different groups will have the `400 Bad Request`
response returned.
