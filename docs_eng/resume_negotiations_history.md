# History of responses/invitations for a resume

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](/docs_eng/payable/employer_payable_methods.md)

Only employers can get the history of responses/invitations. The list will contain the last actions
with the resumes specified: no more than 30 jobs of this employer, and no more than 10 status changes in responses/invitations
for each of these jobs.


### Request

You do not need to construct the URL of the request manually, you need to get it
from the [`negotiations_history` field in the resume](resumes.md#negotiations-history-field).

`GET /resumes/{resume_id}/negotiations_history`,

where `resume_id` – resume ID.

<a name="response"></a>
### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "vacancies": [
        {
            "id": "321",
            "name": "Test vacancy",
            "url": "https://api.hh.ru/vacancies/321",
            "archived": false,
            "can_edit": true,
            "items": [
                {
                    "employer_state": {
                        "id": "offer",
                        "name": "Offer"
                    },
                    "created_at": "2017-01-30T15:06:47+0300",
                    "with_message": true
                }
            ],
            "negotiations_url": "https://api.hh.ru/negotiations/123",
            "messages_url": "https://api.hh.ru/negotiations/123/messages"
        }
    ]
}
```

Each of the `vacancies[]` elements has the following parameters specified:

Name | Type | Description
-----|-----|---------
id | number | unique job ID
name | string | job name
url | string | the URL to perform a GET request to obtain the [information on the job](vacancies.md#item)
archived | logical | a flag that indicates that the job is in the archive
can_edit | logical | a flag that indicates that the manager can edit job data and work with information on the responses/invitations for this job
items | list | a list of the latest changes in the statuses of responses/invitations for the specified resume and job
items[].employer_state.id | string | a unique identifier of the [response/invitation status](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/paths/~1dictionaries/get)
items[].employer_state.name | string | response/invitation status name
items[].created_at | string (date) | date of the response/invitation status change
items[].with_message | logical | a flag that indicates that a message was sent to the applicant when the response/invitation status was changed
negotiations_url | string | the URL to perform a GET request to obtain the [information on the response/invitation](employer_negotiations.md#get-negotiation). If `can_edit` is `false`, the field value should be ignored.
messages_url | string | the URL to perform a GET request to obtain the [list of messages for the response/invitation](employer_negotiations.md#get-messages). If `can_edit` is `false`, the field value should be ignored.

### Errors

* `403 Forbidden` — The user is not an employer.
* `404 Not Found` — The resume does not exist or is not available.
