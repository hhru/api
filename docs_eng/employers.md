# Employers/companies

* [сompany search](#search)
* [employer/company](#item)

<a name="search"></a>
## Company search

`GET /employers` will return the company search results.

Additional available parameters:

* text – text field, sent value is searched in the name and description of the company.
* area – employer ID, multiple parameter. You can find region ID in the [directory of regions](areas.md)
* type – type of employer, multiple parameter. Allowed values — keys in the [directory `employer_type`](dictionaries.md)
* only_with_vacancies – return only employers who have open vacancies at the moment (`true`) or all employers (`false`).
                        Default — `false`.
* page – number of page with employers (counted up from 0, default is 0)
* per_page – number of elements on page (default — 20, max value - 100)

For page parameters (`page`, `per_page`) there is a limit:
the depth of returned results cannot exceed 2000. For example, a request `per_page=10&page=199` 
(search results from 1991 to 2000 companies) is possible, but a request with `per_page=10&page=200` 
will return an error (results from 2001 to 2010 companies).

### Response

Successful server response is returned with `200 OK` code and contains:

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

Name     | Type             | Description
---------|------------------|--------------------------------------------------------
per_page | number           | number of elements shown per page
page     | number           | number of shown page
pages    | number           | number of pages with data
found    | number           | number of employers found for the selected search criteria
items    | array of objects | found employers (maximum per_page elements)

Each element of the items array contains a brief description of the employer
with an additional value for the number of open vacancies.

 Name           | Type         | Description
----------------|--------------|-------------------------------------------------------
id              | string       | employer ID
name            | string       | employer name
url             | string       | url for full description of the employer
alternate_url   | string       | link to employer description on the website
vacancies_url   | string       | url for search results with vacancies of this company
open_vacancies  | number       | number of employer's open vacancies
logo_urls       | object, null | [company logos](#logo-urls)

### Errors

* `400 Bad Request` – error in the request parameters. The response body can contain details of the field with error.

<a name="item"></a>
## Employer/company

`GET /employers/{employer_id}` returns the data about the company with a link
to the company's vacancies.

### Response

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
    "insider_interviews": [
        {
            "url": "https://hh.ru/interview/12345?employerId=1455",
            "id": "12345",
            "title": "The best of the best"
        },
        {
            "url": "https://hh.ru/interview/54321?employerId=1455",
            "id": "54321",
            "title": "Success story"
        }
    ],
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
    "trusted": true,
    "relations": []
}
```

Name | Type | Description
---- | ---- | -----------
id | string | employer ID
name | string | employer name
type | string, null | type of company (immediate employer, HR agency, etc). Possible values are described in [collection of directories](dictionaries.md) under the key `employer_type`. `null` is possible if the company type is hidden.
site_url | string | link to employer website
description | string, null | a string with the HTML code (`<script/>` and `<style/>` presence is not possible)
branded_description | string, null | [branded description](#branded-description) as a string with the HTML code
vacancies_url | string | a link to the search results of the company's vacancies
trusted | boolean | the flag indicates that [the company is verified by the website](https://feedback.hh.ru/article/details/id/5951)
alternate_url | string | link to employer description on the website
insider_interviews | array | interview list or blank list if there are no interviews
insider_interviews[].id | string | interview ID
insider_interviews[].title | string | interview title
insider_interviews[].url | string | address of the page containing the interview
logo_urls | object, null | [company logos](#logo-urls)
area | string | region of employer
area.id | string | region ID [from dictionary](areas.md)
area.name | string | region name
area.url | string | link to information about the region
relations | array | if the employer is blacklisted, it will return `['blacklisted']` else `[]`

<a name="branded-description"></a>
#### Branded description

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

<a name="logo-urls"></a>
#### Logo images

`logo_urls` – company logo images of different sizes.

`original` – an unedited logo, which can be big in size. If the originally
uploaded logo is smaller than 240px and/or 90px in its smaller side,
the corresponding keys will have links to the original images. Object
can be null, if the company hasn't uploaded its logo. The client should foresee
the possibility of the logo missing in the indicated link (response with the
`404 Not Found` code).
