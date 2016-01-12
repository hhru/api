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


<a name="active"/>
## Published vacancy list

`GET /employers/{employer_id}/vacancies/active?manager_id={manager_id}`

To view the list of published vacancies, you should indicate the manager ID even
if you need to make a request for the current manager (the value can be taken
from `/me`).

In addition to [the standard vacancy fields](vacancies.md#nano), additional
fields will be returned:

```json
{
    "counters": {
        "views": 100500,
        "responses": 5,
        "unread_responses": 3,
        "invitations": 10
    },
    "expires_at": "2013-07-08T16:17:21+0400",
    "has_updates": false
}
```

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


<a name="archive"/>
## Storing vacancies

To archive a vacancy, you should send a PUT request:

`PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}`

If archived successfully, `204 No Content` will be returned.


<a name="archived"/>
## Archived vacancy list

`GET /employers/{employer_id}/vacancies/archived?manager_id={manager_id}`

To view the list of archived vacancies, you also need to indicated manager id,
even if you need to make request for the current manager (the value can be taken
from `/me`). Pagination (`per_page` and `page`) and sorting (`order_by`) are
supported. Possible sorting values are available in the
`employer_archived_vacancies_order` (`/dictionaries`) directory. As opposed to
the list of published vacancies, this collection does not support search (the
parameters `text` and `area`).

In addition to [the standard vacancy fields](vacancies.md#nano), additional
fields will be returned:

```json
    {
      "counters": {
        "responses": 0
      },
      "archived_at": "2013-07-08T16:17:21+0400"
    }
```

| key                | type   | description                          |
|--------------------|--------|--------------------------------------|
| counters.responses | number | number of applications for a vacancy |
| archived_at        | string | vacancy archivation date             |


<a name="hide"/>
## Deleting vacancies

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can delete only an archived vacancy.
If performed successfully, `204 No Content` will be returned.


<a name="hidden"/>
## Deleted vacancy list

`GET /employers/{employer_id}/vacancies/hidden?manager_id={manager_id}`

Pagination (`per_page` and `page`) and sorting (`order_by`) are supported.
Possible sorting values are available in the `employer_hidden_vacancies_order`
(`/dictionaries`) directory. As opposed to the list of published vacancies, this
collection does not support search (the parameters `text` and `area`).


<a name="restore"/>
## Restoring deleted vacancies

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

You can restore only a vacancy deleted from the archive.
If performed successfully, `204 No Content` will be returned.
The vacancy will be returned to the archive.
