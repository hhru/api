# HeadHunter API

[По-русски](../README.md) | **In english**

HeadHunter API lets you integrate [HeadHunter](https://hh.ru/) into your product.

First of all, read the [general information](https://api.hh.ru/openapi/en/redoc#section/General-information) on work with API and
the [requirements](https://dev.hh.ru/articles/logos) for logos and application
names use.

To use services that require user or application authorization, you should register the
application at [https://dev.hh.ru](https://dev.hh.ru) and set up the [authorization](authorization.md) process.

After registration, the application can request of hh.ru users permission to access their personal data without obtaining 
and storing their usernames and password.
>‼️ Please note that the methods for handling response/invitation messages on behalf of the [applicant](negotiations.md#get_messages) and 
> [employer manager](employer_negotiations.md#get-messages) are deprecated and the new chat capabilities will not be supported in these methods. As such, correspondence may not display correctly.

> ‼️ Note the [description](./payable/resume.md) of the new resume database management model.
> The employer has to [pay](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access) for access to some methods .

## [OpenAPI](https://api.hh.ru/openapi/en/redoc)

[OpenAPI](https://api.hh.ru/openapi/en/redoc) documentation will be complemented.  
Methods are defined in OpenAPI have relevant links.

Specification HeadHunter API: [openapi.yml](https://api.hh.ru/openapi/specification/public/en).

<a name="content"></a>
## Content

Article labels:

* <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> –
  for anonymous requests, authrization isn't required.
* <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> –
  for anonymous requests, requires [application authorisation](authorization_for_application.md).
* <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> –
  for applicant requests, requires [user authorisation](authorization_for_user.md).
* <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" /> –
  relevant for free methods for the employer, requires [user authorisation](authorization_for_user.md).
* <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> –
  relevant for [paid](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access) methods for the employer, requires [user authorisation](authorization_for_user.md).

## Main
* [General information](https://api.hh.ru/openapi/en/redoc#section/General-information) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [API Service Terms of Use](https://dev.hh.ru/admin/developer_agreement) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Logo use requirements](https://dev.hh.ru/articles/logos) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Application name requirements](https://dev.hh.ru/articles/apps) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Authorization](authorization.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Caching](cache.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Errors and response codes](errors.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Paid access to some API methods for employers](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [New resume database management model (supported by API)](./payable/resume.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resources"></a>
<a name="context"></a>
### Context

* Information on the authorised user or application <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Obtaining information on the authorised applicant](https://api.hh.ru/openapi/en/redoc#tag/Applicant-info/operation/get-current-user-info) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> 
  * [Obtaining information on the authorised employer manager](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-current-user-info) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Obtaining information on the authorised application](https://api.hh.ru/openapi/en/redoc#tag/Application-info/operation/get-current-user-info) <img src="http://hhru.github.io/api/badges/client.png" alt="client" />
  * [Editing information on the authorised user](https://api.hh.ru/openapi/en/redoc#tag/Applicant-info/operation/edit-current-user-info) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* Manager details
  * [Manager work accounts](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/operation/get-manager-accounts) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Manager preferences](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/operation/get-manager-settings) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Information on active API services for paid methods](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-actions) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Locales](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-locales) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [CV locales](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-locales-for-resume) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Site choice](https://api.hh.ru/openapi/en/redoc#section/General-information/Host-selection) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="webhook"></a>
### [Webhook API](https://api.hh.ru/openapi/en/redoc#tag/Webhook-API)

* [The list of notifications that the user is subscripted](https://api.hh.ru/openapi/en/redoc#tag/Webhook-API/operation/get-webhook-subscriptions) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Subscription to notifications](https://api.hh.ru/openapi/en/redoc#tag/Webhook-API/operation/post-webhook-subscription) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Delete a subscription on notifications](https://api.hh.ru/openapi/en/redoc#tag/Webhook-API/operation/cancel-webhook-subscription) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Change a subscription on notifications](https://api.hh.ru/openapi/en/redoc#tag/Webhook-API/operation/change-webhook-subscription) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resume"></a>
### CV

* [View a CV](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* Work with CVs for an applicant <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CVs for an applicant. Phone](https://api.hh.ru/openapi/en/redoc#tag/CVs-for-an-applicant)
  * [List of CVs for current user](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-mine-resumes) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [View a CV](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV creation](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/create-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV editing](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/edit-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV publication & prolongation](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Publication/operation/publish-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Cloning a resume](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/create-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Deleting a resume](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/delete-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV view history](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume-view-history) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Information on a resume's status and readiness for publication](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-information/operation/get-resume-status) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Checking for the ability to create a resume](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Creating-and-updating/operation/get-resume-creation-availability) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Conditions to fill in the fields of a resume](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-resume-conditions) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Resume visibility lists](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Getting visibility lists](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists/operation/get-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Retrieving a list of resume visibility types](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists/operation/get-resume-access-types) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Adding companies to the visibility list](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists/operation/add-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Removing companies from the visibility list](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists/operation/delete-employer-from-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Clearing the visibility list](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists/operation/delete-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Searching for employers to add to the visibility list](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists/operation/get-resume-visibility-employers-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Search for CV](https://api.hh.ru/openapi/en/redoc#tag/Resume-search/operation/search-for-resumes) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Saved CV search](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [List of saved CV searches](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/get-saved-resume-searches) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Getting single saved CV search](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/get-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Creating new saved resume search](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/create-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Updating saved resume search](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/update-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Deleting saved resume search](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/delete-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Moving saved resume search to other manager](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/move-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Artifacts (photos, portfolio)](https://api.hh.ru/openapi/en/redoc#tag/Artifact-managing) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Search for vacancies similar to the CV](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [History of responses/invitations for a resume](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-resume-negotiations-history) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

<a name="vacancies"></a>
### Vacancies

* [Receiving vacancies](vacancies.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Search for vacancies](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/operation/get-vacancies) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
    * [Clusters](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/Clusters-of-vacancy-search) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [View a vacancy](vacancies.md#item) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Search for vacancies similar to the vacancy](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/operation/get-vacancies-similar-to-vacancy) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Favorite vacancies](vacancies.md#favorited) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Hidden vacancies](https://api.hh.ru/openapi/en/redoc#tag/Hidden-vacancies) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Blacklisted employers](https://api.hh.ru/openapi/en/redoc#tag/Blacklisted-employers) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Saved vacancy searches](https://api.hh.ru/openapi/en/redoc#tag/Saved-vacancy-searches/operation/get-saved-vacancy-searches) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [List of saved vacancy searches](https://api.hh.ru/openapi/en/redoc#tag/Saved-vacancy-searches/operation/get-saved-vacancy-searches) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Obtaining single saved vacancy search](https://api.hh.ru/openapi/en/redoc#tag/Saved-vacancy-searches/operation/get-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Creating new saved vacancy search](https://api.hh.ru/openapi/en/redoc#tag/Saved-vacancy-searches/operation/create-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Updating saved vacancy search](https://api.hh.ru/openapi/en/redoc#tag/Saved-vacancy-searches/operation/update-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Deleting saved vacancy search](https://api.hh.ru/openapi/en/redoc#tag/Saved-vacancy-searches/operation/delete-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Vacancies for the employer / manager](employer_vacancies.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Possible options available to current manager for publishing of vacancies](employer_vacancies.md#available_types) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy posting](employer_vacancies.md#creation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy editing](employer_vacancies.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy prolongation](employer_vacancies.md#prolongate) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Published vacancy list](employer_vacancies.md#active) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Storing vacancies](employer_vacancies.md#archive) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Archived vacancy list](employer_vacancies.md#archived) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleting vacancies](employer_vacancies.md#hide) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleted vacancy list](employer_vacancies.md#hidden) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [List of vacancy upgrades](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-vacancy-upgrade-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Vacancy statistics](employer_vacancies.md#stats) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Vacancy visitors](employer_vacancies.md#visitors) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Vacancy drafts](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Getting a list of vacancy drafts](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft/operation/get-vacancy-draft-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleting a draft](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft/operation/delete-vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Creating vacancy draft](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft/operation/create-vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Publishing a vacancy from draft](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft/operation/publish-vacancy-from-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
<a name="applicants"></a>
### Applicants

* [Applicant comments](https://api.hh.ru/openapi/en/redoc#tag/Applicant-comments) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Info on current authorized user](https://api.hh.ru/openapi/en/redoc#tag/Applicant-info/operation/get-current-user-info) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Editing information on the authorized user](https://api.hh.ru/openapi/en/redoc#tag/Applicant-info/operation/edit-current-user-info) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />

<a name="employers"></a>
### Employers / companies

* [Company search](https://api.hh.ru/openapi/en/redoc#tag/Employer/operation/search-employer) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [View an employer/company](https://api.hh.ru/openapi/en/redoc#tag/Employer/operation/get-employer-info) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Employer services](https://api.hh.ru/openapi/en/redoc#tag/Employer-services) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Employer info](https://api.hh.ru/openapi/en/redoc#tag/Employer-info) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Employer managers](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="employer_managers"></a>
### Employer's managers

* [Managers](employer_managers.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Adding a manager](employer_managers.md#add) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Editing a manager](employer_managers.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleting a manager](employer_managers.md#delete) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Employer's manager directory](employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Getting information about a manager](employer_managers.md#item) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Manager's limits ](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/operation/get-employer-manager-limits) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  

<a name="negotiations"></a>
### Messaging (applications/invitations)

* [Messaging for applicants](negotiations.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Receiving the list of responses](negotiations.md#get_negotiations) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Getting a list of active responses](negotiations.md#get_negotiations_active) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Respond to the vacancy](negotiations.md#post_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [View the response/invitation](negotiations.md#get_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Hide a response](negotiations.md#hide_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [View the list of messages in the response](negotiations.md#get_messages) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Sending new message](negotiations.md#send_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Editing a message in a response](negotiations.md#edit_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* Resume to apply for a given job <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [List of resumes that can be used to apply for a given job](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-suitable-resumes) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Resumes grouped by the possibility of responding to a given job](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resumes-by-status) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Messaging for employers](employer_negotiations.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Processing model, terms and procedures](employer_negotiations.md#model) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [General description of processing responses/invitations](employer_negotiations.md#flow) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Collections and employer statuses for responses/invitations](employer_negotiations.md#collections) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [List of responses/invitation](employer_negotiations.md#negotiations-list) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [View the response/invitation](employer_negotiations.md#get-negotiation) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Work with messages in the response/invitation](employer_negotiations.md#get-messages) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Sending a message in the response/invitation](employer_negotiations.md#add-messages) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Inviting an applicant for a vacancy](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-management/operation/get-active-vacancy-list) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Response/invitation actions (status change)](employer_negotiations.md#actions) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Mark responses as read](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/post-negotiations-topics-read) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Message templates](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-negotiation-message-templates) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Edit a template for response to an applicant](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/put-mail-templates-item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Assessments](assessment.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />


<a name="dictionaries"></a>
### Directories

* [Directories in OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Public-directories) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Region directory](areas.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Professional roles](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-professional-roles-dictionary) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Metro directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-metro-stations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Language directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-languages) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Company branches](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-industries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Educational institutions](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-educational-institutions-dictionary) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Basic information about educational institutions](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-educational-institutions-dictionary) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of educational institution faculties](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-faculties) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Employer directories](employer_dictionaries.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Address directory](https://api.hh.ru/openapi/en/redoc#tag/Employer-addresses) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Types of managers and their rights](employer_managers.md#dict) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Employer's managers](employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Department directory](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-employer-departments) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Test directory](https://api.hh.ru/openapi/en/redoc#tag/Employer-directories/operation/get-tests-dictionary) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of regions with active vacancies](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-employer-vacancy-areas) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of branded vacancy templates](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-vacancy-branded-templates-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Key skills](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Other directories](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="suggests"></a>
### Suggestions (autosuggest, autocomplete)

* [Suggestions (autosuggest, autocomplete)](suggests.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by university](suggests.md#educational_institutions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by organization](suggests.md#companies) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by specialist area](suggests.md#specializations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by key skill](suggests.md#key-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by resume position](suggests.md#resume-positions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by region](suggests.md#areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by job search keyword](suggests.md#vacancy-search-keyword) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="salary"></a>
### Salary Database

* [Reports of the Salary Database](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Salary assessment without forecasts](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database/operation/get-salary-evaluation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Salary Database Dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Industries](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-industries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Competency levels](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-employee-levels) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Professions and specialist areas](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-professional-areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Regions and cities](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-salary-areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="feedback"></a>
## Support, feedback, news

Stay in touch with us via twitter [@apihhru](https://twitter.com/apihhru) or
email api@hh.ru.

If you found a bug in HeadHunter API or
[widgets](https://dev.hh.ru/admin/widgets), please look at
[issues](https://github.com/hhru/api/issues). We probably know and are fixing it
already. If we don't, it's better to report the bug there. There you can also
leave your wishes and suggestions.

If you found a bug in HeadHunter site,
[contact website support](https://hh.ru/feedback) or
[the support community](https://feedback.hh.ru/).

You can follow the news by [commits](https://github.com/hhru/api/commits/master)
in this repository. [RSS](https://github.com/hhru/api/commits/master.atom).
