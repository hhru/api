# Negotiations (responses/invitations) for employers


*Negotiations documentation for the applicant is available in the [separate article](negotiations.md).*

* [Processing model, terms and procedures](#model)
* [General description of processing responses/invitations](#flow)
* [Collections and employer statuses for responses/invitations](#collections)
* [List of responses/invitation](#negotiations-list)
* [View the response/invitation](#get-negotiation)
* [View the list of messages in the response/invitation](#get-messages)
* [Sending a message in the response/invitation](#add-messages)
* [Inviting an applicant for a vacancy](#add-invite)
* [Response/invitation actions (status change)](#actions)


<a name="model"></a>
## Processing model, terms and procedures

Responses and invitations correspond to the model displayed in API
requests and responses. If the application uses the model correctly, the change
of response and invitation business logics won't require their reprocessing or
corrections.

Responses and invitations contain following terms:

* *response* – object generated on the initiative of the applicant (response to the vacancy).
  Response is always sent with single CV on single vacancy.

* *invitation* – object generated on the initiative of the employer (vacancy
  invitation). Invitation is always sent for one vacancy for one CV.

Except of the object appearance process, the response and invitation processing is made
identically.

* <a name="term-collection"></a> *collection* – the set of responses/invitations,
  combined by certain criteria. Collections are used when your
  application needs **to display** the list of responses/invitations.
  The logic response/invitation processing is subject to change,
  so don't rely on having response/invitation in certain collection during processing.

* <a name="term-state"></a> *applicant status of response/invitation* –
  response/invitation status **displayed for the applicant**. Possible values
  are given in [`negotiations_state` reference guide](dictionaries.md#negotiations) and
  don't depend on vacancy in response/invitation.

* <a name="term-employer-state"></a> *employer status of response/invitation* –
  employer status of response/invitation. May differ from the
  applicant's. The list of possible statuses
  **depends on the vacancy and the employer**, so the list
  [should be requested](#states) upon transferring proper vacancy.

* <a name="term-action"></a> *respond/invitation action* – the action to be
  performed for response/invitation. As the result,
  the employer and the applicant statuses of response/invitation may be
  changed or leaved as is.

Don't confuse *action*, *collection* and *status* – they can look similar, but
designed for different purposes.


<a name="flow"></a>
## General description of processing responses/invitations

All actions on processing responses/invitations are made within
**one selected vacancy**. One employer can have vacancies
with different rules on processing responses/invitations.

First, you need to get the list
[of collections and employer statuses](#collections). Use collections
to **get the list of responses/invitations**. Ask user
to select the preferred collections. Retrive all
collection successively to receive all responses/invitations. List
of statuses should be used for reference only.

Request the vacancies related to selected CV to **create the invitation**
from the employer. See [employer vacancy list](employer_vacancies_for_invitation.md) for this data as well as required
parameters (key `arguments`) and status of generated
response (key `resulting_employer_state`). Different employers and vacancies
may employ different rules and statuses for added response. Each
pair *vacancy + CV* can have only one response/invitation.

To generate the invitation, the employer should have enabled access to
CV database. No access required to process the existing response/invitation. This
allows processing vacancy responses without access to CV database.

To **make an action** on response/invitation,
see [the list of actions](#actions-info) available in
[the list (collection) of responses/invitations](#negotiations-list) and in
[individual response/invitation](#get-negotiation). If this action results in
change of response/invitation status, it will be displayed in key
`resulting_employer_state`. Not all actions result in status change.

Invite the applicant to initiate
[free negotiation](#get-messages). You can
[send messages](#add-messages), and applicant can respond on them.
When necessary, the negotiation on certain vacancy may be
[disabled](employer_vacancies.md#allow_messages) (field `allow_messages`).


<a name="states"></a>
<a name="collections"></a>
## Collections and employer statuses for responses/invitations on vacancy

Employer has available collections of responses and invitations. The list of these collections
may be changed depending on the vacancy.

You can get available vacancies of the current user through
[employer vacancy list](employer_vacancies.md#active).

Presently, there is no collection combining all responses/invitations on the vacancy
available. Request all collections successively to get
the full list.


### Request

`GET /negotiations?vacancy_id={vacancy_id}`

where `vacancy_id` – ID of the vacancy.


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "collections": [
        {
            "id": "somecollection",
            "name": "Name of collection",
            "description": "Collection description",
            "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456"
        },
        {
            "id": "anothercollection",
            "name": "Name of anothercollection",
            "url": "https://api.hh.ru/negotiations/anothercollection?vacancy_id=123456"
        }
    ],
    "employer_states": [
        {
            "id": "response",
            "name": "Response"
        },
        {
            "id": "invitation",
            "name": "Invitation"
        },
        {
            "id": "discard",
            "name": "Rejection"
        },
        {
            "id": "discard_after_interview",
            "name": "Rejected after interview"
        }
    ]
}

```

Name | Type | Description
--- | --- | --------
collections | list | of [collections](#term-collection) of responses/invitations for this vacancy
collections.id | string | collection ID unique at least for this vacancy
collections.name | string | collection name
collections.description | string | collection description
collections.url | string | URL to send the GET request to in order to get responses/invitations for this collection
employer_states | list | of [employer statuses](#term-employer-state) for responses/invitations on the vacancy
employer_states.id | string | status ID unique at least for this vacancy
employer_states.name | string | status name

### Errors

* `400 Bad Request` - parameter `vacancy_id` is not sent.
* `403 Forbidden` – authorization is failed.


<a name="negotiations-list"></a>
## List of responses/invitation


### Request

Upon getting URL from the [collection list](#collections) send a GET request to
this URL, e.g.:

`GET https://api.hh.ru/negotiations/invited?vacancy_id=123456`

Parameters:

Name | Required | Description
--- | ------------ | --------
vacancy_id| yes | Vacancy ID
page | no | Page number, default: 0
per_page | no | Number of elements displayed per page, by default: 20


### Response

Successful server response is returned with `200 OK` code and contains:

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
                "id": "response",
                "name": "Response"
            },
            "employer_state": {
                "id": "response",
                "name": "Response"
            },
            "actions": [
                {
                    "id": "invitation",
                    "name": "Invite",
                    "enabled": true,
                    "method": "PUT",
                    "url": "https://api.hh.ru/negotiations/invited/123456789",
                    "resulting_employer_state": {
                        "id": "invitation",
                        "name": "Invitation"
                    },
                    "templates": [
                        {
                            "id": "invite_after_response",
                            "name": "Invite responded applicant",
                            "quick": false,
                            "url": "https://api.hh.ru/message_templates/invite_after_response?topic_id=123456789"
                        }
                    ],
                    "arguments": [
                        {
                            "id": "message",
                            "required": true,
                            "required_arguments": []
                        },
                        {
                            "id": "send_sms",
                            "required": false,
                            "required_arguments": [
                                {
                                    "id": "message"
                                }
                            ]
                        },
                        {
                            "id": "address_id",
                            "required": false,
                            "required_arguments": [
                                {
                                    "id": "message"
                                }
                            ]
                        }
                    ]
                },
                {
                    "id": "hold",
                    "name": "Think",
                    "enabled": true,
                    "method": "PUT",
                    "url": "https://api.hh.ru/negotiations/hold/123456789",
                    "arguments": [],
                    "resulting_employer_state": null,
                    "templates": []
                }
            ],
            "url": "https://api.hh.ru/negotiations/123456789",
            "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
            "viewed_by_opponent": false,
            "resume": {
                "id": "0123456789abcdef",
                "title": "Young specialist",
                "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
                "first_name": "Ivan",
                "last_name": "Ivanov",
                "middle_name": "Ivanovich",
                "age": 19,
                "can_view_full_info": true,
                "alternate_url": "https://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
                "total_experience": {
                    "months": 118
                },
                "experience": [
                    {
                        "position": "cattleman",
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
                                "name": "Farming, crop growing, livestock farming"
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
                        "company_url": "https://hh.ru",
                        "company_id": "1455",
                        "employer": {
                            "alternate_url": "https://hh.ru/employer/1455",
                            "id": "1455",
                            "logo_urls": {
                                "90": "https://hh.ru/employer/logo/1455"
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
                    "medium": "https://hh.ru/...",
                    "small": "https://hh.ru/...",
                    "id": "1337"
                },
                "owner": {
                    "id": "123456",
                    "comments": {
                        "url": "https://api.hh.ru/applicant_comments/123456",
                        "counters": {
                            "total": 7
                        }
                    }
                },
                "download": {
                    "pdf": {
                        "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.pdf?type=pdf"
                    },
                    "rtf": {
                        "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.rtf?type=rtf"
                    }
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

Name | Type | Description
--- | --- | --------
found | number | Number of responses found ( ≥ 0 )
pages | number | Number of pages with responses ( ≥ 1 )
per_page | number | Number of elements per page ( > 0 )
page | number | Number of the current page ( ≥ 0 )

<a name="negotiations-list-item"></a>
The `items` entity contains response/invitation data and CVs for them:

Name | Type | Description
--- | --- | --------
id | string | Response ID
created_at | string | Response/invitation creation date and time
updated_at| string | Response/invitation update date and time
state | object | Current [response status of the applicant](#term-state).
employer_state | object | Current [employer status of the applicant](#term-employer-state).
actions| list | list of possible [actions on response/invitation](#actions-info)
url | string | URL to get [the full version of response/invitation](#get-negotiation)
messages_url | string | URL to get [the list of messages in the response](#get-messages)
resume| object, null | [Short CV](resumes.md#resume-short). To get full CV, send a GET request to URL from key `url`. It can be `null`, if the applicant deleted the CV or disabled access to it.
has_updates| logical | Whether the response/invitation includes updates that require attention. The flag can be disabled upon different response/invitation actions, e.g. upon [viewing message list](#get-messages), and [appropriate view of CV on response/invitation](#view-resume).
viewed_by_opponent| logical | Whether the response was viewed by the applicant

<a name="view-resume"></a>

The list of responses/invitations contains only basic CV info.
To get full info, such as applicant contact details,
request the full CV. The applicant will see this CV request in
view history.

**Important!** Additional request on CV data **should be**
sent to URL from JSON response. This is the only option
to correctly process the request in view history. E.g, if the CV is requested from the response
to anonymous vacancy, the history will display anonymous name of the company.

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - the vacancy of requested responses doesn't exist or not available to the current user.

<a name="actions-info"></a>
### Response/invitation actions (`actions`)

The number of actions may differ, and the list of actions may be
empty.

Each action is indicated with:

Name | Type | Description
--- | --- | --------
id | string | Action ID
name | string | Action name
enabled | logical | Whether the action is possible
method | string | HTTP method to perform
url | string | URL to send the request to
resulting_employer_state | object, null | [employer status](#term-employer-state) on response/invitation enabled upon the action. If the action doesn't change the status – `null`.
templates | list | Letter templates. Contains the template ID and url for [obtaining text according to the template](negotiation_message_templates.md).
arguments | list | Mandatory and optional arguments for the request

Action has attached list of possible arguments
such as:

* `message` – the message that will be sent to the applicant's email. Use [templates](negotiation_message_templates.md) to obtain texts.
* `address_id` – ID of the [address](employer_addresses.md) that will be specified in the invitation
* `send_sms` – whether to notify the applicant of the invitation via SMS. In order to send specify `true`, default value is `false`.

The application should be capable of entering these arguments. In future we may add other arguments, however
they won't be mandatory. Mandatory arguments may vary depending
on response/invitation.

Each argument will be indicated with:

Name | Type | Description
--- | --- | --------
id | string | Argument ID
required | logical | Mandatory argument
required_arguments | list | Arguments to be applied if this argument is indicated. E.g., the address is optional, however if it is indicated you must also specify the message.

### Errors

* `403 Forbidden` – authorization is failed.


<a name="get-negotiation"></a>
## View the response/invitation

### Request

`GET /negotiations/{nid}`

where `nid` is the response/invitation ID.

Usually is taken from key `url` in
[the list of responses/invitations](#negotiations-list).

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "id": "123456789",
    "created_at": "2015-05-14T00:00:00+0300",
    "updated_at": "2015-05-14T12:00:05+0300",
    "has_updates": true,
    "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
    "messaging_status": "ok",
    "state": {
        "id": "response",
        "name": "Response"
    },
    "employer_state": {
        "id": "response",
        "name": "Response"
    },
    "actions": [
        {
            "id": "invitation",
            "name": "Invite",
            "enabled": true,
            "method": "PUT",
            "url": "https://api.hh.ru/negotiations/invited/123456789",
            "resulting_employer_state": {
                "id": "invitation",
                "name": "Invitation"
            },
            "templates": [
                {
                    "id": "invite_after_response",
                    "name": "Invite responded applicant",
                    "quick": false,
                    "url": "https://api.hh.ru/message_templates/invite_after_response?topic_id=123456789"
                }
            ],
            "arguments": [
                {
                    "id": "message",
                    "required": true,
                    "required_arguments": []
                },
                {
                    "id": "send_sms",
                    "required": false,
                    "required_arguments": [
                        {
                            "id": "message"
                        }
                    ]
                },
                {
                    "id": "address_id",
                    "required": false,
                    "required_arguments": [
                        {
                            "id": "message"
                        }
                    ]
                }
            ]
        },
        {
            "id": "hold",
            "name": "Think",
            "enabled": true,
            "method": "PUT",
            "url": "https://api.hh.ru/negotiations/hold/123456789",
            "arguments": [],
            "resulting_employer_state": null,
            "templates": []
        }
    ],
    "viewed_by_opponent": false,
    "resume": {
        "id": "0123456789abcdef",
        "title": "Young specialist",
        "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
        "first_name": "Ivan",
        "last_name": "Ivanov",
        "middle_name": "Ivanovich",
        "age": 19,
        "alternate_url": "https://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
                    "organization": "IT Department",
                    "organization_id": null,
                    "result": "",
                    "result_id": null,
                    "year": 2012
                }
            ]
        },
        "total_experience": {
            "months": 118
        },
        "experience": [
            {
                "area": {
                    "id": "1",
                    "name": "Moscow",
                    "url": "https://api.hh.ru/areas/1"
                },
                "company": "Roga i Kopyta",
                "company_id": null,
                "company_url": "http://example.com/",
                "employer": null,
                "end": "1999-03-01",
                "industries": [
                    {
                        "id": "45.507",
                        "name": "Mining and dressing of ferrous, non-ferrous, precious, noble and rare metals"
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
        },
        "owner": {
            "id": "123456",
            "comments": {
                "url": "https://api.hh.ru/applicant_comments/123456",
                "counters": {
                    "total": 7
                }
            }
        },
        "download": {
            "pdf": {
                "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.pdf?type=pdf"
            },
            "rtf": {
                "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.rtf?type=rtf"
            }
        }
    },
    "vacancy": {
        "address": null,
        "alternate_url": "https://hh.ru/vacancy/123456",
        "archived": false,
        "area": {
            "id": "1",
            "name": "Moscow",
            "url": "https://api.hh.ru/areas/1"
        },
        "created_at": "2015-05-14T11:00:00+0300",
        "employer": {
            "alternate_url": "https://hh.ru/employer/1",
            "id": "1",
            "logo_urls": {
                "240": "https://hh.ru/employer-logo/1111.jpeg",
                "90": "https://hh.ru/employer-logo/1111.jpeg",
                "original": "https://hh.ru/employer-logo-original/1111.jpeg"
            },
            "name": "Roga i Kopyta",
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

Response body is identical
[to the element in the list of responses/invitations](#negotiations-list-item), and
contains key `vacancy` giving
[short info regarding vacancy](vacancies.md#nano).

<a name="messaging_status"></a>
Additionally, field `messaging_status` showing negotiation status
is returned for the response/invitation. Possible values
see in [messaging_status](dictionaries.md) reference guide.

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - response/invitation doesn't exist or negotiation not available to the current user.


<a name="get-messages"></a>
## View the list of messages in the response/invitation

Messages contained in the response/invitation can be made as:

* cover letter left by the applicant upon response to the vacancy
* text sent by the employer upon inviting for the vacancy, for the interview
  or upon rejection
* free negotiation messages between the applicant and the employer

### Request

`GET /negotiations/{nid}/messages`

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

<a name="negotiations-message-item"></a>
The `items` entity contains message data:

Name | Type | Description
--- | --- | --------
id | string | Message ID
viewed_by_me| logical | Whether the message was read by the viewer (for messages sent by employer the value is always `true`)
viewed_by_opponent| logical | Whether the message was read by the applicant (for messages sent by applicant the value is always `true`)
created_at | string | Message creation date and time
text| string, null | Message text. `null` can be displayed if the applicant didn't attach the cover letter to the response.
state | object | Current state of the application. Possible values are listed in the [/dictionaries](./dictionaries.md) reference, section `negotiations_state`
author| object | Who is the message author
author.participant_type| string | Message author role. Possible values are listed in the [/dictionaries](./dictionaries.md) reference, section `negotiations_participant_type`
address| object, null | [Address](./address.md) linked to the response/invitation
assessments| array | [assessment tools](assessment.md) linked to the message

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - response/invitation doesn't exist or negotiation not available to the current user.


<a name="add-messages"></a>
## Sending a message in the response/invitation

Messaging is possible after invitation of the applicant. Find out whether you can
leave the message from
[field `messages_status` in response/invitation](#messaging_status).

### Request

`POST /negotiations/{nid}/messages`

where `nid` is the response/invitation ID.

Additionally, the `message` parameter – message text – must be specified.

### Response

Successful server response is returned with `201 Created` code and does not have a body.

### Errors

* `400 Bad Request` – error in the request parameters.
* `403 Forbidden` – message cannot be sent.
* `404 Not Found` – sent response/invitation doesn't exist or current
  manager is not authorized to process it.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).

For example:

* `resume_not_found` – if the CV in the response/invitation was hidden
  or deleted
* `invalid_vacancy` – if the vacancy in the response/invitation was archived
  or hidden
* `no_invitation` – if the response/invitation is not in the "invitation" status.
  For example, it is already in the "rejected" status or still in the "response" status.
* `in_a_row_limit` – if the number of successive messages is exceeded.
  The applicant must reply to the message in order the employer is able to send
  new messages.
* `overall_limit` – if the messages limit is exceeded


<a name="add-invite"></a>
## Inviting an applicant for a vacancy

The invitation is initiated between an employer's vacancy and an applicant's CV by
the employer. To send the request you need to know initial
statuses of this pair of vacancy and CV. Learn more in
[general description of processing](#flow).

### Request

`POST /negotiations/{state}`

where `state` – is the initial status of the invitation.

Invitation parameters can be got from
[action list](employer_vacancies_for_invitation.md#actions-info).

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
* `403 Forbidden` – authorization is failed.
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

### Request

`PUT /negotiations/{collection}/{nid}`

where

* `nid` is the response ID
* `collection` is the collection

Accurate URL for the request, mandatory and optional
parameters should be received from the [action list](#actions-info)
on response/invitation.

Parameters should be sent in standard format
`application/x-www-form-urlencoded`.

Action examples:

* Put the response on hold
* Invitation of the applicant for an interview in response to his/her response
* Reject an applicant

Possible actions may differ for each response/invitation and
actions listed above may be not available.

### Response

Successful server response is returned with `204 No Content` code and does not have a body.


### Errors

* `400 Bad Request` – one of the mandatory parameters is not sent.
* `403 Forbidden` – authorization is failed.
* `403 Forbidden` – response action is not possible.
* `404 Not Found` – response doesn't exist, refers to other employer, or
  current manager is not authorized to process it.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).

For example:

* `wrong_state` – action is not possible due to current response status
* `resume_not_found` – if the CV from the response was hidden or deleted
  by the applicant
* `empty_message` and `too_long_message` – text size limit is
  violated
* `address_not_found` – if the sent address does not exist or belongs to
  another employer
* `invalid_vacancy` – if the response vacancy was archived or hidden
* `limit_exceeded` – if the manager's number of invitations per day limit
  was exceeded
