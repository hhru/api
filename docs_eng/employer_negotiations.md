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
* [Changing the response/invite state](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/change-negotiation-action)
* [Changing the state of multiple responses/invites](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/put-negotiations-collection-to-next-state)
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

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-negotiation-messages)

<a name="add-messages"></a>
## Sending a message in the response/invitation

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/send-negotiation-message)

<a name="add-invite"></a>
## Inviting an applicant for a vacancy

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/invite-applicant-to-vacancy)

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
