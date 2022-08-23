# Vacancies suitable for invitation

The request is used for selection of a suitable vacancy when
[inviting an applicant](employer_negotiations.md#add-invite).


### Request

`GET /employers/{employer_id}/vacancies/active?resume_id={resume_id}`

where
* `employer_id` – the employer ID that can be found using the
  [current user information request](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/paths/~1me/get),
* `resume_id` – the CV ID.

Additionally, [pagination parameters](general.md#pagination) `page`, `per_page`
are supported.


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "per_page": 20,
    "items": [
        {
            "negotiations_state": null,
            "negotiations_employer_state": null,
            "can_invite": true,
            "negotiations_actions": [
                {
                    "id": "invitation",
                    "name": "Invite",
                    "enabled": true,
                    "method": "POST",
                    "url": "https://api.hh.ru/negotiations/invited",
                    "resulting_employer_state": {
                        "id": "invitation",
                        "name": "Invitation"
                    },
                    "templates": [
                        {
                            "id": "invite",
                            "name": "Invite",
                            "quick": false,
                            "url": "https://api.hh.ru/message_templates/invite?resume_id=0123456789abcdef&vacancy_id=123456"
                        }
                    ],
                    "arguments": [
                        {
                            "id": "resume_id",
                            "required": true,
                            "required_arguments": []
                        },
                        {
                            "id": "vacancy_id",
                            "required": true,
                            "required_arguments": []
                        },
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
                }
            ],

            "id": "123456",
            "premium": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/123456",
            "salary": {
                "to": null,
                "from": 100000,
                "currency": "RUR"
            },
            "name": "Testing automation specialist (Java, Selenium)",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Moscow"
            },
            "url": "https://api.hh.ru/vacancies/123456",
            "published_at": "2013-10-11T13:27:16+0400",
            "relations": [ ],
            "employer": {
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/1455.png",
                    "240": "https://hh.ru/employer-logo/1455.png",
                    "original": "https://hh.ru/file/1455.png"
                },
                "name": "HeadHunter",
                "id": "1455"
            },
            "response_letter_required": false,
            "type": {
                "id": "open",
                "name": "Open"
            }
        }
    ],
    "page": 0,
    "pages": 1,
    "found": 1
}
```

Returned is a list similar to
[published vacancies of the current manager](employer_vacancies.md#active)
with [standard fields](vacancies.md#nano), as well as additional fields:

 * `negotiations_state`-- response/invitation status for this vacancy or `null`
   if there was no response/invitation
 * `can_invite`-- The flag that determines whether it is possible to invite
   the specified CV to this vacancy
 * `employer_negotiations_state` - current employer status of
   the response/invitation or `null` if there was no response/invitation
 * `templates`-- list of [templates](negotiation_message_templates.md) with
   texts for invitation
 * <a name="actions"></a> `negotiations_actions`-- list of possible actions on
   response/invitation for [creating invitation](employer_negotiations.md#add-invite).
   Where a response cannot be generated (e.g., the required services are not available), an empty array will return.
   The action results format is identical to the [response/invite actions](employer_negotiations.md#actions-info).

When deciding whether to grant a user the possibility to invite a selected CV
for the vacancy, you should not rely on the fact that `negotiations_state` has
the `null` value and should use the `can_invite` flag.

Presence of the `can_invite` = `true` flag in the vacancy means the invitation
process will be successful. For example, in the meantime between obtaining a
list of suitable vacancies and invitation, an applicant may delete his/her CV.

In case the vacancy with specified CV already has a response/invitation, its
state will be specified as:

```json
{
    "negotiations_state": {
        "id": "response",
        "name": "Response"
    },
    "negotiations_employer_state": {
        "id": "response",
        "name": "Response"
     }
}
```

Possible values of the state/invitation for an applicant are available in the
[negotiations_state reference](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/paths/~1dictionaries/get), for employer in the
[employer statuses for responses/invitations on vacancy](employer_negotiations.md#collection).


### Errors

When the request is made without any authorization or with the applicant
authorization, `403 Forbidden` code will be returned.

If the specified employer does not exist, or its vacancies are unavailable,
`404 Not Found` error will be returned.
