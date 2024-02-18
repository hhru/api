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

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Negotiations-(responsesinvitations)-for-applicants/operation/get-negotiations)

<a name="get_negotiations_active"></a>
## Receiving the list of active responses

### Request

Use the `status=active` parameter in your request for [the list of responses](#get_negotiations) to obtain the list of active responses.
 ```
 GET /negotiations?status=active
 ```

The following resource was used before April 20, 2020 to request active vacancies:

```
GET /negotiations/active
```

The resource is currently out of date, and is supported for backward connectivity purposes only.

<a name="post_negotiation"></a>
## Respond to the vacancy

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Vacancies/operation/apply-to-vacancy)

<a name="get_negotiation"></a>
## View the response/invitation

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Negotiations-(responsesinvitations)-for-applicants/operation/get-negotiation-item)

<a name="hide_message"></a>
## Hide the response
> !! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Negotiations-(responsesinvitations)-for-applicants/operation/hide-active-response)


<a name="get_messages"></a>
## View the list of messages in the response

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Negotiations-(responsesinvitations)-for-applicants/operation/get-negotiation-messages)

<a name="send_message"></a>
## Sending new message

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Negotiations-(responsesinvitations)-for-applicants/operation/send-negotiation-message)

<a name="edit_message"></a>
## Edit messages in the response

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Negotiations-(responsesinvitations)-for-applicants/operation/edit-negotiation-message)
