# Applicant comments

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](employer_payable_methods.md)

* [List of comments](#list)
* [Adding a comment](#add_comment)
* [Comment update](#edit_comment)
* [Delete comment](#delete_comment)

<a name="list"></a>
## List of comments

Receiving the list of comments is available only for an employer. The list will
contain comments of the current user as well as comments of other company
managers provided that the managers made these comments accessible to others at
the moment of posting.


### Request

No need to construct the request url on your own – it should be received from
the [owner CV field](resumes.md#owner-field)

`GET /applicant_comments/{applicant_id}`

where `applicant_id` is the applicant ID.

Additional request parameters:

* [`page` and `per_page` pagination parameters](general.md#pagination)
* `order_by` – comments sorting, available values are provided in the
  [`applicant_comments_order` reference](dictionaries.md)


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
            "author": {
                "full_name": "Ivanov Ivan Ivanovich"
            },
            "created_at": "2015-08-27T10:19:55+0300",
            "id": "123456",
            "is_mine": true,
            "text": "look at this candidate\nnow!",
            "access_type": {
                "id": "coworkers",
                "name": "Visible to me and my colleagues",
            }
        },
        {
            "author": {
                "full_name": "Ivanova Maria Ivanovna"
            },
            "created_at": "2015-08-27T10:30:14+0300",
            "id": "123654",
            "is_mine": false,
            "text": "do not consider necessary",
            "access_type": {
                "id": "owner",
                "name": "Visible only to me",
            }
        }
    ]
}
```

key| type| description
-----|-----|---------
author.full_name| string| comment author full name
created_at| string, date| comment creation date
id| string| comment unique ID
is_mine| logical| was the comment written by the current user?
text| string| comment content, text that can contain newline characters
access_type | object | access types for comments, possible values are stored in the [directory](dictionaries.md#etc)

### Errors

* `404 Not Found` – the specified applicant was not found.
* `403 Forbidden` – receiving comments is not available for the current user.


<a name="add_comment"></a>
## Adding a comment

### Request

You do not need to construct the request URL manually, you can get it from
[the `owner` field in the resume](resumes.md#owner-field)

`POST /applicant_comments/{applicant_id}`

where

* `applicant_id` – applicant ID

Request parameters:

* `text` - comment text,
* `access_type` - access type (possible values are stored in the [applicant_comment_access_type directory](dictionaries.md#etc))


### Response

Successful response is returned with `201 Created` code and contains added comment:


```json
{
    "author": {
        "full_name": "Ivanova Maria Ivanovna"
    },
    "created_at": "2015-08-27T10:30:14+0300",
    "id": "123654",
    "is_mine": true,
    "text": "do not consider necessary",
    "access_type": {
        "id": "owner",
        "name": "Visible only to me",
    }
}
```


### Errors

* `403 Forbidden` – if the current user is not an employer.
* `404 Not Found` – the specified applicant does not exist.
* `400 Bad argument` – error in the request parameters.


<a name="edit_comment"></a>
## Comment update

You can change the access type and text of an existing comment.
Only the author can change the comment.

### Request

To get the URL, add a comment ID to the URL of the [list of comments](#list).

`PUT /applicant_comments/{applicant_id}/{comment_id}`

where

* `applicant_id` – applicant ID,
* `comment_id` – comment ID.

Request parameters:

* `text` - comment text,
* `access_type` - access type (possible values are stored in the [applicant_comment_access_type directory](dictionaries.md#etc))

The comment text and access type can be changed. If the parameter is not passed,
then the value will remain the same.


### Response

A successful response contains a code `204 No Content` and is body-less.


### Errors

* `403 Forbidden` – if the current user is not an employer.
* `404 Not Found` – if the specified applicant or comment does not exist.
* `400 Bad argument` – error in the request parameters; in addition, the names of parameter with errors may be specified.


<a name="delete_comment"></a>
## Delete comment

Only the author can delete the comment.

### Request

To get the URL, add a comment ID to the URL of the [list of comments](#list).

`DELETE /applicant_comments/{applicant_id}/{comment_id}`

where
* `applicant_id` – applicant ID,
* `comment_id` - comment ID

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – if the current user is not an employer
* `404 Not Found` – if the specified applicant or comment does not exist.