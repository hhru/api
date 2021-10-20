# Saved CV search

Saved search (autosearch) is the saved set of search parameters used
to track new CVs on this request.
In addition to saving search request parameters the autosearch function allows to
obtain notifications on new search results. For convenience, you can assign a name to
the autosearch.

* [List of saved CV searches](#resumes-saved-search-list)
* [Getting single saved CV search](#resumes-saved-search-item)
* [Creating new saved resumes search](#resumes-saved-search-create)
* [Updating saved resumes search](#resumes-saved-search-update)
* [Deleting saved resumes search](#resumes-saved-search-delete)
* [Moving saved resumes search to other manager](#resumes-saved-search-move-to-other-manager)

<a name="resumes-saved-search-list"></a>
##  List of saved CV searches

`GET /saved_searches/resumes`

Request is available only if authorized by an employer, otherwise error
`403 Forbidden` is returned.

You can additionally indicate
[standard pagination parameters](general.md#pagination) `page` and `per_page`.
By default `per_page` is `5`, max value is `10`.

Successful server response is returned with `200 OK` code and contains:

```json
{
  "per_page": 0,
  "page": 0,
  "pages": 1,
  "found": 2,
  "items": [
    {
      "id": "609535",
      "name": "Managers in Moscow",
      "created_at": "2015-01-01T13:12:17+0400",
      "subscription": true,
      "items": {
        "count": 55,
        "url": "https://api.hh.ru/resumes?order_by=publication_time&saved_search_id=123456&text=manager&area=1"
      },
      "new_items": {
        "count": 15,
        "url": "https://api.hh.ru/resumes?order_by=publication_time&saved_search_id=123456&text=manager&area=1&last_used=2015-11-12T18%3A06%3A04%2B0300"
      },
    }
  ]
}
```

<a name="resumes-saved-search-object"></a>
Each collection item contains following info:

name | type | comment
---------|-----|------------
id | string | ID
name | string | name
subscription | logical | subscription enabled/disabled
items | object | info on found CVs
new_items | object | Information on CVs found since the last autosearch view

Objects `items` and `new_items` contain following fields:

name | type | comment
---------|-----|------------
count | int | number of saved search results
url | string | reference to saved search results is available if access to CV search is enabled

<a name="resumes-saved-search-item"></a>
# Getting single saved CV search

`GET /saved_searches/resumes/{id}`

where `id` is the autosearch ID.

Request is available only if authorized by an employer, otherwise error
`403 Forbidden` is returned. If autosearch is not found or unavailable to current user,
error `404 Not Found` is returned.

Successful response is returned with `200 OK` code and contains single autosearch object
identical to [objects from CV autosearch list](#resumes-saved-search-object).


<a name="resumes-saved-search-create"></a>
## Creating new saved resumes search

In order to create autosearch you must send `POST` request to
`/saved_searches/resumes` with following parameters:

* resumes search parameters. Correspond to parameters
  sent to resumes search [/resumes](resumes_search.md#search-params)

If successful, response `201 Created` will be returned with title
`Location` indicating created autosearch (e.g.
`/saved_searches/resumes/123`, where 123 is ID of created autosearch).

Request is available only if authorized by an employer, otherwise error
`403 Forbidden` is returned. If parameters are indicated incorrectly or
there is an incorrect parameter set, `400 Bad request` will be returned.


<a name="resumes-saved-search-update"></a>
## Updating saved resumes search

You can change subscription name and status for saved search. To do this,
send `PUT /saved_searches/resumes/{id}`, where id is
saved search ID.

You can change only subscription name (parameter `name`) or status
(parameter `subscription=false`) at a time. If parameter is missing or invalid,
`400 Bad Request` is returned.

If you try to change both, response `409 Conflict` is returned.
If autosearch is not found, response `404 Not Found` will be returned.
Request is available only if authorized by an employer, otherwise error
`403 Forbidden` is returned.


<a name="resumes-saved-search-delete"></a>
## Deleting saved resumes search

In order to delete autosearch, send request
`DELETE /saved_searches/resumes/{id}`, where id is autosearch ID.

If autosearch is not found, status `404 Not Found` will be returned.

Request is available only if authorized by an employer, otherwise error
`403 Forbidden` is returned.

If autosearch is deleted successfully, status `204 No Content` will be returned.


<a name="resumes-saved-search-move-to-other-manager"></a>
## Moving saved resumes search to other manager

For moving saved resumes search to other manager, send
`PUT /saved_searches/resumes/{saved_search_id}/managers/{manager_id}`,
where saved_search_id is autosearch ID and manager_id - manager ID
([managers of this company](https://github.com/hhru/api/blob/master/docs_eng/employer_managers.md#list)).

If autosearch or manager is not found, status `404 Not Found` will be returned.
Response body can contain details about the [error reason](errors_additional.md#resumes-saved-searches)
(`saved_search_not_found` or `manager_not_found`).

Request is available only if authorized by an employer, otherwise error
`403 Forbidden` is returned.

If autosearch is moved successfully, status `204 No Content` will be returned.
