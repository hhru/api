# Saved search

Saved search (autosearch) is the saved set of search parameters used
to track new vacancies or CVs on this request.
In addition to saving search request parameters the autosearch function allows to
obtain notifications on new search results. For convenience, you can assign a name to
the autosearch.

* Saved vacancy search
  * [List of saved vacancy searches](#vacancies-saved-search-list)
  * [Obtaining single saved vacancy search](#vacancies-saved-search-item)
  * [Creating new saved vacancy search](#vacancies-saved-search-create)
  * [Updating saved vacancy search](#vacancies-saved-search-update)
  * [Deleting saved vacancy search](#vacancies-saved-search-delete)
* Saved CV search
  * [List of saved CV searches](#resumes-saved-search-list)
  * [Getting single saved CV search](#resumes-saved-search-item)
  * [Creating new saved resumes search](#resumes-saved-search-create)
  * [Updating saved resumes search](#resumes-saved-search-update)
  * [Deleting saved resumes search](#resumes-saved-search-delete)


<a name="vacancies-saved-search-list"></a>
## List of saved vacancy searches

`GET /saved_searches/vacancies` returns paginated autosearch list.

Request is available only if authorized by an applicant, otherwise error
`403 Forbidden` is returned.

Accepted parameters:

* `page` – page number (counted from 0, by default 0)
* `per_page` – number of items (by default 10,
  max value 10)


The response will contain standard collection of paginated items.


```json
{
  "per_page": 1,
  "page": 0,
  "found": 1,
  "pages": 1,
  "items": [
    {
      "id": "123",
      "name": "Test autosearch",
      "created_at": "2014-04-11T13:12:17+0400",
      "subscription": true,
      "items": {
        "count": 304234,
        "url": "https://api.hh.ru/vacancies?area=1&saved_search_id=123"
      },
      "new_items": {
        "count": 12,
        "url": "https://api.hh.ru/vacancies?area=1&saved_search_id=123&date_from=2014-01-11T13%3A12%3A17%2B0400"
      }
    }
  ]
}
```

Each item contains following info:

 Name | Type | Description
---- | --- | ---
 id  | string | ID
 name | string | Name
 created_at | string | Creation date and time
 subscription | logical | Subscription status
 items | object | Vacancy list data
 new_items | object | Information on list of vacancies appeared since the last vacancy view

Vacancy list info contains number of items in search (`count`) and
reference to such items. Upon requesting `new_items` reference
new vacancy count will be reset (value may be reset after short
delay).


<a name="vacancies-saved-search-item"></a>
## Obtaining single saved vacancy search

In order to get autosearch by ID you must send
`GET /saved_searches/vacancies/{id}`.

Request is available only if authorized by an applicant, otherwise error
`403 Forbidden` is returned.

If successful, status`200 OK` containing single autosearch object in body
will be returned. For example:

```json
{
  "id": "123",
  "name": "Test autosearch",
  "created_at": "2014-04-11T13:12:17+0400",
  "subscription": true,
  "items": {
    "count": 304234,
    "url": "https://api.hh.ru/vacancies?area=1&saved_search_id=123"
  },
  "new_items": {
    "count": 12,
    "url": "https://api.hh.ru/vacancies?area=1&saved_search_id=123&date_from=2014-01-11T13%3A12%3A17%2B0400"
  }
}
```

If autosearch is not found, status `404 Not Found` will be returned.


<a name="vacancies-saved-search-create"></a>
## Creating new saved vacancy search

In order to create autosearch you must send `POST` request to
`/saved_searches/vacancies` with following parameters:

* vacancy search parameters. Correspond to parameters
  sent to vacancy search [/vacancies](vacancies.md#search)

If successful, response `201 Created` will be returned with title
`Location` indicating created autosearch (e.g.
`/saved_searches/vacancies/123`, where 123 is ID of created autosearch).

Request is available only if authorized by an applicant, otherwise error
`403 Forbidden` is returned. If parameters are indicated incorrectly or 
there is an incorrect parameter set, `400 Bad request` will be returned.


<a name="vacancies-saved-search-update"></a>
## Updating saved vacancy search

You can change subscription name and status for saved search. To do this,
send `PUT /saved_searches/vacancies/{id}`, where id is
saved search ID.

You can change only subscription name (parameter `name`) or status
(parameter `subscription=false`) at a time.

If you try to change both, response `409 Conflict` is returned.
If autosearch is not found, response `404 Not Found` will be returned.
Request is available only if authorized by an applicant, otherwise error
`403 Forbidden` is returned.


<a name="vacancies-saved-search-delete"></a>
## Deleting saved vacancy search

In order to delete autosearch, send request
`DELETE /saved_searches/vacancies/{id}`, where id is autosearch ID.

If autosearch is not found, status `404 Not Found` will be returned.

Request is available only if authorized by an applicant, otherwise error
`403 Forbidden` is returned.

If autosearch is deleted successfully, status `204 No Content` will be returned.


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
        "url": "https://api.hh.ru/resumes?order_by=publication_time&saved_search_id=123456&text=manager&area=1&date_from=2015-11-12T18%3A06%3A04%2B0300"
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

Note that in order to get autosearch results (CV list)
the application used to authorize the employer should
[pass the procedure on granting access to CV](employer_resumes.md#resume-search-request).


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
  sent to resumes search [/resumes](employer_resumes.md#request-and-acceptable-parameters)

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
(parameter `subscription=false`) at a time.

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
