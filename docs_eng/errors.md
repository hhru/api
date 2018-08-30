# Errors and response codes

API extensively uses informing through HTTP response codes. The application must
process them correctly.

When an error occurs, the response body, besides the response code, will have an
additional information that helps the developer to learn the cause of the error.

All errors are displayed in the format:

```json
{
    "errors": [
        {
            "type": "...",
            "value": "..."
        }
    ]
}
```

Several errors can be returned at the same time. The `type` key is present in
each `errors` array object and contains a text identifier of the error class.
The `value` key is optional and provides more detail on the error.

> Apart from the `errors` described above, API can optionally return other keys
> left for backward compatibility. **It is not recommended to use them.**


<a name="general-errors"></a>
## General errors

If the requested resource can't be found, the
`404 Not Found` response will be returned and the `errors` array will have
the object:

```json
{
    "type": "not_found"
}
```

If there is an error in request parameters (e.g.
`GET https://api.hh.ru/vacancies/?employer_id=foo`) the
`400 Bad Request` response will be returned, and the error array will have
the object:

```json
{
    "type": "bad_argument",
    "value": "employer_id"
}
```

<a name="system-errors"></a>
## System error

If the service can't process the request at the moment, but understood it
correctly, the `503 Service Unavailable` response will be returned and `type`
will contain `service_unavailable`.

In case of unforeseen situation, API will return 500.

In rare cases errors with 5** codes can be returned with the body that doesn't
contain the valid json. In such a case the application should rely only on the
response code.


## General request errors

<a name="user-agent"></a>
### Incorrect User-Agent

