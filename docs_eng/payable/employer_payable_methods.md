# Paid access to some API methods for employers

Employers have had to pay for some HH API  methods since July 16, 2018.

Paid methods are marked with the following label in the [Table of Contents](/docs_eng/README.md#headhunter-api)
<img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

Please contact your personal manager to buy access to paid methods for employers.

Please note that where the app is used by several employer accounts (employer_id), each employer account has to have access to the paid API methods.
There is a [special method](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/paths/~1employers~1{employer_id}~1services~1payable_api_actions~1active/get) you can use to verify information about the enabled employer services.

If you request a paid method without purchasing access, you'll get this [error](/docs_eng/errors.md#employer_payable_methods) `403 Forbidden`.

## Check access to a paid method

The employer has to authorize before lodging the request; otherwise, an error will return.

### Request

```
GET /employers/{employer_id}/managers/{manager_id}/method_access
```

where:
* `employer_id` is the employer's ID, which you can find in [current user information](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/paths/~1me/get).
* `manager_id` is the manager's ID, which you can find in [current user information](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/paths/~1me/get).

All existing method groups will return complete with their access details.

The following groups currently exist:
1. Availability of access to the methods:
    * [Resume viewing](/docs_eng/resumes.md#item)
    * [Response management](/docs_eng/employer_negotiations.md)
    * [Correspondence](/docs_eng/employer_negotiations.md#get-messages)
2. Availability of access to the methods:
    * [Resume search](/docs_eng/resumes_search.md)
    * [Saved resume searches](https://api.hh.ru/openapi/en/redoc#tag/Resume-search/paths/~1saved_searches~1resumes/get)
3. Availability of access to the [viewing of resumes](/docs_eng/resumes.md#item) that have a response or invite
4. Availability of access to the [viewing of resumes](/docs_eng/resumes.md#item) for resumes found via [database search](/docs_eng/resumes_search.md)

>!! Note that there have been changes in access to contact details. Please read the information on [contact-by-contact resume access](/docs_eng/payable/resume.md) carefully

### Response

A successful response contains the code `200 OK` and this body:

```json
{
    "items": [
        {
            "id": "3",
            "description": "Access to viewing a resume that has a response or invite",
            "access": {
                "has_access": true
            }
        },
        {
            "id": "4",
            "description": "Availability of resume viewing access",
            "access": {
                "has_access": false
            }
        },
        ...
    ]
}
```

Each element of the items array contains the description of a group of methods

Name | Type | Description
--- | --- | --------
id | string | method group ID
description | string | method group description
access.has_access | boolean | whether access is available to the method group

### Errors

* `403 Forbidden` – if the current user is not the employer.
* `404 Not Found` – if the named employer or manager was not found.
