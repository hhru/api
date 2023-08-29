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

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/operation/get-vacancies)

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
    "archived": "false",
    "show_logo_in_search": true
}
```

Here:

Name| Type| Description
--- | --- | -----------
 id | string| Vacancy identifier
 premium | logical | Whether it is a premium vacancy
 address | object, null | [vacancy address](address.md)
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

Please see the [full vacancy](https://api.hh.ru/openapi/en/redoc#tag/Vacancies/operation/get-vacancy) for a description of the fields.

`url` and `alternate_url` can have the `null` meaning if the detailed
information on the vacancy is unavailable (for instance, when the vacancy has
been deleted)
