# Errors and response codes

* [General errors](#general-errors)
* [System error](#system-errors)
* [Incorrect User-Agent](#user-agent)
* [Receiving/updating tokens](#oauth-get-errors)
* [Authorization use errors](#oauth)
* [Errors when accessing a paid method](#employer_payable_methods)
* [Errors of separate resources](#service-errors)
* [Saved resume searches](#resumes-saved-searches)
* [Negotiations (responses/invitations)](#negotiations)
* [Vacancy posting and editing](#vacancies-create-n-edit)
* [Vacancy prolongation](#vacancies-prolongate)
* [Employer's managers](#employer_managers)
* [Working with a resume](#resumes)
* [Manager work accounts](#manager-accounts)
* [The captcha requirement](#captcha_required)

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

More detail on the [User-Agent title](https://api.hh.ru/openapi/en/redoc#section/General-information/Request-requirements).

| HTTP code | type             | value       | description                         |
|-----------|------------------|-------------|-------------------------------------|
| 400       | bad_user_agent   | unset       | User-Agent title is not transferred |
| 400       | bad_user_agent   | blacklisted | User-Agent value in the black list  |


## Authorization errors

More detail on [authorization](authorization.md).

<a name="oauth-get-errors"></a>
### Description of errors while receiving/updating tokens

Description of the fields:

| Name | Type | Value   
|-----------|------------------|-------------|
| error | string | One of the values [described in RFC 6749](http://tools.ietf.org/html/rfc6749#section-5.2). For example, `invalid_request` if any of the required parameters were not transferred
| error_description | string | Additional description of the error

Below are some of the possible errors with descriptions.

<table>
<tr><th>HTTP code</th><th>error</th><th>error_description</th><th>описание</th></tr>
 <tr>
    <td rowspan=8>400</td>
    <td rowspan=8>invalid_request</td>
    <td>account not found</td>
    <td>This error can occur if an invalid client_id and client_secret pair was transferred</td>
</tr>
<tr>
    <td>account is locked</td>
    <td>User account is locked. The user must contact <a href="https://github.com/hhru/api/blob/master/docs_eng/README.md#feedback">the website support team</a></td>
</tr>
<tr>
    <td>password invalidated</td>
    <td>User account password is outdated. The user must restore the password on the website <a href="https://hh.ru">https://hh.ru</a></td>
</tr>
<tr>
    <td>login not verified</td>
    <td>User account is not verified. The user must contact <a href="https://github.com/hhru/api/blob/master/docs_eng/README.md#feedback">the website support team</a></td>
</tr>
<tr>
    <td>bad redirect url</td>
    <td>Invalid redirect_url was transferred</td>
</tr>
<tr>
    <td>token is empty</td>
    <td>refresh_token was not transferred</td>
</tr>
<tr>
    <td>token not found</td>
    <td>Invalid refresh_token was transferred</td>
</tr>
<tr>
    <td>code not found</td>
    <td>The transferred authorization_code was not found</td>
</tr>
 <tr>
    <td>400</td>
    <td>invalid_client</td>
    <td>client_id or client_secret not found</td>
    <td>The error can occur if this client_id was not found or has been deleted, or if an invalid client_secret was transferred</td>
</tr>
 <tr>
    <td rowspan=8>400</td>
    <td rowspan=8>invalid_grant</td>
    <td>token has already been refreshed</td>
    <td>The error occurs when trying to re-use the refresh token</td>
</tr>
<tr>
    <td>token not expired</td>
    <td>The error occurs when trying to update a valid access token. access token can be updated only after expiration</td>
</tr>
<tr>
    <td>token was revoked</td>
    <td>The token was revoked. For example, a token is revoked if the password has expired</td>
</tr>
<tr>
    <td>bad token</td>
    <td>An invalid token value was transferred</td>
</tr>
<tr>
    <td>code has already been used</td>
    <td>authorization_code has already been used (it can only be used once)</td>
</tr>
<tr>
    <td>code expired</td>
    <td>authorization_code expired</td>
</tr>
<tr>
    <td>code was revoke</td>
    <td>authorization_code was revoked (if the password has expired)</td>
</tr>
<tr>
    <td>token deactivated</td>
    <td>The token was deactivated. The token is deactivated if the user has changed the password</td>
</tr>
 <tr>
    <td>400</td>
    <td>unsupported_grant_type</td>
    <td>unsupported grant_type</td>
    <td>The error occurs if an invalid value in the grant_type field was transferred</td>
</tr>
 <tr>
    <td>403</td>
    <td>forbidden</td>
    <td>app token refresh too early</td>
    <td>The error occurs if the application token is requested more than once every five minutes</td>
</tr>
</table>


<a name="oauth"></a>
### Authorization use errors

In case you [make an authorized request](authorization.md#check-access_token) in
api and your authorization is not valid for any reason, an error with `type`
`oauth`, and, possibly, with one of the listed `values`, will be returned.

| HTTP code | type  | value                   | description  |
|-----------|-------|-------------------------|--------------|
| 403       | oauth | bad_authorization      | authorization token doesn't exist or is not valid |
| 403       | oauth | token_expired          | access_token validity period has expired, it is necessary to [refresh the access_token](https://api.hh.ru/openapi/en/redoc#tag/Employer-authorization/operation/authorize)  |
| 403       | oauth | token_revoked          | the token is revoked by the user, the application should [request a new authorization](authorization.md) |
| 403       | oauth | application_not_found  | your application has been deleted

<a name="employer_payable_methods"></a>
## Errors when accessing a paid method

In case you request a [paid method](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access) without buying access, the following error will be generated:

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

<a name="resumes-saved-searches"></a>
### Saved resume searches

In addition to the error code pertaining to
[the transfer of a saved resume search to another manager](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/move-saved-resume-search),
the following errors may return:

HTTP code | type | value | description
----------|------|-------|-----------
404 | saved_searches | saved_search_not_found | auto search not found or not owned by current user
404 | saved_searches | manager_not_found | invalid manager_id

<a name="artifacts"></a>
### Artifacts

When uploading artifacts, errors are possible, including:

HTTP code | type | value | description
----------|-----|--------|-----------
400 | bad_argument | file | file not specified, or several files specified
400 | bad_argument | type | incorrect parameter `type` value
400 | bad_argument | description | description too long
400 | artifacts | limit_exceeded | number of artifacts exceeded
400 | artifacts | image_too_large | file size exceeds the limit
400 | artifacts | unknown_format | unknown file format
403 | forbidden | — | insufficient access rights



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
403 | negotiations | chat_archived | action regarding a response/invitation can't be performed as response/invitation is archived


<a name="vacancies_favorited"></a>
### Favorited vacancies

When [adding to the list of selected vacancies](vacancies.md#favorited)
the following errors can be returned, in addition to the error code:

HTTP code | type | value | description
----------|------|-------|-----------
403 | vacancies_favorited | vacancy_archived | the vacancy is archived and cannot be added to the list of selected number of selected vacancies exceeds the limit
403 | vacancies_favorited | limit_exceeded | `authorization_code` has already been used (it can only be used once)


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
403 | vacancies | duplicate | a similar job has already been published; the [response](#vacancies-duplicate-response) contains information about duplicate jobs; this error can be disabled by force (when [adding](employer_vacancies.md#creation) or [editing](employer_vacancies.md#edit-ignore-duplicates))
403 | vacancies | creation_forbidden | jobs cannot be published by the current manager
403 | vacancies | unavailable_for_archived | you cannot edit an archived job
403 | vacancies | conflict_changes | a conflict was detected between changes to the job's data ([read more](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/edit-vacancy))

#### Reasons for errors

reason | description 
-------|---------
is_empty | empty value
wrong_size | wrong value size
is_too_short | value size is too small
is_too_long | value size is too big
currency_code_is_invalid | the salary currency is incorrect
chosen_area_is_not_a_leaf_or_not_exist | the vacancy location is incorrect or is not the final region (city, town)
email_in_description | the vacancy description contains an email
anonymous_vacancy_contains_address | an anonymous vacancy should not contain the employer's address
anonymous_vacancy_has_real_company_name | the vacancy title should not contain the employer's company name
only_for_anonymous_type | this action is only available for anonymous vacancies
address_is_disabled | address is unavailable
vacancy_type_employer_billing_type_mismatch | the vacancy type is incompatible with current billing type
only_for_direct_type | this action is only available for direct vacancies
address_is_empty_with_checked_show_metro_flag | empty address was entered together with an indication to show the metro station
address_has_no_metro_but_checked_show_metro_flag | a metro station is not available at the entered address, but the option to show the metro station is selected
default_vacancy_branded_template_is_invalid_or_not_enough_purchased_services | branded vacancy template is entered incorrectly, or you have not paid for the service allowing you to use a [branded vacancy template](https://hh.ru/price?from=menu#branding) 
department_code_prohibited_in_anonymous_vacancy | you cannot specify a department code for an anonymous vacancy
branded_template_prohibited_in_anonymous_vacancy | you cannot use a branded template for an anonymous vacancy
value_conflict_with_business_rules | you cannot use specified billing_type 

<a name="vacancies-duplicate-response"></a>
#### Example response on error duplicate

```json
{
    "errors": [
        {
            "type": "vacancies",
            "value": "duplicate",
            "found": 2,
            "items": [
                {
                    "id": 1337
                },
                {
                    "id": 78789890
                }
            ]
        }
    ]
}
```

### Response fields

Path | JSON type | Description
--- | --- | --------
found | number | total number of duplicate jobs
items | array | limited number of records with information about duplicates. Does not guarantee all duplicates will be returned.
items[].id | number | job id

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

In addition to [general errors](#general-errors), the following errors can be returned when [editing](employer_managers.md#edit) an employer's manager:

HTTP code | type | value | reason | description
----------|------|-------|--------|---------
400 | managers | *field_name* | | error in the *field_name* field
403 | managers | email | already_exist | a manager with this email address already exists
403 | managers |  | creation_limit_exceeded | the limit for creating managers has been reached
403 | managers | *field_name* | not_editable | the *field_name* field cannot be edited


<a name="resumes"></a>
### Working with a resume

In addition to [general errors](#general-errors),
the following errors can be returned when [getting](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume) or [updating](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/edit-resume) a resume:

HTTP code | type | value | description
----------|------|-------|---------
400 | bad_argument | with_contact | incorrect field value `with_contact`
400 | resumes | total_limit_exceeded | the allowed number of resumes is exceeded (this applies only to applicants)
429 | resumes | view_limit_exceeded | the allowed number of resume views is exceeded (this applies only to employers)
403 | resumes | quota_exceeded | resume viewing quota available to manager has been exceeded (applies to employers only)
403 | resumes | no_available_service | no sufficient services available to view resume
403 | resumes | cant_view_contacts | no contact viewing rights

In addition to the `type` and `value`, the returned error response body may contain a `description`, i.e., description of the events that give rise to the error in question.

<a name="vacancies_blacklist"></a>
### Adding hidden jobs to the list

In addition to [general errors](#general-errors), the following errors can be returned when [adding hidden jobs to the list](https://api.hh.ru/openapi/en/redoc#tag/Hidden-vacancies):

HTTP code | type | value | description
----------|------|-------|---------
400 | vacancies_blacklist | limit_exceeded | the allowed number of hidden jobs is exceeded
404 | vacancies_blacklist | not_found | the job to be added to the list has not been not found


<a name="employers_blacklist"></a>
### Adding hidden companies to the list

In addition to [general errors](#general-errors),
the following errors can be returned when [adding company's hidden jobs to the list](https://api.hh.ru/openapi/en/redoc#tag/Blacklisted-employers):

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

<a name="manager-accounts"></a>
### Manager work accounts
HTTP code | type | value | description
----------|------|-------|-----------
403 | manager_extra_accounts | manager_extra_account_not_found | Incorrect Account ID in the header
403 | manager_accounts | used_manager_account_forbidden | [Work Account is blocked](#manager-accounts-blocked)

<a name="manager-accounts-blocked"></a>
If User Account is blocked, the following error message will be generated:
```json
{
    "errors": [
    {
        "type": "manager_accounts",
        "value": "used_manager_account_forbidden",
        "allowed_accounts": [
            {
                "id": "1",
                "employer": {
                    "id": "12345678",
                    "name": "Alpha Corp."
                }
            },
            {
                "id": "2",
                "employer": {
                    "id": "87654321",
                    "name": "Beta Inc."
                }
            }
        ]
    }
  ]
}
```
where `allowed_accounts` contains an array of the accounts available for this token
Array elements are similar to the [result in the list of the Work Accounts](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/operation/get-manager-accounts)
<a name="captcha_required"></a>
### The captcha requirement

Some operations in API may be protected with a captcha.
It is clearly indicated in the resource description where the captcha test applies.
The following error is returned in this case :

```json
{
    "type": "captcha_required",
    "value": "captcha_required",
    "fallback_url": "https://hh.ru/account/connect/register....",
    "captcha_url": "https://hh.ru/account/captcha?state=..."
}
```

Name | Type | Description
--- | --- | ---
fallback_url | string or null | Address of the webpage where a similar operation can be completed (more often than not, the page itself is protected with a captcha)
captcha_url | string or null | Address of the webpage where to pass the captcha. Once the captcha is passed successfully, a similar request in API should also be completed successfully. The app is to add to `captcha_url` the required parameter `backurl`, to which the redirect will go after the captcha is passed. The `backurl` must always contain a schema, e.g., `https://`, or the app schema

One or the other of the `fallback_url` or `captcha_url` parameters may be absent, but both cannot be absent at the same time.

* `403 Forbidden` — captcha required (this will never come, unless the token has not been transmitted)

Additional description of the errors:

HTTP code | type | value | description
----------|------|-------|-----------
403 | captcha_required | captcha_required | [Learn more about captcha](errors.md#captcha_required)
