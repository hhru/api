# Vacancies

* [View a vacancy](#item)
* [Extra fields for the author of the vacancy](#author)
* [Favorite vacancies](#favorited)
* [Search by vacancies](#search)
* [Short description of the vacancy](#nano)
* [Hidden vacancies](blacklisted.md)
* [Vacancy posting](#creation)
* [Vacancy fields conditions](#conditions)
* [Vacancy editing](#edit)
* [Vacancy prolongation](#prolongate)


<a name="item"/>
## View a vacancy

`GET /vacancies/{vacancy_id}` will return a detailed information on the indicated vacancy

Example: [https://api.hh.ru/vacancies/12080698?locale=EN](https://api.hh.ru/vacancies/12080698?locale=EN)

```json
{
      "description": "...",
      "branded_description": "<style>...</style><div>...</div><script></script>",
      "key_skills": [
        {"name": "Visitor reception"},
        {"name": "Source document circulation"}
      ],
      "schedule": {
        "id": "fullDay",
        "name": "Full time"
      },
      "accept_handicapped": false,
      "experience": {
        "id": "between3And6",
        "name": "Between 3 and 6 years"
      },
      "address": null,
      "alternate_url": "http://hh.ru/vacancy/8331228",
      "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=8331228",
      "employment": {
        "id": "full",
        "name": "Full time"
      },
      "id": "8331228",
      "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR"
      },
      "archived": false,
      "name": "Secretary",
      "area": {
        "url": "https://api.hh.ru/areas/1?locale=EN",
        "id": "1",
        "name": "Moscow"
      },
      "published_at": "2013-07-08T16:17:21+0400",
      "relations": [ ],
      "negotiations_url": "https://api.hh.ru/negotiations?vacancy_id=8331228&locale=EN",
      "allow_messages": true,
      "suitable_resumes_url": "https://api.hh.ru/vacancies/8331228/suitable_resumes?locale=EN",
      "employer": {
        "logo_urls": {
          "90": "http://hh.ru/employer-logo/289027.png",
          "240": "http://hh.ru/employer-logo/289169.png",
          "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455?locale=EN",
        "alternate_url": "http://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "response_letter_required": true,
      "response_url": null,
      "type": {
        "id": "open",
        "name": "Open"
      },
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
      "site": {
        "id": "hh",
        "name": "hh.ru"
      },
      "department": {
        "id": "HH-1455-TECH",
        "name": "HeadHunter::Technical Department"
      },
      "hidden": null
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


<a name="author"/>
## Extra vacancy fields

If a vacancy is requested by an authorized user, the object will return the
following fields:

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
  }
}
```

| key                     | JSON type | description                                                            |
|-------------------------|-----------|------------------------------------------------------------------------|
| expires_at              | string    | date+vacancy posting expiration date                                   |
| response_notifications  | boolean   | whether to notify the manager about new applications                   |
| hidden                  | boolean   | whether the vacancy is deleted (hidden from the archive)               |

The `manager` object contains information about the manager who posted the
vacancy.

The `branded_template` object contains information about the
[branded template](employer_vacancy_branded_templates.md) which is used in
the vacancy.

The author of the vacancy can also access the `id` key in the `test` object, and
in the `address` object, they can access:


```json
{
  "address": {
    "id": "1448",
    "show_metro_only": false
  }
}
```

You can find more information about these fields in the section about 
[vacancy posting](#creation_fields).


<a name="favorited"/>
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



<a name="search"/>
## Search by vacancies

`GET /vacancies` will return the results of vacancy search.

Acceptable parameters:

Some parameters take multiple values: `key=value&key=value`.

* `text` – text field.  
  The sent value is searched in the vacancy fields specified in the `search_field` parameter.  
  As with the main website, a query language is available: [http://hh.ru/article/1175](http://hh.ru/article/1175).  
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

* <a name="field-area"/> `area` – a region.
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
      "relations": [ ],
      "employer": {
        "logo_urls": {
          "90": "http://hh.ru/employer-logo/289027.png",
          "240": "http://hh.ru/employer-logo/289169.png",
          "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "http://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "http://hh.ru/vacancy/8331228",
      "type": {
        "id": "open",
        "name": "Open"
      },
      "id": "8331228"
    }
  ],
  "page": 0,
  "pages": 13,
  "found": 13,
  "clusters": null
}
```

Example: [https://api.hh.ru/vacancies?locale=EN](https://api.hh.ru/vacancies?locale=EN)


<a name="nano"/>
## Short description of the vacancy

```json
{
    "id": "7760476",
    "premium": true,
    "address": null,
    "alternate_url": "http://hh.ru/vacancy/7760476",
    "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=7760476",
    "salary": {
        "to": null,
        "from": 100000,
        "currency": "RUR"
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
        "alternate_url": "http://hh.ru/employer/1455",
        "logo_urls": {
            "90": "http://hh.ru/employer-logo/289027.png",
            "240": "http://hh.ru/employer-logo/289169.png",
            "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "id": "1455"
    },
    "response_letter_required": false,
    "type": {
        "id": "open",
        "name": "Open"
    }
}
```

Here:

Name| Type| Description
--- | --- | -----------
 id | string| Vacancy identifier
 premium | logical| Whether it is a premium vacancy
 address | object, null | [vacancy address](address.md#Address)
 alternate_url | string, null | Link to the full vacancy presentation in web site
 apply_alternate_url | string, null | Link to the vacancy respond page in web site
 salary | object, null | Wage
 name | string | Vacancy name
 area | object | Region of vacancy posting
 url | string, null | Link to the full vacancy presentation in the api
 published_at | string | Vacancy posting date and time
 employer | object | Short description of the employer
 response_letter_required | logical | Whether the message must be written when applying
 type | object | Vacancy type, one of the elements `vacancy_type` in the [Directory](dictionaries.md)

`url` and `alternate_url` can have the `null` meaning if the detailed
information on the vacancy is unavailable (for instance, when the vacancy has
been deleted)



<a name="creation"/>
## Vacancy posting

`POST /vacancies`


### General information

The request body should be [JSON](general.md#request-body) with data on the
vacancy being posted. The format of the data is similar to the
[vacancy view](#item), but also contains some additional fields.

> In accordance with
> [RF law № 1032-1 dated 19.04.1991, as amended on 02.07.2013](http://hh.ru/article/13967)
> it is prohibited to post information limiting rights or providing privileges
> for applicants on the base of their gender, age, marital status as well as
> other circumstances that are not related to the qualifications of employees.

* if posted successfully, a corresponding service will be written off.
* all vacancies undergo manual moderation.
* in a few minutes after having been posted, the vacancy will become available
  for search.


### Useful links

* [rules for posting vacancies](http://hh.ru/article/341)
* [how do I formulate a good vacancy description](http://hh.ru/article/16239)
* [list of posted vacancies](employer_vacancies.md#active)
* [list of archived vacancies](employer_vacancies.md#archived)
* [list of deleted vacancies](employer_vacancies.md#hidden)
* [field filling conditions](#conditions)


<a name="creation-example"/>
### Request body example

```json
{
  "description": "<p>— Eh bien, mon prince. Gênes et Lucques ne sont plus que des apanages, des поместья, de la famille Buonaparte. Non, je vous préviens que si vous ne me dites pas que nous avons la guerre, si vous vous permettez encore de pallier toutes les infamies, toutes les atrocités de cet Antichrist (ma parole, j'y crois) — je ne vous connais plus, vous n'êtes plus mon ami, vous n'êtes plus мой верный раб, comme vous dites. Ну, здравствуйте, здравствуйте.</p><p><em>Je vois que je vous fais peur</em>, садитесь и рассказывайте.</p>",
  "key_skills": [
    {"name": "Cold calling"},
    {"name": "Sales promotion"}
  ],
  "schedule": {
    "id": "flyInFlyOut"
  },
  "experience": {
    "id": "moreThan6"
  },
  "employment": {
    "id": "full"
  },
  "name": "Sales manager",
  "area": {
    "id": "1"
  },
  "type": {
    "id": "open"
  },
  "employer": {
    "id": "1455"
  },
  "specializations": [
    {
      "id": "17.324"
    },
    {
      "id": "3.148"
    }
  ],
  "response_letter_required": true,
  "salary": {
    "from": 100,
    "to": 500,
    "currency": "USD"
  },
  "contacts": {
    "name": "Ivanov Ivan",
    "email": "i.ivanov@example.com",
    "phones": [
      {
        "country": "7",
        "city": "495",
        "number": "1234567",
        "comment": "from 10 to 20"
      }
    ]
  },
  "accept_handicapped": true,
  "code": "code-1234",
  "response_notifications": true,
  "allow_messages": true,
  "billing_type": {
    "id": "standard"
  },
  "site": {
    "id": "hh"
  },
  "address": {
    "id": "123",
    "show_metro_only": true
  },
  "manager": {
    "id": "321"
  },
  "test": {
    "id": "42",
    "required": true
  },
  "branded_template": {
    "id": "marketing"
  }
}
```


<a name="creation_fields"/>
### Request body

* `[]` (e.g. in specialization fields and in contacts) means that the value of
  the key is an array of objects.

* `a.b` means an object `a` with a key `b` of the described type.

| Path                        | JSON type       | Description |
|-----------------------------|-----------------|-------------|
| name                        | string          | title |
| description                 | string          | description in html, at least 200 characters |
| key_skills                  | array           | key skills list, no more than 30 |
| key_skills[].name           | string          | key skill name |
| specializations             | array           | specialization list |
| specializations[].id        | string          | specialization from the [directory](specializations.md) |
| area.id                     | string          | posting region from the [directory](areas.md) |
| type.id                     | string          | type from the [vacancy_type directory](dictionaries.md) |
| billing_type.id             | string          | billing type from the [vacancy_billing_type directory](dictionaries.md) |
| site.id                     | string          | website for posting from the [vacancy_site directory](dictionaries.md) |
| code                        | string          | internal vacancy code |
| department.id               | string          | department from the [directory](employer_departments.md), on behalf of which the vacancy is being posted (if this is available for the company) |
| salary                      | object or null  | salary |
| salary.from                 | numeric or null | salary range minimum |
| salary.to                   | numeric or null | salary range maximum |
| salary.currency             | string          | currency code from the [currency directory](dictionaries.md) |
| address                     | object or null  | address |
| address.id                  | string          | address from the [list of employer's available addresses](employer_addresses.md) |
| address.show_metro_only     | boolean         | show only metro for the indicated address |
| experience.id               | string          | required work experience from the [experience directory](dictionaries.md) |
| schedule.id                 | string          | work schedule from the [schedule directory](dictionaries.md) |
| employment.id               | string          | employment type from the [employment directory](dictionaries.md) |
| contacts                    | object          | contact information (for trade vacancies) |
| contacts.name               | string          | contact person |
| contacts.email              | string          | email |
| contacts.phones             | array           | phone number list for communication |
| contacts.phones[].country   | string          | country code |
| contacts.phones[].city      | string          | city code |
| contacts.phones[].number    | string          | telephone |
| contacts.phones[].comment   | string or null  | comment (convenient time to call this number) |
| test                        | object          | vacancy test |
| test.id                     | string          | test that will be added to the vacancy |
| test.required               | boolean         | require to take a test to apply for the vacancy |
| response_url                | string          | application URL for direct vacancies (`type.id=direct`) |
| custom_employer_name        | string          | company name for anonymous vacancies (`type.id=anonymous`), e.g. "a large Russian bank" |
| employer.id                 | string          | employer who the vacancy is being posted for |
| manager.id                  | string          | contact person (a manager) for the vacancy being posted; by default it is the current user |
| response_notifications      | boolean         | whether to notify about new applications |
| allow_messages              | boolean         | ability to [message candidates](http://inboxemp.hh.ru/) on the subject of the vacancy |
| response_letter_required    | boolean         | demand a cover letter |
| accept_handicapped          | boolean         | indication that the vacancy is available for disabled applicants |
| branded_template.id         | string          | <a name="branded-template-field" /> branded template from the [directory](employer_vacancy_branded_templates.md#list) |


<a name="creation-results"/>
### Request result

* `204 No Content` – added successfully. The `Location` header will contain a
  link to the added vacancy.
* `403 Forbidden` – addition of vacancies is not available for this user or
  is not available because a vacancy with similar data had already been posted
  by this employer. If you are sure that addition of the duplicate is necessary,
  you can add the `POST /vacancies?ignore_duplicates=true` parameter to
  your request.
* `400 Bad Request` – errors in fields when adding a vacancy.

In addition to an HTTP code, the server can return
[error reasons](errors.md#vacancies-create-n-edit).


<a name="conditions"/>
## Field filling and vacancy editing conditions

`GET /vacancy_conditions`

Each end field is described by the rules object. If the field consists of the
object with a number of fields, these fields are described in the `fields`.

The vacancy fields conditions are available only to employers, otherwise `403
Forbidden` error code will be returned.

For all the fields and their parts it is specified whether they are required
(`required`).


### Response example

Successful response will include the `200 OK` response code and will have a
body:

```json
{
    "accept_handicapped": {
        "required": false
    },
    "address": {
        "fields": {
            "show_metro_only": {
                "required": false
            }
        },
        "required": false
    },
    "allow_messages": {
        "required": false
    },
    "area": {
        "required": true
    },
    "billing_type": {
        "required": true
    },
    "code": {
        "max_length": 50,
        "min_length": 0,
        "required": false
    },
    "contacts": {
        "fields": {
            "email": {
                "max_length": 255,
                "min_length": 0,
                "required": false
            },
            "name": {
                "max_length": 255,
                "min_length": 0,
                "required": true
            },
            "phones": {
                "fields": {
                    "city": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\d{0,6}$",
                        "required": true
                    },
                    "comment": {
                        "max_length": 255,
                        "min_length": 0,
                        "required": false
                    },
                    "country": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\+?\\d{0,5}$",
                        "required": true
                    },
                    "number": {
                        "max_length": 32,
                        "min_length": 4,
                        "regexp": "^[\\d -]{4,32}$",
                        "required": true
                    }
                },
                "max_count": 2,
                "min_count": 0,
                "required": true
            }
        },
        "required": false
    },
    "custom_employer_name": {
        "max_length": 150,
        "min_length": 0,
        "required": false
    },
    "department": {
        "max_length": 32,
        "min_length": 0,
        "required": false
    },
    "description": {
        "max_length": 10000,
        "min_length": 200,
        "required": true
    },
    "employment": {
        "required": false
    },
    "experience": {
        "required": false
    },
    "key_skills": {
        "max_count": 30,
        "min_count": 0,
        "required": false
    },
    "manager": {
        "required": false
    },
    "name": {
        "max_length": 220,
        "min_length": 0,
        "required": true
    },
    "response_letter_required": {
        "required": false
    },
    "response_notifications": {
        "required": false
    },
    "response_url": {
        "max_length": 511,
        "min_length": 0,
        "regexp": "^(http|https)://.+$",
        "required": false
    },
    "salary": {
        "fields": {
            "currency": {
                "required": false
            },
            "from": {
                "required": false
            },
            "to": {
                "required": false
            }
        },
        "required": false
    },
    "schedule": {
        "required": false
    },
    "site": {
        "required": true
    },
    "specializations": {
        "max_count": null,
        "min_count": 1,
        "required": true
    },
    "test": {
        "fields": {
            "required": {
                "required": false
            }
        },
        "required": false
    },
    "type": {
        "required": true
    }
}

```



<a name="edit"/>
## Vacancy editing

`PUT /vacancies/{vacancy_id}`

Vacancy editing is similar to vacancy creation, but there is also a possibility to transfer separate fields in the object for partial editing of the vacancy.
Composite fields (e.g. `salary`, `contacts`, `specializations`) can be edited only wholly, indicating the entire object. For example, to edit a salary currency, one must also state the currency values, and to edit a specialization, one should also specify the entire list.


### Fields available for editing

| field                      | description                                                      |
|----------------------------|------------------------------------------------------------------|
| name                       | title                                                            |
| description                | description                                                      |
| key_skills                 | key skills                                                       |
| schedule                   | work schedule                                                    |
| experience                 | required work experience                                         |
| employment                 | employment type                                                  |
| specializations            | specialization list                                              |
| salary                     | salary                                                           |
| address                    | address                                                          |
| test                       | test task                                                        |
| department                 | department                                                       |
| code                       | internal vacancy code                                            |
| response_letter_required   | requirement to enclose a cover letter when applying              |
| accept_handicapped         | indication that the vacancy is available for disabled applicants |
| response_notifications     | tuning of the new application notifications                      |
| allow_messages             | ability to message candidates on the subject of the vacancy      |
| contacts                   | contact information (for trade vacancies)                        |
| custom_employer_name       | company name for anonymous vacancies                             |
| response_url               | application URL for direct vacancies                             |

Other fields are either read-only or can be set only when creating a vacancy.


### Request result

* `204 No Content` – updated successfully.
* `404 Not Found` – the edited vacancy is not found.
* `403 Forbidden` – vacancy editing is not available for this user.
* `400 Bad Request` – errors in fields when editing a vacancy.

In addition to an HTTP code, the server can return
[error reasons](errors.md#vacancies-create-n-edit).


<a name="edit_more"/>
### Changing the billing type, vacancy manager

Changing the vacancy billing type as well as transferring the vacancy to another
company manager is similar to editing `POST /vacancies/{vacancy_id}`. The only
feature is that these fields (`billing_type` and `manager`) must be sent
separately from other vacancy fields.

```
PUT /vacancies/{vacancy_id}
{"billing_type":{"id":"premium"}
```

```
PUT /vacancies/{vacancy_id}
{"manager":{"id":"1337"}
```

If sent with any other fields, an error will be returned.


<a name="other-actions" />
### Other actions

* [archiving](employer_vacancies.md#archive)
* [deleting](employer_vacancies.md#hide)
* [restoring deleted vacancies](employer_vacancies.md#restore)


<a name="prolongate"/>
## Vacancy prolongation

**Prolongation of the vacancy costs the same as a new posting**

To extend a vacancy posting, a `POST /vacancies/{vacancy_id}/prolongate` request
must be sent.

There are limitations on vacancy extension, which are subject to change. At the
moment, the following rules are in force:

* standard vacancies can be extended if no less than 3 days have passed since
  the last extension.
* "standard plus" vacancies can be extended no earlier than 5 days before the
  posting end date.
