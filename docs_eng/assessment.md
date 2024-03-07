# Assessment tools

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Assessment tools require [paid access](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access) for the employer.

Assessment tools are tests and questionnaires designed to be taken by
applicants.

Information about them may be present in messages sent by an
[employer](employer_negotiations.md#get-messages) to an
[applicant](negotiations.md#get_messages) within the responses/invitations.


The object looks as follows:

```json
{
    "id": "123",
    "name": "Dynamic numerical ability test",
    "actions": [
        {
            "id": "proceed",
            "name": "Go to testing",
            "enabled": true,
            "alternate_url": "https://hh.ru/applicant/assessment/123"
        }
    ]
}
```

where:

 Name| Type| Description
 --- | --- | ---
 id| string| Tool unique ID
 name| string| Tool name
 actions| array| Array of possible [actions on the tool](#actions)


<a name="actions"></a>
## Action on the tool

Depending on the assessment tool state, specific actions on it can be
available or not.

Available action example:

```json
{
    "id": "proceed",
    "name": "Go to testing",
    "enabled": true,
    "alternate_url": "https://hh.ru/applicant/assessment/123"
}
```

Unavailable action example:

```json
{
    "id": "proceed",
    "name": "Go to testing",
    "enabled": false,
    "disable_reason": "Testing completed"
}
```


where:

 Name| Type| Description
 --- | --- | ---
 id| string| Action type
 name| string| Action description
 enabled| boolean| Whether the action is available
 alternate_url| string| Link to a website clicking on which will initiate the action
 disable_reason| string| Explanation why the action is unavailable
