# Applicant comments

* [List of comments](#list)
* [Create comment](#add_comment)
* [Update comment](#edit_comment)
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
            "text": "pay attention to this candidate\nimmediately!"
        },
        {
            "author": {
                "full_name": "Ivanova Maria Ivanovna"
            },
            "created_at": "2015-08-27T10:30:14+0300",
            "id": "123654",
            "is_mine": false,
            "text": "do not consider necessary"
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

### Errors

* `404 Not Found` – the specified applicant was not found.
* `403 Forbidden` – receiving comments is not available for the current user.


<a name="add_comment"></a>
## Create comment

Documentation translation for this article is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/applicant_comments.md.html#add_comment) powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="edit_comment"></a>
## Update comment

Documentation translation for this article is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/applicant_comments.md.html#edit_comment) powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="delete_comment"></a>
## Delete comment

Documentation translation for this article is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/applicant_comments.md.html#delete_comment) powered by
[Yandex.Translate](https://translate.yandex.com/translate).

