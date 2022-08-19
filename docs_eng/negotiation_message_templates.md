# Message texts

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](/docs_eng/payable/employer_payable_methods.md)

An employer can obtain template texts for use in vacancy invitations sent to applicants or [actions on responses/invitations](employer_negotiations.md#actions).

The number of available templates depends on specific response/invitation or vacancy and their statuses. Currently, the following templates are available:

Name| Description
----|---------
invite| text for invitation of the applicant for a vacancy
invite_after_response| text [for invitation after the applicant's response](employer_negotiations.md#invite)
discard_after_response| text for [rejection after the response](employer_negotiations.md#discard)
discard_after_interview| text for [rejection after invitation of the applicant for an interview](employer_negotiations.md#discard)

In the future, the list of templates may be extended.


<a name="request"></a>
## Request

Rather than construct the url on your own, it is recommended to use the url included in the `templates` object in the
[list of responses/invitations](employer_negotiations.md#negotiations-list) and suitable vacancies:

```json
{
    "templates": [
        {
            "url": "https://api.hh.ru/message_templates/invite?resume_id=0123456789abcdef&vacancy_id=123456",
            "id": "invite"
        }
    ]
}
```

```
GET /message_templates/{template}?topic_id={topic_id}
GET /message_templates/{template}?vacancy_id={vacancy_id}&resume_id={resume_id}
```

where `template` is the name of the template from the list above.

Parameters:

Name| Description
----|---------
topic_id| ID of the existing response/invitation. Simultaneous sending with other parameters is not allowed.
vacancy_id| ID of the vacancy for invitation. Requires sending of the `resume_id` parameter.
resume_id| ID of the CV for invitation to the vacancy. Requires sending of the `vacancy_id` parameter.

In case the conflicting parameters are sent – `topic_id` with `resume_id` or `vacancy_id`, or no parameters are sent at all – an error will be returned.


<a name="response"></a>
## Response

Successful server response is returned with `200 OK` code and contains

```json
{
    "mail": {
        "text": "Hello Ivan Ivanovich! Thank you for your response to the vacancy... "
    }
}
```

Name| Type| Description
----|-----|---------
text| String| Text of the message sent to the applicant by email when inviting/rejecting the applicant. It may vary depending on the vacancy type (e.g. for anonymous vacancy).


<a name="errors"></a>
## Errors

* `404 Not Found` – if a non-existent template is used.
* `403 Forbidden` – the request is fulfilled anonymously, with authorization of the applicant or the employer without enabled CV database access service.
* `400 Bad Request` – invalid request parameters.

In addition to an HTTP code, the server can return [error reasons](errors.md#general-errors).

In particular:

Code| type| value| Reason
----|------|-------|--------
400| bad_argument| topic_id| <ul><li>ID of the non-existent response/invitation was sent; ID of the response/invitation of another employer was sent or the response/invitation which the current manager doesn't have access to</li><li>vacancy from the response/invitation was archived</li><li>the CV from the response/invitation was hidden/deleted</li></ul>
400| bad_argument| resume_id| ID sent is the ID of a non-existent CV or a CV that is inaccessible for the employer
400| bad_argument| vacancy_id| ID sent is the ID of a non-existent, hidden or archived vacancy, a vacancy of another employer or a vacancy that is inaccessible for the current manager
