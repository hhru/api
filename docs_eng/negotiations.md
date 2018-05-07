# Negotiations (responses/invitations) for applicants

_Negotiations documentation for the employer is available in the [separate article](employer_negotiations.md)._

Using the website, applicants choose vacancies. In order to contact an employer
for vacancy details, an applicant can respond to the chosen vacancy. An
employer, on his part, can offer an applicant to consider a vacancy (invitation).

For these purposes, there are special entities – responses and invitations.
They can include a vacancy, CV and negotiations with employer; at any given time
such entities have one of the states. Transition between the states is
accompanied by appearance of messages with optional text descriptions and other
fields. Messages with `null` status do not transit the whole respond to a new
state.

* [Receiving the list of responses](#get_negotiations)
* [Receiving the list of active responses](#get_negotiations_active)
* [Respond to the vacancy](#post_negotiation)
* [View the response/invitation](#get_negotiation)
* [Hide the response](#hide_message)
* [View the list of messages in the response](#get_messages)
* [Sending new message](#send_message)
* [Edit a message in the response](#edit_message)


<a name="get_negotiations"></a>
## Receiving the list of responses

### Request

```
GET /negotiations
```

Parameters:

 Name| Required| Description
 --- | --- | ---
 page| no| Page number, default: 0
 per_page| no| Number of elements displayed per page, default is 20.
 order_by| no| The field to sort the displayed data by. Possible values: `updated_at`, `created_at`. Default: `updated_at`
 order| no| Sort order. Possible values: `asc`, `desc`. Default: `desc`
 vacancy_id| no| filter by a vacancy id

### Response

```javascript
{
    "found": 1,
    "pages": 1,
    "per_page": 20,
    "page": 0,
    "items": [
        {
            "id": "123",
            "state": {
                "id": "invitation",
                "name": "Invitation"
            },
            "hidden": false,
            "created_at": "2013-10-05T19:51:38+0400",
            "updated_at": "2013-10-07T18:30:57+0400",
            "url": "https://api.hh.ru/negotiations/123",
            "resume": {},
            "vacancy": {},
            "has_updates": true,
            "viewed_by_opponent": true
        }
        // , .....
    ]
}
```

where:

 Name| Type| Description
 --- | --- | ---
 found| number| Number of responses found ( ≥ 0 )
 pages| number| Number of pages with responses ( ≥ 1 )
 per_page| number| Number of elements per page ( > 0 )
 page| number| Number of the current page ( ≥ 0 )

The `items` entity contains response data:

 Name| Type| Description
 --- | --- | ---
 id| string| Response ID
 state| object| Current state of the application. Allowed values are listed in the [/dictionaries](./dictionaries.md) reference, section ```negotiations_state``` 
 hidden| logical| Whether the current response is hidden (True – the response is hidden, False – the response is active)
 created_at| string| Response creation date and time
 updated_at| string| Response update date and time
 url| string| Link to the full response
 resume| object, null| [CV short view](resumes.md#resume-nano)
 vacancy| object, null| [Vacancy short view](vacancies.md#nano)
 has_updates| logical| Whether the response includes updates that require attention. The flag is reset by various actions on the response, e.g. [messages list view](#get_messages).
 viewed_by_opponent| logical| Whether the response was viewed by the employer

Within the vacancy object, keys `url` and `alternate_url` can be `null` if the
vacancy is unavailable (deleted).

### Errors

* `403 Forbidden` – authorization is failed.


<a name="get_negotiations_active"></a>
## Receiving the list of active responses

### Request

```
GET /negotiations/active
```

Optional parameters and the response are the same as in the
[list of responses](#get_negotiations)

### Errors

* `403 Forbidden` – authorization is failed.


<a name="post_negotiation"></a>
## Respond to the vacancy

In order to know with which CVs the specific vacancy can be responded to, one
can use the [list of suitable CVs](suitable_resumes.md).

### Request

```
POST /negotiations
```
Parameters

 Name| Required| Description
  --- | --- | ---
 vacancy_id| yes| ID of the vacancy that was responded
 resume_id| yes| ID of the CV an applicant responded with
 message| yes| Response cover letter. Is required if the vacancy specifies the cover letter as mandatory


### Response

If successful, the status `201 Created` will be returned and the response
`Location` header will contain a link to the response created (except for
`direct` see below)

```
HTTP/1.1 201 Created
...
Location: /negotiations/123
...
```

For vacancies with `direct` type, a response with `303 See Other` code will be
returned.

```
HTTP/1.1 303 See Other
...
Location: http://example.com/respond/vacancy
...
```

Vacancies with `direct` type are vacancies with direct responses. Such vacancies
have non-empty `response_url` – an external url of the employer website that is
returned in the `Location` header at the response attempt. Use `response_url` to
offer a user to respond to the vacancy via the employer website instead of the
standard response mechanism.


### Errors

* `400 Bad Request` – indicated vacancy or CV doesn't exist;
  or you need to pass the test or fill in the cover letter to respond;
  or employer closed the option to respond to the vacancy;
  or number of responses per day is exceeded for the user.
* `403 Forbidden` – authorization is failed.
* `403 Forbidden` – you can't respond to indicated vacancy because you
  don't have access to it, responded to the vacancy beforehand or
  display visibility settings of selected CV prevent from responding to
  vacancy.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).


<a name="get_negotiation"></a>
## View the response/invitation


### Request

```
GET /negotiations/{nid}
```
where nid is the response ID.


### Response

The object returned is identical to a separate response received in
[the list of responses](#get_negotiations), excl. `messaging_status` field.

 Name | Type | Description
 --- | --- | ---
 messaging_status | string | Current negotiation status. Possible values are provided in the [`messaging_status` reference guide](./dictionaries.md).

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - negotiation is not found.

<a name="hide_message"></a>
## Hide the response
To hide the response, use the following request:

```
DELETE /negotiations/active/{nid}
```

where:

 * nid is the response ID

HTTP status `204 No Content` will be returned

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - negotiation is not found.


<a name="get_messages"></a>
## View the list of messages in the response

### Request

```
GET /negotiations/{nid}/messages
```

where:

 * nid is the response ID

Optional parameters

 Name| Type| Required| Description
 --- | --- | --- | ---
 page| number| no| Page number, default is 0
 per_page| number| no| Number of elements per page, default is 20


### Response

```json
{
    "found": 1,
    "pages": 1,
    "per_page": 20,
    "page": 0,
    "items": [
        {
            "id": "123",
            "viewed_by_me": true,
            "viewed_by_opponent": true,
            "created_at": "2013-10-07T18:30:57+0400",
            "text": "A major bank invites you for a job with salary that Arab sheikhs can only dream of",
            "state": {
                "id": "invitation",
                "name": "Invitation"
            },
            "author": {
                "participant_type": "employer"
            },
            "address": null,
            "assessments": [
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
            ],
            "editable": false
        },
        {
            "id": "124",
            "viewed_by_me": true,
            "viewed_by_opponent": false,
            "created_at": "2013-10-08T10:12:23+0400",
            "text": "Give me a camel and a horse!",
            "state": {
                "id": "text",
                "name": "Text"
            },
            "author": {
                "participant_type": "applicant"
            },
            "address": null,
            "editable": false
        }
    ]
}
```

where:

 Name| Type| Description
 --- | --- | ---
 found| number| Number of messages found
 pages| number| Number of pages with messages found
 per_page| number| Number of elements per page
 page| number| Current page number (starts with 0)
 items| array| Message array, see below

 Individual message has the following structure:

 Name| Type| Description
 --- | --- | ---
 id| string| Message ID
 viewed_by_me| logical| Whether the message was read by the viewer (for messages sent by applicants, the value is always `true`)
 viewed_by_opponent| logical| Whether the message was read by the employer (for messages sent by employers, the value is always `true`)
 editable| logical| Whether the message text can be edited
 created_at| string| Message creation date and time
 text| string| Message text
 state| object| Current state of the application. Possible values are listed in the [/dictionaries](./dictionaries.md) reference, section `negotiations_state`
 author| object| Who is the message author
 author.participant_type| string| Message author role. Possible values are listed in the [/dictionaries](./dictionaries.md) reference, section `negotiations_participant_type`
 address| object, null| [Address](./address.md) linked to the response/invitation
 assessments| array| [assessment tools](assessment.md) linked to the message
 
### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - response/invitation doesn't exist or negotiation not available to the current user.


<a name="send_message"></a>
## Sending new message

You can send new message to employer only after the employer
invited the applicant for a vacancy. Also, messages can be sent if there is a rejection
after the interview. Negotiation is unavailable if the vacancy is archived or
the applicant deleted the CV. Employer can also disable the negotiation for
the vacation manually.


### Request

```
POST /negotiations/{nid}/messages
```

where:

 * nid is the response ID

Parameters

Name | Required | Description
--- | ------------ | --------
message | yes | Message text


### Response

Successful response is returned with `201 Created` code and contains added
comment:

```json
{
    "id": "124",
    "viewed_by_me": true,
    "viewed_by_opponent": false,
    "created_at": "2013-10-08T10:12:23+0400",
    "text": "Give me a camel and a horse!",
    "state": {
        "id": "text",
        "name": "Text"
    },
    "author": {
        "participant_type": "applicant"
    },
    "address": null,
    "editable": false
}
```

### Errors

* `404 Not Found` – response with this ID doesn't exist
* `403 Forbidden` – authorization is failed.
* `403 Forbidden` – respond is prohibited.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).


<a name="edit_message"></a>
## Edit messages in the response

Under certain conditions, the message text can be edited after it is sent. In
order to allow message editing, use the flag `editable`.

> At the moment, editing is available for response message only,
> and such message should not be read by the other party, the vacancy should be
> active (not archived) and CV should not be deleted. However, these conditions
> are subject to change.


### Request

```
PUT /negotiations/{nid}/messages/{mid}
```

where:

 * nid is the response ID
 * mid is the response message ID

Parameters

 Name | Required | Description
 --- | --- | ---
 message | yes | Message text


### Response

In case of successful message text update the HTTP status
`204 No Content` is returned.


### Errors

* `403 Forbidden` – authorization is failed.
* `403 Forbidden` – editing is prohibited (For example, if receiving party has already read the message).
* `404 Not Found` – the message is not found.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).
