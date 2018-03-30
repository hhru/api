# Employers/companies

<a name="search"></a>
## Company search

`GET /employers` will return the company search results.

Possible parameters:

* text – a text field, the given value is searched in the company name and
  description.
* area – a multiple parameter, identifier of the employer's region. You can
  find region identifiers in the [region directory](areas.md)
* type – a multiple parameter, employer type. Permitted values – keys in the
  `employer_type` section in [/dictionaries](dictionaries.md)
* only_with_vacancies – return only the employers that currently
  have open vacancies (`true`) or all employers (`false`); by default it is
  set to `false`
* page – the number of the page with employers (counted from 0, by default
  set to 0)
* per_page – number of elements per page (by default – 20)

Maximum number of employers displayed – 2000.

Response:

```json
{
    "per_page": 20,
    "page": 0,
    "pages": 1,
    "found": 1,
    "items": [
        {
            "id": "1455",
            "name": "HeadHunter",
            "url": "https://api.hh.ru/employers/1455",
            "alternate_url": "https://hh.ru/employer/1455",
            "vacancies_url": "https://api.hh.ru/vacancies?employer_id=1455",
            "open_vacancies": 19,
            "logo_urls": {
              "90":  "https://hh.ru/employer-logo/289027.png"
            }
        }
    ]
}
```

| Name      | Type             | Description                                            |
|-----------|------------------|--------------------------------------------------------|
| per_page  | number           | number of elements displayed per page                  |
| page      | number           | number of page displayed                               |
| pages     | number           | number of pages with data                              |
| found     | number           | number of employers found by the given search criteria |
| items     | array of objects | found employers (maximum of per\_page elements)        |

Each element of the items array contains a short presentation of the employer
and additionally indicates the number of open vacancies.

| Name            | Type         | Description                                           |
|-----------------|--------------|-------------------------------------------------------|
| id              | string       | employer identifier                                   |
| name            | string       | employer name                                         |
| url             | string       | link to the detailed employer description             |
| alternate_url   | string       | link to the employer description on the website       |
| vacancies_url   | string       | link to the search results of the company's vacancies |
| open_vacancies  | number       | number of the employer's open vacancies               |
| logo_urls       | object, null | company's logos (see below)                           |

In case incorrect values are given in the parameters, the `400 Bad Request`
response code will be returned. At the same time the response body will contain
the information saying which parameter had the error in it. For example: to the
request `https://api.hh.ru/employers?type=abracadabra` the `400 Bad Request`
response will be returned with the body:

```json
    {
        "bad_arguments": [
            {
                "name": "type",
                "description": "unknown type"
            }
         ]
    }
```

### Errors

* `400 Bad Request` – invalid request parameters.
* `403 Forbidden` – authorization is failed.


<a name="item"></a>
## Employer/company

`GET /employers/{employer_id}` returns the data about the company with a link
to the company's vacancies.

```json
{
    "name": "HeadHunter",
    "type": "company",
    "id": "1455",
    "site_url": "https://hh.ru",
    "description": "...",
    "branded_description": "<style>...</style><div>...</div><script></script>",
    "vacancies_url": "https://api.hh.ru/vacancies?employer_id=1455",
    "alternate_url": "https://hh.ru/employer/1455",
    "logo_urls": {
        "90": "https://hh.ru/employer-logo/289027.png",
        "240": "https://hh.ru/employer-logo/289169.png",
        "original": "https://hh.ru/file/2352807.png"
    },
    "area": {
        "url": "https://api.hh.ru/areas/113",
        "id": "113",
        "name": "Russia"
    },
    "trusted": true
}
```

`branded_description` – a string with the HTML code (`<script/>` and `<style/>`
presence is possible), which is an alternative to the standard company
description. HTML is adapted for mobile devices and is displayed correctly
without any javascript support. At that:

* Content width extends for 100% of the container width and is fit in 300px
  without any scrolling.
* Content is intended to be put in a binding that consists of the name, logo,
  website and a link to the company's vacancies.
* Images that can be found in such a description are adapted for retina
  displays.
* Font size is no less than 12px, line spacing is no less than 16px.

The value can be null, if the company doesn't have an individual description.

`vacancies_url` – a link to the search results of the company's vacancies.

`logo_urls` – company logo images of different sizes.

`original` – an unedited logo, which can be big in size. If the originally
uploaded logo is smaller than 240px and/or 90px in its smaller side,
the corresponding keys will have links to the original images. Object
can be null, if the company hasn't uploaded its logo. The client should foresee
the possibility of the logo missing in the indicated link (response with the
`404 Not Found` code).

`type` – company type (direct employer, employment agency, etc). Possible values
are described in the [directory collection](dictionaries.md) under the
employer_type key.

`area` — employer's region.

`trusted` - boolean flag indicates that the company passed website verification.

Example: [https://api.hh.ru/employers/1455?locale=EN](https://api.hh.ru/employers/1455?locale=EN)

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` – the employer is not found.
