# Receiving vacancies

* [View a vacancy](#item)
* [Additional vacancy fields for employers](#author)
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

`GET /vacancies/{vacancy_id}` 

where `vacancy_id` – vacancy ID

Will return detailed information for the selected vacancy.

### Response

Successful server response is returned with `200 OK` code and contains:

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
            "original": "https://hh.ru/file/2352807.png",
            "medium": "https://hhcdn.ru/employer-logo/289312.png",
            "small": "https://hhcdn.ru/employer-logo/289313.png"
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
    "has_test": true,
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

<a name="vacancy-fields"></a>

Name | Type | Description
---- | --- | --------
id | string | Vacancy ID
description | string | Job description, contains html
branded_description | string or null | [Branded job description](#branded_description)
key_skills | array | Details of key skills indicated in the vacancy. This list may be empty.
key_skills[].name | string | name of key skill
schedule | object | Work schedule. [schedule directory entry](dictionaries.md)
schedule.id | string | Schedule ID
schedule.name | string | Schedule name
accept_handicapped | boolean | Indication that the job is available for applicants with disabilities
accept_kids | boolean | Indication that the job is available for applicants as young as 14 years old
experience | object | Required work experience. [experience](dictionaries.md) directory entry
experience.id | string | Required work experience ID
experience.name | string | Name of required work experience
address | object or null | [Vacancy address](address.md#Адрес)
alternate_url | string | Link to the vacancy on the website
apply_alternate_url | string | Link to the application for the vacancy on the website
code | string or null | Employer's internal vacancy code
department | object or null | Department on whose behalf the vacancy is uploaded (if available for the company). Employers can request [department directory](employer_departments.md).
department.id | string | Department ID
department.name | string | Department name
employment | object or null | Type of employment. [employment](dictionaries.md) directory entry
employment.id | string | Employment type ID
employment.name | string | Employment type name
salary | object or null | Salary
salary.from | number or null | Lower limit of salary range
salary.to | number or null | Upper limit of salary range
salary.gross | boolean or null | Indication that the salary is shown before tax. If not indicated — null.
salary.currency | string | Indication of salary currency ([currency](dictionaries.md) directory).
archived | boolean | Whether the vacancy is archived
name | string | Vacancy name
area | object | Vacancy region
area.id | string | Region ID
area.name | string | Region name
area.url | string | URL for getting information on the region
published_at | string | Date and time of vacancy publication
employer | object | Brief description of employer. See field description in [employer information](employers.md#item).
employer.blacklisted | boolean | Whether all vacancies of the employer are added to the [list of hidden](blacklisted.md#employers)
response_letter_required | boolean | Whether it is mandatory to fill out a message for application
type | object | Vacancy type. [vacancy_type](dictionaries.md) directory entry.
type.id | string | Vacancy type ID
type.name | string | Vacancy type name
response_url | string or null | You cannot apply for vacancies with `direct` type on hh.ru, these vacancies have an external website URL in the `response_url` key (in most cases, the employer's website with an application form)
test | object or null | Information about attached test for the job. If there is no test — `null`. **At the moment it is impossible to apply for vacancies with mandatory test with API.**
test.required | boolean | If the test is mandatory for an application
specialization | array | Specialisations. [specialisations](specializations.md) directory entries
specializations[].id | string | Specialisation ID
specializations[].name | string | Specialisation name
specializations[].profarea_id | string | ID of the profession that includes this specialisation
specializations[].profarea_name | string | Name of the profession that includes this specialisation
contacts | object or null | Contact info. For vacancies without contacts, it returns `null`.
contacts.name | string or null | Name of contact person
contacts.email | string or null | Email of contact person
contacts.phones | array | List of phone numbers of contact person. This list may be empty.
contacts.phones[].country | string | Country code
contacts.phones[].city | string | City code
contacts.phones[].number | string | Phone number
contacts.phones[].comment | string or null | Commentary
billing_type | object | Vacancy billing type. [vacancy_billing_type](dictionaries.md) directory entry.
billing_type.id | string | ID of the vacancy billing type
billing_type.name | string | Name of the vacancy billing type
allow_messages | boolean | Whether the option is enabled for the candidate to send messages to the employer after invitation/application for the job
premium | boolean | Whether it is a premium vacancy
driver_license_types | array | List of required driver license categories
driver_license_types[].id | string | Driving license category. [driver_license_types](dictionaries.md) directory entry.
accept_incomplete_resumes | boolean | Whether it is possible to apply with an incomplete resume

<a name="branded_description"></a>
### Branded job description

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

The value can be `null` if the vacancy does not have an individual description.

<a name="vacancy-fields-applicant"></a>
### Additional vacancy fields for candidates

Additional fields are returned during candidate authorisation:

```json
{
    "relations": [
        "favorited",
        "got_response"
    ],
    "negotiations_url": "https://api.hh.ru/negotiations?vacancy_id=8331228",
    "suitable_resumes_url": "https://api.hh.ru/vacancies/8331228/suitable_resumes"
}
```

Name | Type | Description
---- | --- | --------
relations | array | relations to the vacancy are returned during candidate authorisation. [vacancy_relation](dictionaries.md) directory entries.
negotiations_url | string | links to get lists of applications/invitations

See also [vacancy applications](negotiations.md#post_negotiation).


<a name="author"></a>
## Additional vacancy fields for employers

If the vacancy is requested when the author (employer) is authorised, the object
will show additional fields:

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
can_upgrade_billing_type | logical | If the vacancy billing type can be upgraded

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
  [/dictionaries](dictionaries.md).
  If the sorting by `distance` from a geo-point is selected, the coordinates
  of the geo-point must be set: `sort_point_lat`, `sort_point_lng`.

* `sort_point_lat`, `sort_point_lng` – the value of geographic coordinates of
  the point that is used to sort vacancies by distance. It must be indicated
  only in case when `order_by` is set to `distance`.

* `clusters` – whether the [clusters for this search](clusters.md) are returned, default: `false`.

* `describe_arguments` — whether the [description of the used search parameters](vacancies_search_arguments.md) is returned, default: `false`

* `per_page`, `page` — [pagination parameters](general.md.#pagination). The parameter per_page is limited by 100. 

* `no_magic` – If 'false' — turn off automatic vacancy transformation. Default — `true`. 
If automatic transformation is enabled, an attempt will be made to change the user's text query to a set of
parameters. For example, a query `text=moscow accountant 100500` will be transformed to
`text=accountant&only_with_salary=true&area=1&salary=100500`.

* `premium` – If `true` — the results of vacancies will take into account
premium vacancies. This type of sorting is used on the website.
Default — `false`. 

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
            "original": "https://hh.ru/file/2352807.png",
            "medium": "https://hhcdn.ru/employer-logo/289312.png",
            "small": "https://hhcdn.ru/employer-logo/289313.png"
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
      "has_test": true,
      "response_url": null,
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

Example: [https://api.hh.ru/vacancies?locale=EN](https://api.hh.ru/vacancies?locale=EN)

In addition to [standard vacancy fields](#nano) following optional fields will be displayed:

key | type | description
---- |---- |---------
sort_point_distance | number, null | Distance in metres between the sorting centre (indicated by parameters `sort_point_lat` and `sort_point_lng`) and the address indicated in the vacancy. If the address only includes metro stations, it will show the distance between the sorting centre and the average geometric point of the indicated stations. `sort_point_distance` value is only shown if parameters for `sort_point_lat`, `sort_point_lgn` and `order_by=distance` are indicated.
snippet | object | Additional text snippets on found vacancy. If snippet text contains search term (parameter `text`), it will be highlighted with tag `highlighttext`.
snippet.requirement | string, null | Vacancy requirements snippet if available in the description text.
snippet.responsibility | string, null | Vacancy responsibilities snippet if available in the description text.

It is also possible to return [clusters](clusters.md) ('clusters' key) and [used parameters](vacancies_search_arguments.md) ('arguments' key) for this search.

<a name="similar"></a>
## Search for vacancies similar to the vacancy

### Request

`GET /vacancies/{vacancy_id}/similar_vacancies`

where `vacancy_id` – ID of the vacancy.

Accepts the same parameters as [vacancy search](#search-params) and returns the same
results as [vacancy search](#search-results)

Additionally if vacancy with `vacancy_id` does not exist `404 Not Found` will be
returned in response.


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
            "original": "https://hh.ru/file/2352807.png",
            "medium": "https://hhcdn.ru/employer-logo/289312.png",
            "small": "https://hhcdn.ru/employer-logo/289313.png"
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

Please see the [full vacancy](#vacancy-fields) for a description of the fields.

`url` and `alternate_url` can have the `null` meaning if the detailed
information on the vacancy is unavailable (for instance, when the vacancy has
been deleted)
