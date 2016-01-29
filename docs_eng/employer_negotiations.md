# Messaging (applications/invitations) for the employer

*Documentation on messaging for the applicant is available in the [separate article*](negotiations.md).*

* [Application/invitation collections](#collections)
* [Application/invitation list](#negotiations-list)
* [Viewing an application/invitation](#get-negotiation)
* [Viewing a message list in an application/invitation](#get-messages)
* [Sending a message in the response/invitation](#add-messages)
* [Inviting an applicant for a vacancy](#add-invite)
* [Actions on a response/invitation](#actions)
  * [Put the response on hold (move to the "Think" list)](#put-on-hold)
  * [Invitation of the applicant for an interview in response to his/her response](#invite)
  * [Reject an applicant](#discard)


<a name="collections" />
## Application/invitation collections

Employer has accessible collections of applications and invitations. Each
collection contains applications/invitations in a certain state. The list of
these collections can change depending on the particular vacancy.

Vacancies available in the current user account can be seen in the
[employer's vacancy list](employer_vacancies.md#active).

If you need to get the full list of applications/invitations for the vacancy,
request all collections one by one.

The most frequently met collections:

* `inbox` – unsorted
* `hold` – need to think
* `invited` – invited
* `discarded` – discarded

### Request for obtaining the collection list

`GET /negotiations?vacancy_id={vacancy_id}`

where `vacancy_id` is a vacancy id.

### Response

Successful response comes with the `200 OK` code and contains:

```json
{
    "states": [
        {
            "id": "inbox",
            "name": "Inbox",
            "url": "https://api.hh.ru/negotiations/inbox?vacancy_id=123456"
        },
        {
            "id": "invited",
            "name": "Invited",
            "url": "https://api.hh.ru/negotiations/invited?vacancy_id=123456"
        }
    ]
}
```

| Name | Type   | Description                                                                            |
|------|--------|----------------------------------------------------------------------------------------|
| id   | string | Collection ID, unique for this vacancy at the least                                    |
| name | string | collection name                                                                        |
| url  | string | url, which GET request must be made to get applications/invitations of this collection |

If the `vacancy_id` parameter is not sent, the response will return with the
`400 Bad Request` code.


<a name="negotiations-list" />
## Application/invitation list


### Request

When url from the [collection list](#collections) is obtained, you should make a
GET request for it, for example:

`GET https://api.hh.ru/negotiations/invited?vacancy_id=123456`

Parameters:

| Name        | Mandatory | Description                                  |
|-------------|-----------|----------------------------------------------|
| vacancy_id  | yes       | Vacancy identifier                           |
| page        | no        | Defaul page number: 0                        |
| per_page    | no        | Default number of elements shown per page 20 |

The `inbox` collection, if available for this vacancy, supports
the optional parameter `with_updates_only``=true` – to show only
applications/invitations that have updates.


### Response

Successful response comes with the `200 OK` code and contains:

```json
{
    "found": 12,
    "pages": 1,
    "page": 0,
    "per_page": 20,
    "items": [
        {
            "id": "123456789",
            "created_at": "2015-05-14T00:00:00+0300",
            "updated_at": "2015-05-14T12:00:05+0300",
            "has_updates": true,
            "state": {
                "id": "invitation",
                "name": "Invitation"
            },
            "url": "https://api.hh.ru/negotiations/123456789",
            "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
            "viewed_by_opponent": false,
            "resume": {
                "id": "0123456789abcdef",
                "title": "Aspiring specialist",
                "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
                "first_name": "Ivan",
                "last_name": "Ivanov",
                "middle_name": "Ivanovich",
                "age": 19,
                "alternate_url": "http://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
                "created_at": "2015-02-06T12:00:00+0300",
                "updated_at": "2015-04-20T16:24:15+0300",
                "area": {
                    "id": "1",
                    "name": "Moscow",
                    "url": "https://api.hh.ru/areas/1"
                },
                "certificate": [
                    {
                        "achieved_at": "2015-01-01",
                        "owner": null,
                        "title": "test",
                        "type": "custom",
                        "url": "http://example.com/"
                    }
                ],
                "education": {
                    "primary": [
                        {
                            "name": "Russian State Social University, Moscow",
                            "name_id": "39420",
                            "organization": "Faculty of Information Technology",
                            "organization_id": null,
                            "result": "",
                            "result_id": null,
                            "year": 2012
                        }
                    ]
                },
                "experience": [
                    {
                        "position": "shepherd",
                        "start": "2010-01-01",
                        "end": null,
                        "company": "Horns and Hoofs",
                        "industries": [
                            {
                                "id": "51.643",
                                "name": "Land and building improvement and cleaning"
                            },
                            {
                                "id": "29.503",
                                "name": "Farming, plant cultivation, cattle breeding"
                            }
                        ],
                        "company_url": "http://example.com/",
                        "area": {
                            "id": "1",
                            "name": "Moscow",
                            "url": "https://api.hh.ru/areas/1"
                        },
                        "company_id": null,
                        "employer": null
                    },
                    {
                        "start": "2005-01-01",
                        "end": "2009-03-01",
                        "company": "HeadHunter",
                        "area": {
                            "id": "1",
                            "name": "Moscow",
                            "url": "https://api.hh.ru/areas/1"
                        },
                        "industries": [
                            {
                                "id": "7.513",
                                "name": "Internet company (search engines, payment systems, social networks, educational and entertainment resources, website promotion, and more)"
                            }
                        ],
                        "company_url": "http://hh.ru",
                        "company_id": "1455",
                        "employer": {
                            "alternate_url": "http://hh.ru/employer/1455",
                            "id": "1455",
                            "logo_urls": {
                                "90": "http://hh.ru/employer/logo/1455"
                            },
                            "name": "HeadHunter",
                            "url": "https://api.hh.ru/employers/1455"
                        }
                    }
                ],
                "gender": {
                    "id": "male",
                    "name": "Male"
                },
                "salary": {
                    "amount": 1000000,
                    "currency": "RUR"
                },
                "photo": {
                    "medium": "http://hh.ru/...",
                    "small": "http://hh.ru/...",
                    "id": "1337"
                }
            },
            "templates": [
                {
                    "url": "https://api.hh.ru/message_templates/discard_after_interview?topic_id=123456789",
                    "id": "discard_after_interview"
                }
            ]
        }
    ]
}
```

where:

| Name      | Type   | Description                             |
|-----------|--------|-----------------------------------------|
| found     | number | Number of applications found (≥ 0)      |
| pages     | number | Number of pages with applications (≥ 1) |
| per_page  | number | Number of elements per page (&gt; 0)    |
| page      | number | Number of the current page (≥ 0)        |

<a name="negotiations-list-item" />
The `items` element contains data on applications/invitations and corresponding
CVs:

| Name                 | Type         | Description                                                                                                                                                                                                                                                                                                      |
|----------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string       | Application identifier                                                                                                                                                                                                                                                                                           |
| created_at           | string       | Application/invitation creation date and time                                                                                                                                                                                                                                                                    |
| updated_at           | string       | Last application/invitation update date and time                                                                                                                                                                                                                                                                 |
| state                | object       | Current state of the application. Possible values are in the \[/dictionaries\] (./dictionaries.md) directory in the `negotiations_state` section.                                                                                                                                                                |
| url                  | string       | url for getting [the full version of an application/invitation](#get-negotiation)                                                                                                                                                                                                                                |
| messages_url         | string       | url for getting [the message list in the application](#get-messages)                                                                                                                                                                                                                                             |
| CV                   | object, null | CV. The fields shown are similar to the [CV search](resumes.md#search-results). To get the full CV, you should request it with a GET request using the url from the `url` key. It can be `null`, if the applicant deleted the CV or restricted access to it.                                                     |
| has_updates          | logical      | Any updates in the application/invitation that call for attention. The flag becames `false` when various actions are performed with the application/invitation, such as [viewing the message list](#get-messages), and also [when the CV is viewed correctly from the application/invitation](#view-resume). |
| viewed_by_opponent   | logical      | Whether the application has been viewed by the applicant                                                                                                                                                                                                                                                         |
| templates            | array        | Letter templates. Contains the template ID and url for [obtaining text according to the template](message_templates.md).                                                                                                                                                                                         |

<a name="view-resume" />

The application/invitation list contains only the main information on the CV. To
obtain the full information, particularly the applicant's contacts, you should
request the full CV. The applicant will have the CV request displayed in the
view history.

**Take note!** The additional request for CV data **must** be performed using
exactly the url from the JSON response. Only in this case the request will be
registered correctly in the view history. For instance, if a CV is requested
from the application for an anonymous vacancy, the history will display the
anonymous name of the company.

In case the vacancy the applications are requested for doesn't exist or is not
accessible for the current user, the `404 Not Found` response returns.


<a name="get-negotiation" />
## Viewing an application/invitation

### Request

`GET /negotiations/{nid}`

where `nid` is an application/invitation identifier.

It is usually obtained from the `url` key in the
[application/invitation list](#negotiations-list).

### Response

Successful response comes with the `200 OK` code and contains:

```json
{
    "id": "123456789",
    "created_at": "2015-05-14T00:00:00+0300",
    "updated_at": "2015-05-14T12:00:05+0300",
    "has_updates": true,
    "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
    "state": {
        "id": "invitation",
        "name": "Invitation"
    },
    "viewed_by_opponent": false,
    "resume": {
        "id": "0123456789abcdef",
        "title": "Aspiring specialist",
        "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
        "first_name": "Ivan",
        "last_name": "Ivanov",
        "middle_name": "Ivanovich",
        "age": 19,
        "alternate_url": "http://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
        "created_at": "2015-02-06T12:00:00+0300",
        "updated_at": "2015-04-20T16:24:15+0300",
        "area": {
            "id": "1",
            "name": "Moscow",
            "url": "https://api.hh.ru/areas/1"
        },
        "certificate": [
            {
                "achieved_at": "2015-01-01",
                "owner": null,
                "title": "тест",
                "type": "custom",
                "url": "http://example.com/"
            }
        ],
        "education": {
            "primary": [
                {
                    "name": "Russian State Social University, Moscow",
                    "name_id": "39420",
                    "organization": "Faculty of Information Technology",
                    "organization_id": null,
                    "result": "",
                    "result_id": null,
                    "year": 2012
                }
            ]
        },
        "experience": [
            {
                "area": {
                    "id": "1",
                    "name": "Moscow",
                    "url": "https://api.hh.ru/areas/1"
                },
                "company": "Horns and Hoofs",
                "company_id": null,
                "company_url": "http://example.com/",
                "employer": null,
                "end": "1999-03-01",
                "industries": [
                    {
                        "id": "45.507",
                        "name": "Extraction and processing of ore, black, base, precious, noble and rare metal"
                    }
                ],
                "industry": null,
                "start": "1998-01-01"
            }
        ],
        "gender": {
            "id": "male",
            "name": "Male"
        },
        "salary": {
            "amount": 1000000,
            "currency": "RUR"
        }
    },
    "vacancy": {
        "address": null,
        "alternate_url": "http://hh.ru/vacancy/123456",
        "archived": false,
        "area": {
            "id": "1",
            "name": "Moscow",
            "url": "https://api.hh.ru/areas/1"
        },
        "created_at": "2015-05-14T11:00:00+0300",
        "employer": {
            "alternate_url": "http://hh.ru/employer/1",
            "id": "1",
            "logo_urls": {
                "240": "http://hh.ru/employer-logo/1111.jpeg",
                "90": "http://hh.ru/employer-logo/1111.jpeg",
                "original": "http://hh.ru/employer-logo-original/1111.jpeg"
            },
            "name": "Horns and Hoofs",
            "url": "https://api.hh.ru/employers/1",
            "vacancies_url": "https://api.hh.ru/vacancies?employer_id=1"
        },
        "id": "123456",
        "name": "Manager",
        "premium": false,
        "published_at": "2015-05-14T10:00:00+0300",
        "response_letter_required": false,
        "salary": null,
        "type": {
            "id": "closed",
            "name": "Closed"
        },
        "url": "https://api.hh.ru/vacancies/123456?host=hh.ru"
    }
}
```

Response body is similar to
[the element in the application/invitation list](#negotiations-list-item),
and also contains the `vacancy` key, which has some
[brief information on the vacancy](vacancies.md#nano).


<a name="messaging_status"/>

Additionally, `messaging_status` field specifying the messaging state is
returned for a response/invitation. Possible values are provided in the
[messaging_status](dictionaries.md) reference.

In case the response/invitation does not exist or is unavailable for the current
user, '404 Not Found' server response will be returned.


<a name="get-messages" />
## Viewing a message list in an application/invitation

Messages in an application/invitation can be:

* a cover letter written by the applicant when applying for the vacancy
* some text sent by the employer when inviting for the vacancy, inviting for
  the interview or declining
* a part of free messaging between the applicant and the employer


### Request

`GET /negotiations/{nid}/messages`

where `nid` is an application/invitation identifier.

Usually the url is obtained from the `messages_url` key in the
[application/invitation list](#negotiations-list) or when
[viewing an application/invitation](#get-negotiation).


### Response

Successful response comes with the `200 OK` code and contains:

```json
{
   "found": 2,
   "pages": 1,
   "page": 0,
   "per_page": 20,
   "items": [
       {
           "id": "123",
           "text": "We are inviting you for our vacancy...",
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
                "description": "To the Right, Under the Sign",
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
                "raw": null,
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
                            "alternate_url": "http://hh.ru/applicant/assessment/123"
                        }
                    ]
                }
            ]
       },
       {
           "id": "321",
           "text": "Great, it will be my pleasure to attend the interview...",
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

| Name      | Type   | Description                           |
|-----------|--------|---------------------------------------|
| found     | number | Number of messages in messaging (≥ 0) |
| pages     | number | Number of pages with messages (≥ 1)   |
| per_page  | number | Number of messages per page (> 0)     |
| page      | number | Number of the current page (≥ 0)      |
| assessments | array| [assessment tools](assessment.md) linked to the message |

<a name="negotiations-message-item" />

The `items` element contains the data about messages:

| Name                     | Type         | Description                                                                                                                                                      |
|--------------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                       | string       | Message identifier                                                                                                                                               |
| viewed_by_me             | logical      | Whether the message is read by the viewer (for messages sent by the employer it is always `true`)                                                                |
| viewed_by_opponent       | logical      | Whether the message is read by the applicant (for the applicant's messages it is always `true`)                                                                  |
| created_at               | string       | Message creation date and time                                                                                                                                   |
| text                     | string, null | Message text. `null` can be in case when the applicant didn't send a cover letter with their application.                                                        |
| state                    | object       | Current state of the application. Possible values are in the [/dictionaries](./dictionaries.md) directory in the `negotiations_state` section                    |
| author                   | object       | Who the author of the message is                                                                                                                                 |
| author.participant_type  | string       | The role of the author of the message. Possible values are in the [/dictionaries](./dictionaries.md) directory in the `negotiations_participant_type` section    |
| address                  | object, null | [Address](./address.md), bound to the application/invitation                                                                                                     |

In case the application/invitation doesn't exist or the current user can't
access messaging, the `404 Not Found` response is returned.



<a name="add-messages" />
## Sending a message in the response/invitation

Messaging is possible after invitation of the applicant. Possibility to create a
message is determined by the
[`messages_status` field in the response/invitation](#messaging_status).


### Request

`POST /negotiations/{nid}/messages`

where `nid` is the response/invitation ID.

Additionally, the `message` parameter – message text – must be specified.

### Response

Successful server response is returned with `201 Created` code and does not have
a body.

### Errors

* `400 Bad Request` – error in the request parameters.
* `403 Forbidden` – message cannot be sent.
* `404 Not Found` – the sent response/invitation doe not exist or the current
  manager is not authorized to handle it.

In addition to an HTTP code, the server can return
[error reasons](errors.md#negotiations).

For example:

* `resume_not_found` – if the CV in the response/invitation was hidden or deleted
* `invalid_vacancy` – if the vacancy in the response/invitation was archived or deleted
* `no_invitation` – if the response/invitation is not in the "invitation"
  status. For example, it is already in the "rejected" status or still in the "response" status.
* `in_a_row_limit` – if the number of successive messages is exceeded.
  The applicant must reply to the message in order the employer is able to send new messages.
* `overall_limit` – if the messages limit is exceeded


<a name="add-invite" />
## Inviting an applicant for a vacancy

The invitation is initiated between a employer's vacancy and applicant's CV by
the employer.

In order to find out what vacancies are available for applicant invitation, use
[the list of vacancies suitable for invitation](employer_vacancies_for_invitation.md).

Also see [invitation of the applicant for an interview after the response](#invite).


### Request

`POST /negotiations`

Parameters:

Name| Required| Description
--- | ------------ | --------
vacancy_id| yes| ID of the vacancy which the applicant is invited for.
resume_id| yes| ID of the CV which the applicant is invited for.
send_sms| no| Whether to notify the applicant of the invitation via SMS. In order to send specify `true`, default value is `false`.
message| yes| The message that will be sent to the applicant's email. Use [templates](negotiation_message_templates.md) to obtain texts.
address_id| no| ID of the [address](employer_addresses.md) that will be specified in the invitation.


### Response

Successful server response is accompanied by `201 Created` code, does not have any body and contains the `Location` header pointing to the created invitation:

```
HTTP/1.1 201 Created

Location: /negotiations/321
```


### Errors

* `400 Bad Request` – error in the request parameters.
* `403 Forbidden` – invitation is impossible.

In addition to an HTTP code, the server can return [error reasons](errors.md#negotiations).

For example:

* `already_invited` – if the response between the sent CV and the vacancy
  already exists
* `resume_not_found` – if the sent CV was hidden or deleted
* `invalid_vacancy` – if the sent vacancy was archived or hidden
* `limit_exceeded` – if the manager's number of invitations per day limit was
  exceeded
* `application_denied` – general invitation denial error in case the additional
  information is unavailable
* `address_not_found` – if the sent address does not exist or belongs to
  another employer
* `not_enough_purchased_services` – if the paid services are insufficient,
  usually [CV database services](http://hh.ru/price#dbaccess)


<a name="actions" />
## Actions on a response/invitation

Action on the response is equivalent to its movement to a specific
[collection](#collections). Request:

`PUT /negotiations/{collection}/{nid}`

where
* `nid` is the response ID
* `collection` is the collection

There may be additional required and optional movement parameters.

Action examples:

* [Put the response on hold](#put-on-hold)
* [Invitation of the applicant for an interview in response to his/her response](#invite)
* [Reject an applicant](#discard)


<a name="put-on-hold"/>
## Put the response on hold (move to the "Think" list)

The action is possible if the `hold` [collection is available](#collections) for
the vacancy responses.

The response movement to the "Think" list is possible if the applicant has not
yet been invited and was not rejected. The response movement information is not
disclosed to the applicant.


### Request

`PUT /negotiations/hold/{nid}`

where `nid` is the response ID.


### Response

Successful server response is returned with `204 No Content` code and does not
have a body.


### Errors

* `404 Not Found` – the response does not exist, belongs to another employer,
  or the current manager is not authorized to handle it.
* `403 Forbidden` – movement to the "Think" list is impossible.

In addition to an HTTP code, the server can return
[error reasons](errors.md#negotiations). For example, `wrong_state`
if the movement from the current response status to the on hold list
is impossible.


<a name="invite"/>
## Invitation of the applicant for an interview in response to his/her response

The action is possible if the `invited` [collection is available](#collections)
for the vacancy responses.

The invitation is possible if the applicant has not yet been invited and was not
rejected. Upon the invitation, the applicant will receive a corresponding email.

Also see [invitation of the applicant for a vacancy](#add-invite).


### Request

`PUT /negotiations/invited/{nid}`

where `nid` is the response ID.

Parameters:

Name| Required| Description
----|--------------|---------
send_sms| no| whether to notify the applicant of the invitation via SMS. In order to send specify `true`, default value is `false`.
message| yes| The message that will be sent to the applicant's email. Use [templates](negotiation_message_templates.md) to obtain texts.
address_id| no| ID of the [address](employer_addresses.md) that will be specified in the invitation.


### Response

Successful server response is returned with `204 No Content` code and does not
have a body.


### Errors

* `404 Not Found` – the response does not exist, belongs to another employer,
  or the current manager is not authorized to handle it.
* `403 Forbidden` – invitation is impossible.
* `400 Bad Request` – error in the request parameters.


In addition to an HTTP code, the server can return
[error reasons](errors.md#negotiations).

For example:

* `wrong_state` – if the movement from the current response status to the
  invited list is impossible
* `resume_not_found` – if the CV from the response was hidden or deleted
* `empty_message` и `too_long_message` – if the text length limit is exceeded
* `address_not_found` – if the sent address does not exist or belongs to another
  employer
* `invalid_vacancy` – if the response vacancy was archived or hidden
* `limit_exceeded` – if the manager`s number of invitations per day limit
  was exceeded


<a name="discard"/>
## Reject an applicant

The action is possible if the `discarded`
[collection is available](#collections) for this vacancy responses.

The rejection is possible if the applicant had not been rejected earlier.
Upon rejection, the applicant will receive a corresponding email.


### Request

`PUT /negotiations/discarded/{nid}`

where `nid` is the response/invitation ID.

Parameters

Name| Description
----|---------
message| The message that will be sent to the applicant's email. Use [templates](negotiation_message_templates.md) to obtain texts.


### Response

Successful server response is returned with `204 No Content` code and does not
have a body.


### Errors

* `404 Not Found` – the sent response/invitation does not exist, belongs to
  another employer, or the current manager is not authorized to handle it.
* `403 Forbidden` – rejection is impossible.
* `400 Bad Request` – error in the request parameters.

In addition to an HTTP code, the server can return
[error reasons](errors.md#negotiations).

For example:

* `wrong_state` – if the movement from the current response status to the
  discarded list is impossible
* `empty_message` и `too_long_message` – if the text length limit
  is exceeded
