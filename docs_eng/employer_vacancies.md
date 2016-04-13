# Vacancies for the employer

* [Published vacancy list](#active)
* [Storing vacancies](#archive)
* [Archived vacancy list](#archived)
* [Deleting vacancies](#hide)
* [Deleted vacancy list](#hidden)
* [Restoring deleted vacancies](#restore)

See also:

* [Vacancy posting](vacancies.md#creation)
* [Vacancy editing](vacancies.md#edit)
* [Vacancy extension](vacancies.md#prolongate)


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
          "90": "http://hh.ru/employer-logo/289027.png",
          "240": "http://hh.ru/employer-logo/289169.png",
          "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "http://hh.ru/employer/1455",
        "id": "1455"
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "http://hh.ru/vacancy/8331228",
      "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=8331228",
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
        "invitations": 10
      },
      "expires_at": "2013-07-08T16:17:21+0400",
      "has_updates": false
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
| counters.invitations       | number  | number of invitations for a vacancy                                                             |
| expires_at                 | string  | expiration date for a vacancy posting                                                           |
| has_updates                | boolean | Whether there are updates calling for attention in the applications/invitations for the vacancy |


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
          "90": "http://hh.ru/employer-logo/289027.png",
          "240": "http://hh.ru/employer-logo/289169.png",
          "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "http://hh.ru/employer/1455",
        "id": "1455"
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "http://hh.ru/vacancy/8331228",
      "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=8331228",
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


<a name="hide"></a>
## Deleting vacancies

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can delete only an archived vacancy.
If performed successfully, `204 No Content` will be returned.


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
          "90": "http://hh.ru/employer-logo/289027.png",
          "240": "http://hh.ru/employer-logo/289169.png",
          "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "http://hh.ru/employer/1455",
        "id": "1455"
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "http://hh.ru/vacancy/8331228",
      "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=8331228",
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


<a name="restore"></a>
## Restoring deleted vacancies

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can restore only a vacancy deleted from the archive.
If performed successfully, `204 No Content` will be returned.
The vacancy will be returned to the archive.
