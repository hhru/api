# Negotiations (responses/invitations) for employers

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access)

*Negotiations documentation for the applicant is available in the [separate article](negotiations.md).*

* [Model of work, terms and procedures](#model)
* [General description of the process of working with responses/invitations](#flow)
* [Collections and employers' statuses of responses/invitations](#collections)
* [List of responses/invitation](#negotiations-list)
* [View the response/invitation](#get-negotiation)
* [View the list of messages in the response/invitation](#get-messages)
* [Sending a message in the response/invitation](#add-messages)
* [Inviting an applicant for a vacancy](#add-invite)
* [Actions regarding a response/invitation (status change)](#actions)
* [Viewing preferred options for sorting responses](#get-preference-order)
* [Changing preferred options for sorting responses](#update-preference-order)
* [Mark responses as read](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/post-negotiations-topics-read) 


<a name="model"></a>
## Model of work, terms and procedures

Responses and invitations correspond to the model that is expressed in the requests and
API responses. If the application uses the model properly, then changes
in the business logic of responses and invitations will not cause the need for modification or
correction.

Responses and invitations use the following terms:

* *response* is an object generated at the initiative of the applicant as a response to a job.
A response always involves the use of one resume to apply for one job.

* *invitation* is an object generated at the initiative of the employer as an invitation to apply
for a job. An invitation always implies the use of one resume to apply for one job.

Except for the object generation process, the rest of the work with the response or invitation is
the same.

* <a name="term-collection"></a> *collection* is a set of responses/invitations,
  which are combined according to certain criteria. Collections are used when your
  application should **display** a list of responses/invitations. You should not
  rely on the fact that at certain stages of processing a response/invitation,
  your application will use the known collections, as this logic may vary.

* <a name="term-state"></a> *applicant's response/invitation status* is the
  response/invitation status that is **displayed for the applicant**. The possible values
  are available [in the `negotiations_state` directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) and
  do not depend on the job in response/invitation.

* <a name="term-employer-state"></a> *employer's response/invitation status* is the
  response/invitation status that is displayed for the employer. It may differ from the
  applicant's status. The list of possible statuses
  **depends on the job and employer**, therefore this list
  [must be requested](#states), while passing the desired job. 

* <a name="term-action"></a> *action regarding the response/invitation* is the action that
  can be performed in relation to a response/invitation. As a result of the action,
  the employer's or the applicant's response/invitation status can
  change or stay the same.

Do not confuse *action*, *collection*, and *status*, because they may be similar,
but they are designed for different purposes.


<a name="flow"></a>
## General description of the process of working with responses/invitations

All work with responses/invitations takes place within the framework of a
**single selected job**. Even the same employer can have jobs
with different rules for working with responses/invitations.

First, you need to get a list of
[collections and employer's statuses](#collections). Then you should use collections
to **get the lists of responses/invitations**. Prompt the user
to choose which collection to get. To get all the
responses/invitations, you need to request all the collections sequentially. The list of
statuses is used only as a directory.

To **create an invitation**, you should request employer's jobs
applicable to the selected resume. You can get this information in the 
[employer job list](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-active-vacancy-list), which also
contains the required parameters (the "arguments" key) and the status of the created
response (the "resulting_employer_state" key). Different employers and different
jobs may have different rules and statuses for added responses. Each
*job + resume* pair can have only one response/invitation.

To create an invitation, an employer must have activated access to the database of
resumes. Employers do not need such access to work with an existing response/invitation. This
allows them to process responses to jobs even without access to the resume database.

If you need to **take an action** with respect to a response/invitation,
please refer to the list of actions that will be available in the
[list (collection) of responses/invitations](#negotiations-list) and in the
[individual response/invitation](#get-negotiation). If the action
changes the status of a response/invitation, it will be explicitly specified in the
"resulting_employer_state" key. Not all actions lead to a status change.

After inviting the applicant, you can start a
[free conversation](#get-messages). You will be able to
[send messages](#add-messages) and receive responses from the applicant.
If necessary, you
[can disable](https://api.hh.ru/openapi/en/redoc#tag/Vacancies/operation/get-vacancy) conversations for a specific job (the `allow_messages` field).

Take one of the following actions to make sure that the application registers as viewed by the employer:
* request a list of messages using the URL received upon request [a list (collection) of applications/invitations](#negotiations-list) 
or [individual application/invitation](#get-negotiation)
* [request message](#get-messages) by response
* request resume using the URL received upon request [a list (collection) of applications/invitations](#negotiations-list) 
or [individual response/invitation](#get-negotiation)  
* call [the specific method](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/post-negotiations-topics-read) to set certain responses as read

<a name="states"></a>
<a name="collections"></a>
## Collections and employers' statuses of responses/invitations

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-negotiations)

<a name="negotiations-list"></a>
## List of responses/invitation

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-collection-negotiations-list)

<a name="get-negotiation"></a>
## View the response/invitation

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-negotiation-item)

## View the list of messages in the response/invitation

<a name="get-messages"></a>
>‼️ Please note that the methods for handling response/invitation messages on behalf of the [applicant](negotiations.md#get_messages) and
> [employer manager](employer_negotiations.md#get-messages) are deprecated and the new chat capabilities will not be supported in these methods. As such, correspondence may not display correctly.

Messages contained in the response/invitation can be made as:

* cover letter left by the applicant upon response to the vacancy
* text sent by the employer upon inviting for the vacancy, for the interview
  or upon rejection
* free negotiation messages between the applicant and the employer

### Request

```
GET /negotiations/{nid}/messages
```

where `nid` is the response/invitation ID.

Usually is taken from key `messages_url` in
[the list of responses/invitations](#negotiations-list) or in
[view the response/invitation](#get-negotiation).

Parameters:

Name | Required | Possible values | Description
---- | -------- | --------------- | -----------
with_text_only | no | true/false | Return only messages with non empty `text` field, by default: `false`, so all messages will be returned

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
   "found": 2,
   "pages": 1,
   "page": 0,
   "per_page": 20,
   "items": [
       {
           "id": "123",
           "text": "You are invited for the vacancy...",
           "created_at": "2015-05-15T19:23:35+0300",
           "author": {
               "participant_type": "employer"
           },
           "viewed_by_opponent": true,
           "viewed_by_me": true,
           "state": {
               "id": "invitation",
               "name": "Invitation"
           },
           "address": {
                "building": "10",
                "city": "Moscow",
                "description": "Turn right following the sign",
                "lat": 35.0,
                "lng": 30.0,
                "metro": {
                    "lat": 55.789704,
                    "line_id": "2",
                    "line_name": "Zamoskvoretskaya",
                    "lng": 37.558212,
                    "station_id": "2.34",
                    "station_name": "Dinamo"
                },
                "metro_stations": [
                    {
                        "lat": 55.789704,
                        "line_id": "2",
                        "line_name": "Zamoskvoretskaya",
                        "lng": 37.558212,
                        "station_id": "2.34",
                        "station_name": "Dinamo"
                    }
                ],
                "street": "ul. Dinamo"
            },
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
            ]
       },
       {
           "id": "321",
           "text": "Great! I will be glad to meet you for an interview...",
           "created_at": "2015-05-15T19:23:35+0300",
           "author": {
               "participant_type": "applicant"
           },
           "viewed_by_me": false,
           "viewed_by_opponent": true,
           "state": {
               "id": "text",
               "name": "Text"
           },
           "address": null
       }
   ]
}
```

where:

Name | Type | Description
--- | --- | --------
found | number | Number of messages in negotiation ( ≥ 0 )
pages | number | Number of pages with messages ( ≥ 1 )
per_page | number | Number of messages per page ( > 0 )
page | number | Number of the current page ( ≥ 0 )

Messages are sorted in the following order: the oldest message is first and the newest last.

<a name="negotiations-message-item"></a>
The `items` entity contains message data:

Name | Type | Description
--- | --- | --------
id | string | Message ID
viewed_by_me| logical | Whether the message was read by the viewer (for messages sent by employer the value is always `true`)
viewed_by_opponent| logical | Whether the message was read by the applicant (for messages sent by applicant the value is always `true`)
created_at | string | Message creation date and time
text| string, null | Message text. `null` can be displayed if the applicant didn't attach the cover letter to the response.
state | object | Current state of the application. Possible values are listed in the [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) reference, section `negotiations_state`
author| object | Who is the message author
author.participant_type| string | Message author role. Possible values are listed in the [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) reference, section `negotiations_participant_type`
address| object, null | [Address](./address.md) linked to the response/invitation
assessments| array | [assessment tools](assessment.md) linked to the message

If response/invitation doesn't exist or negotiation not available to the current user,
`404 Not Found` response will be returned.


<a name="add-messages"></a>
## Sending a message in the response/invitation

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/send-negotiation-message)

<a name="add-invite"></a>
## Inviting an applicant for a vacancy

The invitation defines the relationship between the employer's job and the applicant's resume
at the employer's initiative. To perform a request, you need to know the initial
status for this "job + resume" pair. For more information, please see
[general description of the process of working with responses/invitations](#flow).

### Request

```
POST /negotiations/{state}
```

where `state` – is the initial state of the invitation

You can get the invitation parameters from the
[action list](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-active-vacancy-list).

Parameters should be sent in standard format
`application/x-www-form-urlencoded`.


### Response

Successful server response is returned with `201 Created` code, does not have a body and contains
title `Location` indicating created invitation:

```
HTTP/1.1 201 Created

Location: /negotiations/321
```


### Errors

* `400 Bad Request` – error in the request parameters.
* `403 Forbidden` – invitation is impossible.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).

For example:

* `already_invited` – if the response between the sent CV and the vacancy
  already exists
* `resume_not_found` – if the sent CV was hidden or deleted
* `invalid_vacancy` – if the sent vacancy was archived or hidden
* `limit_exceeded` – if the manager's number of invitations per day limit
  was exceeded
* `application_denied` – general invitation denial error
  if additional information is unavailable
* `address_not_found` – if the sent address does not exist or belongs to
  another employer
* `not_enough_purchased_services` – the paid services are insufficient, usually
  [CV database services](https://hh.ru/price#dbaccess)


<a name="actions"></a>
<a name="put-on-hold"></a>
<a name="invite"></a>
<a name="discard"></a>
## Response/invitation actions (status change)

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/put-negotiations-collection-to-next-state)

<a name="get-preference-order"></a>
## Viewing preferred options for sorting responses

> !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-pref-negotiations-order)

<a name="update-preference-order"></a>
## Changing preferred options for sorting responses

> !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/put-pref-negotiations-order)
