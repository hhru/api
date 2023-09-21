# CV

* [List of CVs for current user](#mine)
* [View a CV](#item)
  * [Additional fields for the resume publisher](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
  * [Resume-related paid services for the resume publisher](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
  * [Additional fields for the employer](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
  * [Resume-related paid services for the resume publisher (field paid_services)](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
* [Creating a resume](#create_edit)
* [Editing a resume](#create_edit)
* [Publishing a resume](#publish)
* [Information on a resume's status and readiness for publication](#status-and-publication)
* [Cloning a resume](#clone)
* [Deleting a resume](#delete)
* [Checking for the ability to create a resume](#availability)
* [Conditions to fill in the fields of a resume](#conditions)
  * [Conditions to fill in the fields of a new resume](#init-conditions)
* [Resume abstract](#resume-nano)
* [Resume summary](#resume-short)
* [Resume download links](#download-links)
* [Resume viewing history](#views)
* [Searching for jobs similar to a resume](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume)
* [CV hidden fields](#hidden-fields)


<a name="mine"></a>
## List of CVs for current user

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-mine-resumes)

<a name="item"></a>
## View a CV

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](/docs_eng/payable/employer_payable_methods.md)

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume)

<a name="create"></a>
## Creating a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/create-resume)

<a name="edit"></a>
## Editing a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/edit-resume)

<a name="publish"></a>
## Publishing a resume

`POST /resumes/{resume_id}/publish`

The resume can be used as soon as it is first published.

Subsequent publications will update the renewal date of the resume. `next_publish_at` key
in the resume indicates when the resume can be updated.


### Response

A successful response contains a code `204 No Content` and is body-less.


### Errors

* `429 Too Many Requests` - If the update is not available yet.
* `400 Bad Request` - If publication/extension is not possible. The possible causes are:
  * Mandatory fields are empty (to understand what exactly is not filled in, you can call the url [get resume](#item) and look at the `mandatory` field),
  * The fields have not been not edited after banning by a moderator,
  * The resume is being checked by a moderator.
* `403 Forbidden` - If the resume cannot be published because of a lack of necessary privileges (for example, for an employer).


<a name="status-and-publication"></a>
## Information on a resume's status and readiness for publication

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-information/operation/get-resume-status)

<a name="clone"></a>
## Cloning a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/create-resume)

<a name="delete"></a>
## Deleting a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/delete-resume)

<a name="availability"></a>
## Checking for the ability to create a resume

### Request

```
GET /resumes/creation_availability
```

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "is_creation_available": true,
    "max": 20,
    "created": 2,
    "remaining": 18
}
```

where:

Name | Type | Description
---- | ------ | ---
is_creation_available  | boolean | This is a flag that indicates whether the creation of new resumes is available to this user
max | number | Maximum number of resumes
created  | number | The number of previously created resumes
remaining  | number | The number of resumes that can be created

### Errors

* `403 Forbidden` – The request is not from the applicant.

<a name="conditions"></a>
## Conditions to fill in the fields of a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-resume-conditions)

<a name="init-conditions"></a>
## Conditions to fill in the fields of a new resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-new-resume-conditions)

<a name="views"></a>
## Resume viewing history

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume-view-history)

<a name="similar"></a>
## Searching for jobs similar to a resume

The information is available only to the resume publisher.

### Request

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume)

<a name="hidden-fields"></a>
## CV hidden fields

The `hidden_fields` field contains a list of search fields hidden by the applicant. Hidden fields are replaced by `null`. The CV author is provided with relevant data.

* `names_and_photo` enters `null` instead of the values of the `first_name`, `last_name`, `middle_name` and `photo` fields
* `phones`  enters `null` instead of the value of the `contact[].value` field, when `contact[].type` contains `cell,` `work,` or `home`
* `email`  enters `null` instead of the value of the `contact[].value` field, when `contact[].type` contains `email`
* `other_contacts` enters `null` instead of the value of the `site[].url` field
* `experience` enters `null` instead of the values of the `experience[].company`, `experience[].company_id`, `experience[].company_url`, `experience[].employer` fileds; enters an empty list instead of the value of the `recommendation` field

