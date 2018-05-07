# Receiving vacancies

* [View a vacancy](#item)
* [Extra fields for the author of the vacancy](#author)
* [Favorite vacancies](#favorited)
* [Search for vacancies](#search)
* [Search for vacancies similar to the vacancy](#similar)
* [Short description of the vacancy](#nano)
* [Hidden vacancies](blacklisted.md)

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

`GET /vacancies/{vacancy_id}` will return a detailed information on the indicated vacancy

Example: [https://api.hh.ru/vacancies/12080698?locale=EN](https://api.hh.ru/vacancies/12080698?locale=EN)

```json
{
    "id": "8331228",
    "description": "...",
    "branded_description": "<style>...</style><div>...</div><script></script>",
    "key_skills": [
        {
            "name": "Visitor reception"
        },
        {
            "name": "Source document circulation"
        }
    ],
    "schedule": {
        "id": "fullDay",
        "name": "Full time"
    },
    "accept_handicapped": false,
    "accept_kids": false,
    "experience": {
        "id": "between3And6",
        "name": "Between 3 and 6 years"
    },
    "address": {
        "city": "Moscow",
        "street": "Godovikova",
        "building": "9",
        "description": "Additional information",
        "lat": 55.807794,
        "lng": 37.638699,
        "raw": "Textual address description as entered",
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
    "alternate_url": "https://hh.ru/vacancy/8331228",
    "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
    "code": "HHR-3487",
    "department": {
        "id": "18320489-18320489-dept1",
        "name": "DEPT1"
    },
    "employment": {
        "id": "full",
        "name": "Full time"
    },
    "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR",
        "gross": true
    },
    "archived": false,
    "name": "Secretary",
    "area": {
        "url": "https://api.hh.ru/areas/1?locale=EN",
        "id": "1",
        "name": "Moscow"
    },
    "published_at": "2013-07-08T16:17:21+0400",
    "relations": [],
    "negotiations_url": "https://api.hh.ru/negotiations?vacancy_id=8331228&locale=EN",
    "allow_messages": true,
    "suitable_resumes_url": "https://api.hh.ru/vacancies/8331228/suitable_resumes?locale=EN",
    "employer": {
        "logo_urls": {
            "90": "https://hh.ru/employer-logo/289027.png",
            "240": "https://hh.ru/employer-logo/289169.png",
            "original": "https://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455?locale=EN",
        "alternate_url": "https://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
    },
    "response_letter_required": true,
    "type": {
        "id": "open",
        "name": "Open"
    },
    "response_url": null,
    "test": {
        "required": false
    },
    "specializations": [
        {
            "profarea_id": "4",
            "profarea_name": "Administrative staff",
            "id": "4.255",
            "name": "Reception"
        },
        {
            "profarea_id": "4",
            "profarea_name": "Administrative staff",
            "id": "4.429",
            "name": "Office work"
        },
        {
            "profarea_id": "4",
            "profarea_name": "Administrative staff",
            "id": "4.264",
            "name": "Secretary"
        },
        {
            "profarea_id": "4",
            "profarea_name": "Administrative staff",
            "id": "4.181",
            "name": "Beginner level, Little experience"
        }
    ],
    "contacts": {
        "name": "First name",
        "email": "user@example.com",
        "phones": [
            {
                "comment": null,
                "city": "985",
                "number": "000-00-00",
                "country": "7"
            }
        ]
    },
    "billing_type": {
        "id": "standard",
        "name": "Standard"
    },
    "driver_license_types": [
        {
            "id": "A"
        },
        {
            "id": "B"
        }
    ],
    "accept_incomplete_resumes": false
}
```

`branded_description` – a string with HTML code ( `<script/>` and `<style/>` may
be present) that is an alternative to a standard vacancy description. The HTML
code is adapted for mobile devices and displays correctly without javascript
support enabled. Whereas:

* The content stretches to 100% of the container width and fits within 300px
  without scrolling.
* The content is designed to be inserted in a binding including the vacancy
  name, required experience, region, employment type and work schedule, as well
  as a link to the company that posted the vacancy.
* Images that can found in such description are adapted to retina displays.
* Font size should be at least 12px, line spacing – at least 16px.

The value may be null if the vacancy has no individual description.

If case of an authorized request, the `relations` key returns values from the
`vacancy_relation` reference in [/dictionaries](dictionaries.md).


The `negotiations_url` key returns a link to a list of applications/invitations
for the vacancy of the current applicant user (for other user types, `null` is
returned).

One cannot apply for a vacancy of the `direct` type on hh.ru, as these vacancies
have a URL to an external website in the `response_url` key (most often it is
the employer's website with an application form). [More about documents on
applications](negotiations.md#post_negotiation)

The `contacts` key contains contact information. In vacancies with no indicated
contact information, `null` is returned. All internal keys are either strings or
null. The phone number list may be empty.

The `test` key contains information about the test attached to the vacancy. If
there is no test, `null` is returned. Otherwise, an object with the `required`
key is returned, which means a test must be taken to complete the application.

-----

**At the moment, it is impossible to apply for vacancies that require to take a test via the API.**

-----

The returned `key_skills` key contains information about key skills specified in
the vacancy.

Possible values `billing_type` and `site` are available in directories in
[/dictionaries](dictionaries.md) (`vacancy_billing_type` and `vacancy_site`
respectively).

The returned `allow_messages` key specifies whether the applicant will have the
possibility to create messages after the invitation.

### Errors

* `403 Forbidden` – authorization is failed.


<a name="author"></a>
## Extra vacancy fields

For the vacancy request with initiator authorization, optional fields will be
displayed:

```json
{
  "expires_at": "2015-01-09T17:03:35+0300",
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
response_notifications | logical | whether to notify manager on new responses
hidden | logical | whether the vacancy is deleted (hidden from the archive)
can_upgrade_billing_type | logical | Whether it is possible to upgrade vacancy billing type 

In object `manager` – the information on the manager posted the vacancy.

In object `branded_template` – info on
[branded template](employer_vacancy_branded_templates.md) used in vacancy.

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
    "invitations": 10
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


<a name="favorited"></a>
## Selected vacancies

These methods require applicant authorization, otherwise `403 Forbidden` will be
returned.

`GET /vacancies/favorited` – returns a subset of vacancies added in the
favorites list. Paging works with standard page&per\_page parameters, pages are
numbered from zero.

`PUT /vacancies/favorited/{vacancy_id}` returns the indicated vacancy in the
list. This operation is idempotent: when adding a vacancy that is already
present in the favorites list, `204 No Content` will be returned, as in the case
of initial adding. If a vacancy is not found, the server will return
`404 Not Found`; if for some reason the user lacks rights to put a vacancy in
the favorites list, the server will return `404 Not Found`. Apart from the HTTP
code, the server can also return a description of
[the cause of the error](errors.md#vacancies_favorited).

`DELETE /vacancies/favorited/{vacancy_id}` will delete a vacancy from the
authorized user's favorites list. The operation is also idempotent. If deleted
successfully, the method returns `204 No Content`.



<a name="search"></a>
## Search for vacancies

`GET /vacancies` will return the results of vacancy search.

<a name="search-params"></a>
Acceptable parameters:

Some parameters take multiple values: `key=value&key=value`.

* `text` – text field.  
  The sent value is searched in the vacancy fields specified in the `search_field` parameter.  
  As with the main website, a query language is available: [https://hh.ru/article/1175](https://hh.ru/article/1175).
  There is [autoaddition](suggests.md#vacancy-search-keyword) especially for this field.

* `search_field` – an area of search.
  Directory with possible values: `vacancy_search_fields` in
  [/dictionaries](dictionaries.md).
  By default, all fields are used.
  Several values can be indicated.

* `experience` – work experience.
  Directory with possible values: `experience` in
  [/dictionaries](dictionaries.md).

* `employment` – employment type.
  Directory with possible values: `employment` in
  [/dictionaries](dictionaries.md).
  Several values can be indicated.

* `schedule` – work schedule.
  Directory with possible values: `schedule` in
  [/dictionaries](dictionaries.md).
  Several values can be indicated.

* <a name="field-area"></a> `area` – a region.
  Directory with possible values: [/areas](areas.md).
  Several values can be indicated.

* `metro` – a metro line or station.
  Directory with possible values: [/metro](metro.md).
  Several values can be indicated.

* `specialization` – a professional area or specialization.
  Directory with possible values: [/specializations](specializations.md).
  Several values can be indicated.

* `industry` – an industry of the company that posted the vacancy.
  Directory with possible values: [/industries](industries.md).
  Several values can be indicated.

* `employer_id` – a [company](employers.md) identifier.
  Several values can be indicated.

* `currency` – a currency code.
  Directory with possible values: `currency` (code key) in
  [/dictionaries](dictionaries.md).

* `salary` – a salary rate.
  If this field is indicated, but `currency` is not, then the RUR value is
  used for `currency`.

* `label` – filter by vacancy labels.
  Directory with possible values: `vacancy_label` in
  [/dictionaries](dictionaries.md).
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

* `date_to` – an end date which restricts the date range of vacancy posting.
  You must give it only with the `date_from` parameter.
  You can't indicate it with the `period` parameter.
  The value is indicated in the [ISO 8601](general.md#date-format) format –
  `YYYY-MM-DD` or with up-to-the-second precision `YYYY-MM-DDThh:mm:ss±hhmm`.

* `top_lat`, `bottom_lat`, `left_lng`, `right_lng` – values of geographic
  coordinates.
  When searching, the value of the address indicated in the vacancy is used.
  The acceptable value is decimal degrees.
  All the four parameters of geographic coordinates must be given
  simultaneously, otherwise an error will be returned.

* `order_by` – vacancy list sorting.
  Directory with possible values: `vacancy_search_order` in
  [/dictionaries](dictionaries.md).
  If the sorting by `distance` from a geo-point is selected, the coordinates
  of the geo-point must be set: `sort_point_lat`, `sort_point_lng`.

* `sort_point_lat`, `sort_point_lng` – the value of geographic coordinates of
  the point that is used to sort vacancies by distance. It must be indicated
  only in case when `order_by` is set to `distance`.

* `clusters` – whether the cluster list should be returned for this search,
  by default: `false`. More information on this [/docs/clusters.md](clusters.md).

<a name="search-results"></a>

When indicating paging parameters (`page`, `per_page`), a restriction takes
effect: the number of results returned can't exceed 2000. For instance, a
request `per_page=10&page=199` (displaying vacancies from 1991 to 2000) is
possible, but a request with `per_page=10&page=200` will return an error
(displaying vacancies from 2001 to 2010).

If parameters contain an error, `400 Bad request` will be returned in response
with the error description in the body. Unknown parameters and parameters with
an error in the name are ignored.

Depending on the current authorization, results may differ, as filtering by
[the list of hidden vacancies and companies](blacklisted.md) is
used for applicants.


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
      "response_letter_required": true,
      "address": {
        "city": "Moscow",
        "street": "Godovikova",
        "building": "9",
        "description": "Additional information",
        "lat": 55.807794,
        "lng": 37.638699,
        "raw": "Textual address description as entered",
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
      "snippet": {
        "requirement": "...experience as <highlighttext>secretary</highlighttext> / office manager. - presentable appearance. - knowledge of Excel, Lotus Notes and office appliances. - oral and written English.",
        "responsibility": "Keeping private zone order (meeting rooms, kitchen). - ordering necessary goods (stationery, marketing materials, products, flowers, household goods, cleaning services, etc."
      }
    }
  ],
  "page": 0,
  "pages": 13,
  "found": 13,
  "clusters": null
}
```

In addition to [standard vacancy fields](#nano) following optional fields will be displayed:

key | type | description
---- |---- |---------
sort_point_distance | number, null | Distance (meters) between sort center (defined by `sort_point_lat`, `sort_point_lng` parameters) and vacancy address point. In case of only metro stations are presented in address, distance between sort center and vacancy metro stations geometrical center is presented. `sort_point_distance` value is presented only if parameters `sort_point_lat`, `sort_point_lng`, `order_by=distance` are used for query.
snippet | object | Additional text snippets on found vacancy. If snippet text contains search term (parameter `text`), it will be highlighted with tag `highlighttext`.
snippet.requirement | string, null | Vacancy requirements if available in the description text.
snippet.responsibility | string, null | Vacancy responsibilities if available in the description text.

### Errors

* `400 Bad Request` – invalid request parameters.
* `403 Forbidden` – authorization is failed.


<a name="similar"></a>
## Search for vacancies similar to the vacancy

### Request

`GET /vacancies/{vacancy_id}/similar_vacancies`

where `vacancy_id` – ID of the vacancy.

Accepts the same parameters as [vacancy search](#search-params) and returns the same
results as [vacancy search](#search-results)

Additionally if vacancy with `vacancy_id` does not exist `404 Not Found` will be
returned in response.

### Errors

* `403 Forbidden` – authorization is failed.


<a name="nano"></a>
## Short description of the vacancy

```json
{
    "id": "7760476",
    "premium": true,
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
 department | object, null | department from the [directory](employer_departments.md), on behalf of which the vacancy is being posted (if this feature is available for the company)
 department.id | string | Department identifier
 department.name | string | Department name
 salary | object, null | Wage
 name | string | Vacancy name
 area | object | Region of vacancy posting
 url | string, null | Link to the full vacancy presentation in the api
 published_at | string | Vacancy posting date and time
 employer | object | Short description of the employer
 response_letter_required | logical | Whether the message must be written when applying
 type | object | Vacancy type, one of the elements `vacancy_type` in the [Directory](dictionaries.md)
 archived | logical | Whether it is an archived vacancy

`url` and `alternate_url` can have the `null` meaning if the detailed
information on the vacancy is unavailable (for instance, when the vacancy has
been deleted)
