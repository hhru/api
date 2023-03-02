# Receiving vacancies

* [View a vacancy](#item)
* [Additional vacancy fields for employers](#author)
* [Favorite vacancies](#favorited)
* [Search for vacancies](#search)
* [Search for vacancies similar to the vacancy](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/operation/get-vacancies-similar-to-vacancy)
* [Short description of the vacancy](#nano)
* [Hidden vacancies](https://api.hh.ru/openapi/en/redoc#tag/Hidden-vacancies)

See also:

<a name="creation"></a>
<a name="creation-example"></a>
<a name="creation_fields"></a>
<a name="allow_messages"></a>
<a name="creation-results"></a>
<a name="conditions"></a>
<a name="edit"></a>
<a name="edit_more"></a>
<a name="other-actions"></a>
<a name="prolongate"></a>
<a name="prolongate-info"></a>
<a name="branded-template-field"></a>

* [Vacancies for the employer](employer_vacancies.md)
  * [Vacancy posting](employer_vacancies.md#creation)
  * [Vacancy editing](employer_vacancies.md#edit)
  * [Vacancy prolongation](employer_vacancies.md#prolongate)
  * [Deleting vacancies](employer_vacancies.md#hide)


<a name="item"></a>
## View a vacancy

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancies/operation/get-vacancy)

<a name="author"></a>
#### Additional vacancy fields for employers

If the vacancy is requested when the author (employer) is authorised, the object
will show additional fields:

```json
{
  "expires_at": "2015-01-09T17:03:35+0300",
  "archived_at": "2015-01-08T16:17:21+0400",
  "response_notifications": false,
  "manager": {
    "id": "1337"
  },
  "hidden": false,
  "branded_template": {
    "id": "marketing",
    "name": "Marketing"
  },
  "can_upgrade_billing_type": true
}
```

key | type | description
---- | --- | --------
expires_at| string | date and time of vacancy posting termination
archived_at | string or null | date and time of archiving vacancy
response_notifications | logical | whether to notify manager on new responses
hidden | logical | whether the vacancy is deleted (hidden from the archive)
can_upgrade_billing_type | logical | If the vacancy billing type can be upgraded

In object `manager` – the information on the manager posted the vacancy.

In object `branded_template` – info on
[branded template](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-vacancy-branded-templates-list) used in vacancy.

In object `test` key `id` is available for the initiator, in object
`address` following objects are available:

```json
{
  "address": {
    "id": "1448",
    "show_metro_only": false
  }
}
```

More information on these fields see in section
[vacancy posting](#creation_fields).

For request with authorization of a manager having access to responses on a vacancy,
optional field with different counters on vacancy will be displayed in the object:

```json
{
  "counters": {
    "views": 100500,
    "responses": 5,
    "unread_responses": 3,
    "resumes_in_progress": 5,
    "invitations": 10,
    "invitations_and_responses": 14,
    "calls": 8,
    "new_missed_calls": 5
  }
}
```

key | type | description
---- | --- | --------
counters.views | number | number of vacancy views
counters.responses | number | number of responses to the vacancy
counters.unread_responses | number | number of non-viewed responses to the vacancy
counters.resumes_in_progress| number | number of resumes in progress for a vacancy
counters.invitations | number | number of invitations to the vacancy
counters.invitations_and_responses | number | number of invitations and responses to a vacancy
counters.calls | number | number of calls
counters.new_missed | number | number of new missed calls

### Errors

* `404 Not Found` - if the vacancy is not found, or the user does not have the appropriate privileges to view this vacancy


<a name="favorited"></a>
## Selected vacancies

These methods require applicant authorization, otherwise `403 Forbidden` will be
returned.

## Receiving favorite vacancies
> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Favorited-vacancies/operation/get-favorite-vacancies)

## Adding favorite vacancies
> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Favorited-vacancies/operation/add-vacancy-to-favorite)

## Deleting favorite vacancies
> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Favorited-vacancies/operation/delete-vacancy-from-favorite)

<a name="search"></a>
## Search for vacancies

### Request

`GET /vacancies` will return the results of vacancy search.

<a name="search-params"></a>
Acceptable parameters:

> Attention! Unknown parameters and parameters with an error in the name are ignored.

Some parameters take multiple values: `key=value&key=value`.

* `text` – text field.  
  The sent value is searched in the vacancy fields specified in the `search_field` parameter.  
  As with the main website, a query language is available: [https://hh.ru/article/1175](https://hh.ru/article/1175).
  There is [autoaddition](suggests.md#vacancy-search-keyword) especially for this field.

* `search_field` – an area of search.
  Directory with possible values: `vacancy_search_fields` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
  By default, all fields are used.
  Several values can be indicated.

* `experience` – work experience.
  Directory with possible values: `experience` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
  Several values can be indicated.

* `employment` – employment type.
  Directory with possible values: `employment` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
  Several values can be indicated.

* `schedule` – work schedule.
  Directory with possible values: `schedule` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
  Several values can be indicated.

* <a name="field-area"></a> `area` – a region.
  Directory with possible values: [/areas](areas.md).
  Several values can be indicated.

* `metro` – a metro line or station.
  Directory with possible values: [/metro](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-metro-stations).
  Several values can be indicated.

* `industry` – an industry of the company that posted the vacancy.
  Directory with possible values: [/industries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-industries).
  Several values can be indicated.

* `employer_id` – a [company](https://api.hh.ru/openapi/en/redoc#tag/Employer) identifier.
  Several values can be indicated.

* `currency` – a currency code.
  Directory with possible values: `currency` (code key) in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).

* `salary` – a salary rate.
  If this field is indicated, but `currency` is not, then the RUR value is
  used for `currency`.

* `label` – filter by vacancy labels.
  Directory with possible values: `vacancy_label` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
  Several values can be indicated.

* `only_with_salary` – show only the vacancies with salary specified.
  Possible values: true or false.
  By default, false is used.

* `period` – a range of days within which vacancies must be found.
  Maximal value: 30.

* `date_from` – a start date which restricts the date range of vacancy posting.
  You can't indicate it with the `period` parameter.
  The value is indicated in the [ISO 8601](general.md#date-format) format –
  `YYYY-MM-DD` or with up-to-the-second precision `YYYY-MM-DDThh:mm:ss±hhmm`.
  The shown value will be rounded down to the nearest 5 minutes.

* `date_to` – an end date which restricts the date range of vacancy posting.
  You must give it only with the `date_from` parameter.
  You can't indicate it with the `period` parameter.
  The value is indicated in the [ISO 8601](general.md#date-format) format –
  `YYYY-MM-DD` or with accuracy in seconds `YYYY-MM-DDThh:mm:ss±hhmm`.
  The shown value will be rounded down to the nearest 5 minutes.

* `top_lat`, `bottom_lat`, `left_lng`, `right_lng` – values of geographic
  coordinates.
  When searching, the value of the address indicated in the vacancy is used.
  The acceptable value is decimal degrees.
  All the four parameters of geographic coordinates must be given
  simultaneously, otherwise an error will be returned.

* `order_by` – vacancy list sorting.
  Directory with possible values: `vacancy_search_order` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
  If the sorting by `distance` from a geo-point is selected, the coordinates
  of the geo-point must be set: `sort_point_lat`, `sort_point_lng`.

* `sort_point_lat`, `sort_point_lng` – the value of geographic coordinates of
  the point that is used to sort vacancies by distance. It must be indicated
  only in case when `order_by` is set to `distance`.

* `clusters` – whether the [clusters for this search](clusters.md) are returned, default: `false`.

* `describe_arguments` — whether the [description of the used search parameters](vacancies_search_arguments.md) is returned, default: `false`

* `per_page`, `page` — [pagination parameters](general.md.#pagination). The parameter per_page is limited by 100. 

* `no_magic` – If `true` — turn off automatic vacancy transformation. Default — `false`. 
If automatic transformation is enabled, an attempt will be made to change the user's text query to a set of
parameters. For example, a query `text=moscow accountant 100500` will be transformed to
`text=accountant&only_with_salary=true&area=1&salary=100500`.

* `premium` – If `true` — the results of vacancies will take into account
premium vacancies. This type of sorting is used on the website.
Default — `false`. 

* `responses_count_enabled` — If `true` – include optional field `counters` with responses on a vacancy. Default – `false`.

* `part_time` — Vacancies for part times job. Possible values:  
  * all elements from `working_days` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).  
  * all elements from `working_time_intervals` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).  
  * all elements from `working_time_modes` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).  
  * elements `part` or `project` from `employment` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).  
  * element `accept_temporary` that show only the vacancies with accept temporary employment  

   Several values can be indicated.  

* `professional_role` – a professional role.
  Directory with possible values: [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary).
  Several values can be indicated.

<a name="search-results"></a>

When indicating paging parameters (`page`, `per_page`), a restriction takes
effect: the number of results returned can't exceed 2000. For instance, a
request `per_page=10&page=199` (displaying vacancies from 1991 to 2000) is
possible, but a request with `per_page=10&page=200` will return an error
(displaying vacancies from 2001 to 2010).

Depending on the current authorization, results may differ, as filtering by
[the list of hidden vacancies](https://api.hh.ru/openapi/en/redoc#tag/Hidden-vacancies) and [companies](https://api.hh.ru/openapi/en/redoc#tag/Blacklisted-employers) is
used for applicants.

### Response

```json
{
  "per_page": 1,
  "items": [
    {
      "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR",
        "gross": true
      },
      "name": "Secretary",
      "insider_interview": {
          "id": "12345",
          "url": "https://hh.ru/interview/12345?employerId=777"
      },
      "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Moscow"
      },
      "url": "https://api.hh.ru/vacancies/8331228",
      "published_at": "2013-07-08T16:17:21+0400",
      "relations": [ ],
      "employer": {
        "logo_urls": {
          "90": "https://hh.ru/employer-logo/289027.png",
          "240": "https://hh.ru/employer-logo/289169.png",
          "original": "https://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "https://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "contacts": {
          "name": "Name",
          "email": "user@example.com",
          "phones": [
              {
                  "country": "7",
                  "city": "985",
                  "number": "000-00-00",
                  "comment": null
              }
          ]
      },
      "response_letter_required": true,
      "address": {
        "city": "Moscow",
        "street": "Godovikova",
        "building": "9",
        "description": "Additional information",
        "lat": 55.807794,
        "lng": 37.638699,
        "metro_stations": [
          {
            "station_name": "station name",
            "line_name": "Line name",
            "station_id": "Station ID",
            "line_id": "Line ID",
            "lat": 55.807794,
            "lng": 37.638699
          }
        ]
      },
      "sort_point_distance": 226.001293,
      "alternate_url": "https://hh.ru/vacancy/8331228",
      "type": {
        "id": "open",
        "name": "Open"
      },
      "id": "8331228",
      "has_test": true,
      "response_url": null,
      "snippet": {
        "requirement": "...experience as <highlighttext>secretary</highlighttext> / office manager. - presentable appearance. - knowledge of Excel, Lotus Notes and office appliances. - oral and written English.",
        "responsibility": "Keeping private zone order (meeting rooms, kitchen). - ordering necessary goods (stationery, marketing materials, products, flowers, household goods, cleaning services, etc."
      },
      "schedule": {
        "id": "fullDay",
        "name": "Full time"
      },
      "counters": {
        "responses": 0
      }
    }
  ],
  "page": 0,
  "pages": 13,
  "found": 13,
  "clusters": null
}
```

Example: [https://api.hh.ru/vacancies?locale=EN](https://api.hh.ru/vacancies?locale=EN)

In addition to [standard vacancy fields](#nano) following optional fields will be displayed:

key | type | description
---- |---- |---------
sort_point_distance | number, null | Distance in metres between the sorting centre (indicated by parameters `sort_point_lat` and `sort_point_lng`) and the address indicated in the vacancy. If the address only includes metro stations, it will show the distance between the sorting centre and the average geometric point of the indicated stations. `sort_point_distance` value is only shown if parameters for `sort_point_lat`, `sort_point_lgn` and `order_by=distance` are indicated.
snippet | object | Additional text snippets on found vacancy. If snippet text contains search term (parameter `text`), it will be highlighted with tag `highlighttext`.
snippet.requirement | string, null | Vacancy requirements snippet if available in the description text.
snippet.responsibility | string, null | Vacancy responsibilities snippet if available in the description text.
counters.responses | number | number of responses to the vacancy

It is also possible to return [clusters](clusters.md) ('clusters' key) and [used parameters](vacancies_search_arguments.md) ('arguments' key) for this search.

### Errors

* `404 Bad Request` - if parameters have been communicated with an error

<a name="similar"></a>
## Search for vacancies similar to the vacancy

### Request

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/operation/get-vacancies-similar-to-vacancy)

<a name="nano"></a>
## Short description of the vacancy

```json
{
    "id": "7760476",
    "premium": true,
    "has_test": true,
    "response_url": null,
    "address": null,
    "alternate_url": "https://hh.ru/vacancy/7760476",
    "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=7760476",
    "department": {
      "id": "18320489-18320489-dept1",
      "name": "DEPT1"
    },
    "salary": {
        "to": null,
        "from": 100000,
        "currency": "RUR",
        "gross": true
    },
    "name": "Test automation specialist (Java, Selenium)",
    "insider_interview": {
        "id": "12345",
        "url": "https://hh.ru/interview/12345?employerId=777"
    },
    "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Moscow"
    },
    "url": "https://api.hh.ru/vacancies/7760476",
    "published_at": "2013-10-11T13:27:16+0400",
    "relations": [ ],
    "employer": {
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "https://hh.ru/employer/1455",
        "logo_urls": {
            "90": "https://hh.ru/employer-logo/289027.png",
            "240": "https://hh.ru/employer-logo/289169.png",
            "original": "https://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "id": "1455"
    },
    "response_letter_required": false,
    "type": {
        "id": "open",
        "name": "Open"
    },
    "archived": "false"
}
```

Here:

Name| Type| Description
--- | --- | -----------
 id | string| Vacancy identifier
 premium | logical | Whether it is a premium vacancy
 address | object, null | [vacancy address](address.md#Address)
 alternate_url | string, null | Link to the full vacancy presentation in web site
 apply_alternate_url | string, null | Link to the vacancy respond page in web site
 department | object, null | department from the [directory](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-employer-departments), on behalf of which the vacancy is being posted (if this feature is available for the company)
 department.id | string | Department identifier
 department.name | string | Department name
 salary | object, null | Wage
 name | string | Vacancy name
 area | object | Region of vacancy posting
 url | string, null | Link to the full vacancy presentation in the api
 published_at | string | Vacancy posting date and time
 employer | object | Short description of the employer
 response_letter_required | logical | Whether the message must be written when applying
 type | object | Vacancy type, one of the elements `vacancy_type` in the [Directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
 archived | logical | Whether it is an archived vacancy

Please see the [full vacancy](#vacancy-fields) for a description of the fields.

`url` and `alternate_url` can have the `null` meaning if the detailed
information on the vacancy is unavailable (for instance, when the vacancy has
been deleted)
