# Negotiations (responses/invitations) for employers

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](employer_payable_methods.md)

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
  are available [in the `negotiations_state` directory](dictionaries.md#negotiations) and
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
[employer job list](employer_vacancies_for_invitation.md), which also
contains the required parameters (the "arguments" key) and the status of the created
response (the "resulting_employer_state" key). Different employers and different
jobs may have different rules and statuses for added responses. Each
*job + resume* pair can have only one response/invitation.

To create an invitation, an employer must have activated access to the database of
resumes. Employers do not need such access to work with an existing response/invitation. This
allows them to process responses to jobs even without access to the resume database.

If you need to **take an action** with respect to a response/invitation,
please refer to the [list of actions](#actions-info) that will be available in the
[list (collection) of responses/invitations](#negotiations-list) and in the
[individual response/invitation](#get-negotiation). If the action
changes the status of a response/invitation, it will be explicitly specified in the
"resulting_employer_state" key. Not all actions lead to a status change.

After inviting the applicant, you can start a
[free conversation](#get-messages). You will be able to
[send messages](#add-messages) and receive responses from the applicant.
If necessary, you
[can disable](employer_vacancies.md#allow_messages) conversations for a specific job (the "allow_messages" field).


<a name="states"></a>
<a name="collections"></a>
## Collections and employers' statuses of responses/invitations

Collections of responses/invitations are available to the employer. The list of such collections
may vary depending on the specific job.

You can get the jobs for a specific user from the [employer job list](employer_vacancies.md#active).

At the moment, there is no collection that could combine all responses/invitations for a job. 
To get a complete list, you need to sequentially request all collections.


### Request

```
GET /negotiations?vacancy_id={vacancy_id}
```

where `vacancy_id` – ID of the vacancy.


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "collections": [
        {
            "id": "somecollection",
            "name": "Collection name",
            "description": "Collection description",
            "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456",
            "counters": {
                "with_updates": 4,
                "total": 5
            },
            "order_types": [
                {
                    "id": "created_at",
                    "name": "by created date",
                    "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456&order_by=created_at"
                },
                {
                    "id": "relevance",
                    "name": "relevance",
                    "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456&order_by=relevance"
                }
            ]
        },
        {
            "id": "anothercollection",
            "name": "Another collection name",
            "url": "https://api.hh.ru/negotiations/anothercollection?vacancy_id=123456",
            "counters": {
                "with_updates": 0,
                "total": 1
            },
            "order_types": [
                {
                    "id": "created_at",
                    "name": "by created date",
                    "url": "https://api.hh.ru/negotiations/anothercollection?vacancy_id=123456&order_by=created_at",
                }
            ]
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
            "name": "Discard"
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
collections[].id | string | collection ID unique at least for this vacancy
collections[].name | string | collection name
collections[].description | string | collection description
collections[].url | string | URL to send the GET request to in order to get responses/invitations for this collection
collections[].counters.with_updates | number | the number of responses/invitations in this collection that [require attention](#has_updates)
collections[].counters.total | number | the total number of responses/invitations in this collection
collections[].order_types | list | <a name="order-types"></a> possible options for sorting responses/invitations in a collection
employer_states | list | of [employer statuses](#term-employer-state) for responses/invitations on the vacancy
employer_states[].id | string | status ID unique at least for this vacancy
employer_states[].name | string | status name

If parameter `vacancy_id` is not sent, the response with code
`400 Bad Request` will be returned.


<a name="negotiations-list"></a>
## List of responses/invitation


### Request

Upon getting URL from the [collection list](#collections) send a GET request to
this URL, e.g.:

```
GET https://api.hh.ru/negotiations/invited?vacancy_id=123456
```

Parameters:

Name | Required | Description
--- | ------------ | --------
vacancy_id| yes | Vacancy ID
order_by | no | Sorting option. Possible values may differ for different collections; the available options are specified in the [list of collections in the `order_types` field](#order-types).
page | no | Page number, default: 0
per_page | no | Number of items per page: default value is 20; the maximum value is 50


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "ordered_by": {
        "id": "created_at",
        "name": "by created date"
    },
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
                "negotiations_history": {
                    "url": "https://api.hh.ru/resumes/0123456789abcdef/negotiations_history"
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
            ],
             "counters": {
                 "messages": 100,
                 "unread_messages": 50
             }
        }
    ]
}
```

where:

Name | Type | Description
--- | --- | --------
ordered_by | object | Enabled sorting option
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
state | object | The current [applicant's response status](#term-state).
employer_state | object | The current [employer's response status](#term-employer-state).
actions| list | list of possible [actions on response/invitation](#actions-info)
url | string | URL to get [the full version of response/invitation](#get-negotiation)
messages_url | string | URL to get [the list of messages in the response](#get-messages)
resume| object, null | [Short CV](resumes.md#resume-short). To get full CV, send a GET request to URL from key `url`. It can be `null`, if the applicant deleted the CV or disabled access to it.
has_updates| logical | <a name="has_updates"></a> Whether the response/invitation includes updates that require attention. The flag can be disabled upon different response/invitation actions, e.g. upon [viewing message list](#get-messages), and [appropriate view of CV on response/invitation](#view-resume).
viewed_by_opponent| logical | Whether the response was viewed by the applicant
counters | object | Counters
counters.messages | number | Total number of messages
counters.unread_messages | number | Number of messages that have not been read by the employer

<a name="view-resume"></a>

The list of responses/invitations contains only basic CV info.
To get full info, such as applicant contact details,
request the full CV. The applicant will see this CV request in
view history.

**Important!** Additional request on CV data **should be**
sent to URL from JSON response. This is the only option
to correctly process the request in view history. E.g, if the CV is requested from the response
to anonymous vacancy, the history will display anonymous name of the company.

If the vacancy of requested responses doesn't exist or
not available to the current user, `404 Not Found` response will be returned.

<a name="actions-info"></a>
### Response/invitation actions (`actions`)

The number of actions may differ, and the list of actions may be empty.

The following parameters are specified for each action:

Name | Type | Description
--- | --- | --------
id | string | Action ID
name | string | Action name
enabled | logical | Whether the action is possible
method | string | HTTP method to perform
url | string | URL to send the request to
resulting_employer_state | object, null | [employer's response/invitation status](#term-employer-state) to be assigned after the action is performed. If the action does not change the state, the value is "null".
templates | list | Email templates. Contains the template ID and URL for [getting the text for the template](negotiation_message_templates.md).
arguments | list | Mandatory and additional arguments for the request

There is a list of arguments for the action; at this point, you may encounter the following arguments:

* `message` – the message that will be sent to the applicant's email. Use [templates](negotiation_message_templates.md) to obtain texts.
* `address_id` – [address](employer_addresses.md) ID that will be specified in the invitation
* `send_sms` – whether to notify the applicant of the invitation via SMS. To initiate the sending of a message, pass "true"; the default is "false".

The application should be able to fill in these arguments. Other arguments may be added in the future;
however, they will not be mandatory. The list of mandatory arguments
can be different for different responses/invitations.

The following parameters will be specified for each argument:

Name | Type | Description
--- | --- | --------
id | string | Argument ID
required | logical | Whether the argument is mandatory
required_arguments | list | Arguments that must also be passed if this argument is specified. For example, the address is optional, but you must also specify a message when you pass the address.


<a name="get-negotiation"></a>
## View the response/invitation

### Request

```
GET /negotiations/{nid}
```

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
            ],
            "level": {
                "id": "higher",
                "name": "Higher"
            }
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
        "negotiations_history": {
            "url": "https://api.hh.ru/resumes/0123456789abcdef/negotiations_history"
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
    },
    "counters": {
        "messages": 100,
        "unread_messages": 50
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

If response/invitation doesn't exist or not available to the current user,
`404 Not Found` response will be returned.


<a name="get-messages"></a>
## View the list of messages in the response/invitation

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

If response/invitation doesn't exist or negotiation not available to the current user,
`404 Not Found` response will be returned.


<a name="add-messages"></a>
## Sending a message in the response/invitation

Messaging is possible after invitation of the applicant. Find out whether you can
leave the message from
[field `messages_status` in response/invitation](#messaging_status).

### Request

```
POST /negotiations/{nid}/messages
```

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

```
PUT /negotiations/{collection}/{nid}
```

where

* `nid` is the response ID
* `collection` is the collection

The exact URL for the request, as well as the required and optional
parameters should be obtained from the [list of actions](#actions-info)
for the response/invitation.

Parameters should be sent in standard format
`application/x-www-form-urlencoded`.

Action examples:

* Delay the response
* Invite the applicant to an interview in response to the response
* Reject the applicant

Possible actions may be different for each response/invitation, for example,
the above actions may not be available.

### Response

Successful server response is returned with `204 No Content` code and does not have a body.


### Errors

* `404 Not Found` – response doesn't exist, refers to other employer, or
  current manager is not authorized to process it.
* `400 Bad Request` – one of the mandatory parameters is not sent.
* `403 Forbidden` – response action is not possible.

In addition to an HTTP code, the server can return
[error reason](errors.md#negotiations).

For example:

* `wrong_state` – if the action is not possible because of the current response status
* `resume_not_found` – if the resume from this response was hidden or deleted by the applicant
* `empty_message` and `too_long_message` – text size limit is
  violated
* `address_not_found` – if the sent address does not exist or belongs to
  another employer
* `invalid_vacancy` – if the response vacancy was archived or hidden
* `limit_exceeded` – if the manager's number of invitations per day limit
  was exceeded

<a name="get-preference-order"></a>
## Viewing preferred options for sorting responses

### Request

```
GET /vacancies/{id}/preferred_negotiations_order
```

where id - ID of the vacancy

### Response

The response will contain a JSON:

```json
  {
      "order_type": {
        "id": "created_at",
        "name": "by created date"
      }
  }
```

### Errors

* `404 Not Found` - the vacancy was not found or it is impossible to view the responses/invitations.

<a name="update-preference-order"></a>
## Changing preferred options for sorting responses

### Request

```
PUT /vacancies/{id}/preferred_negotiations_order
```

where order_by (sorting option ID) should be passed as a parameter

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `400 Bad Request` – one of the mandatory parameters has not been passed.
* `404 Not Found` – the job was not found or it is impossible to view the responses/invitations.