More detail on the [User-Agent title](general.md#request-requirements).

| HTTP code | type             | value       | description                         |
|-----------|------------------|-------------|-------------------------------------|
| 400       | bad_user_agent   | unset       | User-Agent title is not transferred |
| 400       | bad_user_agent   | blacklisted | User-Agent value in the black list  |


## Authorization errors

More detail on [authorization](authorization.md).


<a name="oauth"></a>
### Authorization use errors

In case you [make an authorized request](authorization.md#check-access_token) in
api and your authorization is not valid for any reason, an error with `type`
`oauth`, and, possibly, with one of the listed `values`, will be returned.

| HTTP code | type  | value                   | description  |
|-----------|-------|-------------------------|--------------|
| 403       | oauth | bad_authorization      | authorization token doesn't exist or is not valid |
| 403       | oauth | token_expired          | access_token validity period has expired, it is necessary to [refresh the access_token](authorization.md#refresh_token)  authorization.md#refresh_token |
| 403       | oauth | token_revoked          | the token is revoked by the user, the application should [request a new authorization](authorization.md) |
| 403       | oauth | application_not_found  | your application has been deleted


### Errors when accessing a paid method

In case you request a [paid method](employer_payable_methods.md) without buying access, the following error will be generated:

HTTP code | type | value | description
----------|------|-------|-----------
403 | api_access_payment | action_must_be_payed | You have requested a paid method without buying access

<a name="service-errors"></a>
## Errors of separate resources

If the service can return more detailed information on the
error, it will be given in the response body. In this case the response code
will likely be 400, 403, 409, 429, but other codes are also possible.

At the least, the application should process HTTP response statuses correctly.
To facilitate the work with the application, it is recommended to also process
the response type that has come. The tables listed below contain an incomplete
error list; it can be extended.


<a name="artifacts"></a>
### Artifacts

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/errors.md.html#artifacts)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).



<a name="negotiations"></a>
### Negotiations (responses/invitations)

In addition to [general errors](#general-errors), the following errors may be
returned:

HTTP code| type| value| description
----------|------|-------|-----------
403 | negotiations | invalid_vacancy | the vacancy from the response/invitation was archived or hidden
400 / 403 | negotiations | resume_not_found | the CV from the response/invitation was hidden or deleted, or not found
400 / 403 | negotiations | limit_exceeded | the limit on the responses/invitations number was exceeded
403 | negotiations | wrong_state | the action on the response/invitation in this status is impossible
403 | negotiations | empty_message | the empty message text was sent
403 | negotiations | too_long_message | the too long message text was sent
403 | negotiations | address_not_found | the address sent for the action does not exist or belongs to another employer
403 | negotiations | not_enough_purchased_services | the required paid services are not available, this usually refers to [access to the resume database](https://hh.ru/price#dbaccess)
403 | negotiations | not_enough_purchased_services | the paid services are insufficient, usually [CV database service](https://hh.ru/price#dbaccess)
403 | negotiations | in_a_row_limit | the number of successive messages is exceeded; the opponent must reply to the message in order the employer is able to send new messages
403 | negotiations | overall_limit | messages limit exceeded
403 | negotiations | no_invitation | negotiations are unavailable as there was no invitation in the response
403 | negotiations | message_cannot_be_empty | negotiation message cannot be empty
403 | negotiations | disabled_by_employer | negotiation by response is disabled by the employer
403 | negotiations | resume_deleted | the message can't be sent as the CV referenced in the response is deleted or hidden
403 | negotiations | archived | the message can't be sent as the vacancy referenced in the response is archived


<a name="vacancies_favorited"></a>
### Favorited vacancies

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/errors.md.html#vacancies_favorited)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="vacancies-create-n-edit"></a>
### Vacancy posting and editing

In addition to an error code, the following errors may be returned when
[posting](employer_vacancies.md#creation) and
[editing](employer_vacancies.md#edit) a vacancy:

HTTP code| type| value| description
----------|------|-------|---------
400 | vacancies | *field_name* | the is an error in a job's field, where the *field_name* is the key of the upper level field and the reason field may be missing
403 | vacancies | not_enough_purchased_services | the purchased services are not enough to publish or update this type of job
403 | vacancies | quota_exceeded | the manager's quota for the publication of this type of job is exhausted
403 | vacancies | duplicate | a similar job has already been published; this error can be disabled by force (when [adding](employer_vacancies.md#creation-ignore-duplicates) or [editing](employer_vacancies.md#edit-ignore-duplicates))
403 | vacancies | creation_forbidden | jobs cannot be published by the current manager
403 | vacancies | unavailable_for_archived | you cannot edit an archived job
403 | vacancies | conflict_changes | a conflict was detected between changes to the job's data ([read more](employer_vacancies.md#edit_more))
403 | vacancies | can_not_accept_kids | you can't publish jobs to search for applicants with a minimum age of 14 ([read more](employer_vacancies_accept_kids.md#accept-kids))


<a name="vacancies-prolongate"></a>
### Vacancy extension

In addition to the error code, the following errors can be returned when [extending](employer_vacancies.md#prolongate) a job:

HTTP code | type | value | description
----------|------|-------|---------
403 | vacancies | not_enough_purchased_services | the purchased services are insufficient for prolongation of this type of vacancy
403 | vacancies | quota_exceeded | the manager's quota for posting of this type of vacancies has been exceeded
403 | vacancies | prolongation_forbidden | extension of vacancies is unavailable for the current manager
403 | vacancies | unavailable_for_archived | extension of vacancies is unavailable for the archived vacancy
403 | vacancies | too_early | premature extension


<a name="employer_managers"></a>
### Employer's managers

In addition to [general errors](#general-errors), the following errors can be returned when [adding](employer_managers.md#add)
and [editing](employer_managers.md#edit) an employer's manager:

HTTP code | type | value | reason | description
----------|------|-------|--------|---------
400 | managers | *field_name* | | error in the *field_name* field
403 | managers | email | already_exist | a manager with this email address already exists
403 | managers |  | creation_limit_exceeded | the limit for creating managers has been reached
403 | managers | *field_name* | not_editable | the *field_name* field cannot be edited


<a name="resumes"></a>
### Working with a resume

In addition to [general errors](#general-errors),
the following errors can be returned when [getting](resumes.md#item) or [updating](resumes.md#create_edit) a resume:

HTTP code | type | value | description
----------|------|-------|---------
400 | resumes | total_limit_exceeded | the allowed number of resumes is exceeded (this applies only to applicants)
429 | resumes | view_limit_exceeded | the allowed number of resume views is exceeded (this applies only to employers)


<a name="vacancies_blacklist"></a>
### Adding hidden jobs to the list

In addition to [general errors](#general-errors), the following errors can be returned when [adding hidden jobs to the list](blacklisted.md#vacancies):

HTTP code | type | value | description
----------|------|-------|---------
400 | vacancies_blacklist | limit_exceeded | the allowed number of hidden jobs is exceeded
404 | vacancies_blacklist | not_found | the job to be added to the list has not been not found


<a name="employers_blacklist"></a>
### Adding hidden companies to the list

In addition to [general errors](#general-errors),
the following errors can be returned when [adding company's hidden jobs to the list](blacklisted.md#employers):

HTTP code | type | value | description
----------|------|-------|---------
400 | employers_blacklist | limit_exceeded | the allowed number of hidden jobs is exceeded
404 | employers_blacklist | not_found | the job to be added to the list has not been not found


<a name="resume-visibility-lists"></a>
### Resume visibility lists

<a name="resume-visibility-lists-get"></a>
#### Getting visibility lists

HTTP code | type | value | description
----------|------|-------|---------
400 | bad_argument | per_page | an invalid number of items per page was passed (the maximum value is 100)

<a name="resume-visibility-lists-add"></a>
#### Adding companies to the list

HTTP code | type | value | description
----------|------|-------|---------
400 | resume_visibility_list | unknown_employer | an unknown employer ID was passed
400 | resume_visibility_list | limit_exceeded | visibility list limit exceeded
400 | resume_visibility_list | too_many_employers | too many employers were passed

<a name="resume-visibility-lists-remove"></a>
#### Removing companies from the list

HTTP code | type | value | описание
----------|------|-------|---------
400 | bad_argument | id | an invalid employer ID was passed
400 | resume_visibility_list | too_many_employers | too many employers were passed

<a name="bulk-request"></a>
#### bulk request

HTTP code | type | value | reason | описание
----------|------|-------|---------|---------
400 | bad_argument | id | too_many_bulk_items | too many IDs
400 | bad_argument | id | | an invalid ID was passed
