# Vacancies suitable for invitation

The request is used for selection of a suitable vacancy when
[inviting an applicant](employer_negotiations.md#add-invite).


### Request

`GET /employers/{employer_id}/vacancies/active?resume_id={resume_id}`

where
* `employer_id` – the employer ID that can be found using the
  [current user information request](me.md#info),
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
            "can_invite": true,
            "templates": [
                {
                    "url": "https://api.hh.ru/message_templates/invite?resume_id=0123456789abcdef&vacancy_id=123456",
                    "id": "invite"
                }
            ],

            "id": "123456",
            "premium": true,
            "address": null,
            "alternate_url": "http://hh.ru/vacancy/123456",
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
                "alternate_url": "http://hh.ru/employer/1455",
                "logo_urls": {
                    "90": "http://hh.ru/employer-logo/1455.png",
                    "240": "http://hh.ru/employer-logo/1455.png",
                    "original": "http://hh.ru/file/1455.png"
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
 * `templates`-- list of [templates](negotiation_message_templates.md) with
   texts for invitation

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
    }
}
```

Possible values of the state/invitation are available in the
[negotiations_state reference](dictionaries.md).


### Errors

When the request is made without any authorization or with the applicant
authorization, `403 Forbidden` code will be returned.

If the specified employer does not exist, or its vacancies are unavailable,
`404 Not Found` error will be returned.
