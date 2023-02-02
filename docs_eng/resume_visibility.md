# Managing resume visibility lists

* [General information](#intro)
* [Getting visibility lists](#get)
* [Adding companies to the visibility list](#add)
* [Removing companies from the visibility list](#remove)
* [Clearing the visibility list](#clear)
* [Searching for employers to add to the visibility list](#search)


<a name="intro"></a>
## General Information

Resume visibility type is determined by the value of its [key `access.type`](resumes.md#access_type).
Some types of visibility, such as `whitelist` and `blacklist`, imply the use of a list of employers 
who can or can't see the resume.

The visibility list contains employer IDs (see the [company search](https://api.hh.ru/openapi/en/redoc#tag/Employer/operation/search-employer) and [getting information about a company](https://api.hh.ru/openapi/en/redoc#tag/Employer/operation/get-employer-info)).

Visibility lists are set up separately for each resume.
You can get [a list of all available visibility types](resumes.md#get_access_types) for a particular resume.

<a name="get"></a>
## Getting visibility lists

```
GET /resumes/{resume_id}/{list_type}
```

where:
* `resume_id` — resume ID
* `list_type` — list type (`whitelist` or `blacklist`)

[Standard pagination parameters](general.md#pagination) `page` and `per_page` are supported (`per_page` must not exceed 100).

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "limit": 2000,
    "items": [
        {
            "id": "1455",
            "name": "HeadHunter",
            "url": "https://api.hh.ru/employers/1455",
            "alternate_url": "https://hh.ru/employer/1455",
            "logo_urls": {
                "90": "https://hh.ru/employer/logo/1455"
            }
        }
    ]
}
```

The response includes [standard pagination fields](general.md#pagination) and:

Name | Type | Description
----|-----|---------
limit | number | The maximum number of items in the list.
items | array | Company list.
items[].id | string | Employer ID.
items[].name | string | Employer name.
items[].url | string | Link to detailed employer description.
items[].alternate_url | string | Link to employer description on the website.
items[].logo_urls.90 | string | Image of the employer's logo. The client should take into account the probable resource unavailability after following the specified link.

### Errors

* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.
* `404 Not Found` — An unknown `list_type` was passed.
* [Additional errors and cause descriptions](errors.md#resume-visibility-lists-get).


<a name="add"></a>
## Adding companies to the visibility list

```
POST /resumes/{resume_id}/{list_type}
```

where:
* `resume_id` — resume ID
* `list_type` — list type (`whitelist` or `blacklist`)

Pass the following JSON in the request body:

```json
{
    "items": [
        {
            "id": "407"
        },
        {
            "id": "412"
        },
    ]
}
```

Name | Type | Description
----|-----|---------
items | array | List of companies to be added
items[].id | string | Employer ID

Any other fields in the elements of the `items` array are ignored.

One request can add no more than 100 companies.

The procedure for adding to the list is idempotent, that is, employers who are already present in the list
will be ignored to avoid duplicate entries.

You can add a banned employer to the list.


### Response

If the add operation is successful, the system will return a body-less response `204 No Content` 
with the `Location` header which points to a [visibility list](#get):

```
Location: /resumes/{resume_id}/{list_type}
```


### Errors

* `400 Bad Request` — Invalid JSON or JSON with a wrong format was passed.
* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.
* `404 Not Found` — An unknown `list_type` was passed.
* [Additional errors and cause descriptions](errors.md#resume-visibility-lists-add).

If any error occurs, no company is added to the list (regardless of the error type).

If an empty list of companies is passed, then a successful response is returned.


<a name="remove"></a>
## Removing companies from the visibility list

```
DELETE /resumes/{resume_id}/{list_type}/employer?id={employer_id}
```

where:
* `resume_id` — resume ID
* `list_type` — list type (`whitelist` or `blacklist`)
* `id` — employer ID (multiple parameter)

An example of removing multiple employers:

```
DELETE /resumes/{resume_id}/{list_type}/employer?id=405&id=406&id=407
```

The operation to remove from the list is idempotent, that is, the removal of employers who are not on the list or do not exist
is ignored and does not lead to errors. The result will be the same if you remove the "real" `id` identifiers from the list.

You can remove a banned employer from the list.

One request can remove no more than 100 companies.

If the `id` parameter is missing, the system returns a successful response.


### Response

A successful response contains a code `204 No Content` and is body-less.


### Errors

* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.
* `404 Not Found` — An unknown `list_type` was passed.
* [Additional errors and cause descriptions](errors.md#resume-visibility-lists-remove).


<a name="clear"></a>
## Clearing the visibility list

```
DELETE /resumes/{resume_id}/{list_type}
```

where:
* `resume_id` — resume ID
* `list_type` — list type (`whitelist` or `blacklist`)


### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.
* `404 Not Found` — An unknown `list_type` was passed.


<a name="search"></a>
## Searching for employers to add to the visibility list

```
GET /resumes/{resume_id}/{list_type}/search?text={text}
```

where:
* `resume_id` — resume ID
* `list_type` — list type (`whitelist` or `blacklist`)
* `text` - Search string. The passed value is searched at the beginning of the employer name and at the beginning of the employer department names.

The response includes [standard pagination fields](general.md#pagination) (the maximum value of `per_page` is 100).

The system will return the results of the search for employers. An employer that is already present in the visibility list will be marked as `selected`: true.

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "found": 2,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "id": "1455",
            "name": "HeadHunter",
            "url": "https://api.hh.ru/employers/1455",
            "alternate_url": "https://hh.ru/employer/1455",
            "logo_urls": {
                "90": "https://hh.ru/employer/logo/1455"
            },
            "selected": true
        },
        {
            "id": "87891",
            "name": "HeadHunter: Kazakhstan",
            "url": "https://api.hh.ru/employers/87891",
            "alternate_url": "https://hh.ru/employer/87891",
            "logo_urls": {
                "90": "https://hh.ru/employer/logo/87891"
            },
            "selected": false
        }
    ]
}
```

The response includes [standard pagination fields](general.md#pagination) and:

Имя | Тип | Описание
----|-----|---------
items | array | Company list.
items[].id | string | Employer ID.
items[].name | string | Employer name.
items[].url | string | Link to detailed employer description.
items[].alternate_url | string | Link to employer description on the website.
items[].logo_urls.90 | string | Image of the employer's logo. The client should take into account the probable resource unavailability after following the specified link.
items[].selected | boolean | Whether the employer is in the resume visibility list.

### Errors

* `400 Bad Request` — Incorrect values were passed in the parameters. In this case, the body of the response will contain information on the erroneous parameter.
* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.
* `404 Not Found` — An unknown `list_type` was passed.
