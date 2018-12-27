# HeadHunter API

[По-русски](../README.md) | **In english**

HeadHunter API lets you integrate [HeadHunter](https://hh.ru/) into your product.

First of all, read the [general information](general.md) on work with API and
the [requirements](https://dev.hh.ru/articles/logos) for logos and application
names use.

To use services that require user or application authorization, you should register the
application at [https://dev.hh.ru](https://dev.hh.ru) and set up the [authorization](authorization.md) process.

After registration, the application can request of hh.ru users permission to access their personal data without obtaining 
and storing their usernames and password.

> ‼️ Please note that as of July 16, 2018, access to some methods became [paid](employer_payable_methods.md) for employers.

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
  relevant for [paid](employer_payable_methods.md) methods for the employer, requires [user authorisation](authorization_for_user.md).


## Main
* [General information](general.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [API Service Terms of Use](https://dev.hh.ru/admin/developer_agreement) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Logo use requirements](https://dev.hh.ru/articles/logos) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Application name requirements](https://dev.hh.ru/articles/apps) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Authorization](authorization.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Caching](cache.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Errors and response codes](errors.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Paid access to some API methods for employers](employer_payable_methods.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

<a name="resources"></a>
<a name="context"></a>
### Context

* [Information on the authorised user or application](me.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Obtaining information on the authorised user](me.md#user-info) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Editing information on the authorised user](me.md#user-edit) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Obtaining information on the authorised application](me.md#application-info) <img src="http://hhru.github.io/api/badges/client.png" alt="client" />
* [Manager preferences](manager_settings.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Locales](locales.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Site choice](hosts.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resume"></a>
### CV

* [View a CV](resumes.md#item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Work with CVs for an applicant](resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [List of CVs for current user](resumes.md#mine) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV creation & editing](resumes.md#create_edit) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV publication & prolongation](resumes.md#publish) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Deleting a resume](resumes.md#delete) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV view history](resumes.md#views) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Information on a resume's status and readiness for publication](resumes.md#status-and-publication) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Resume visibility lists](resume_visibility.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Artifacts (photos, portfolio)](artifacts.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Search for vacancies similar to the CV](resumes.md#similar) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [History of responses/invitations for a resume](resume_negotiations_history.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

<a name="vacancies"></a>
### Vacancies

* [Receiving vacancies](vacancies.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Search for vacancies](vacancies.md#search) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
    * [Clusters](clusters.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
    * [Description of the used parameters](vacancies_search_arguments.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [View a vacancy](vacancies.md#item) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Search for vacancies similar to the vacancy](vacancies.md#similar) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Favorite vacancies](vacancies.md#favorited) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Hidden vacancies](blacklisted.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Saved vacancy searches](saved_search.md#vacancies-saved-search-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Vacancies for the employer / manager](employer_vacancies.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy posting](employer_vacancies.md#creation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy editing](employer_vacancies.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy prolongation](employer_vacancies.md#prolongate) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Published vacancy list](employer_vacancies.md#active) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Storing vacancies](employer_vacancies.md#archive) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Archived vacancy list](employer_vacancies.md#archived) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleting vacancies](employer_vacancies.md#hide) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleted vacancy list](employer_vacancies.md#hidden) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Vacancy statistics](employer_vacancies.md#stats) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="applicants"></a>
### Applicants

* [Applicant comments](applicant_comments.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />


<a name="employers"></a>
### Employers / companies

* [Company search](employers.md#search) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [View an employer/company](employers.md#item) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="employer_managers"></a>
### Employer's managers

* [Managers](employer_managers.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Adding a manager](employer_managers.md#add) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Editing a manager](employer_managers.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleting a manager](employer_managers.md#delete) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Employer's manager directory](employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Getting information about a manager](employer_managers.md#item) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  

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
  * [List of resumes that can be used to apply for a given job](suitable_resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Resumes grouped by the possibility of responding to a given job](resumes_by_status.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Messaging for employers](employer_negotiations.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Processing model, terms and procedures](employer_negotiations.md#model) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [General description of processing responses/invitations](employer_negotiations.md#flow) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Collections and employer statuses for responses/invitations](employer_negotiations.md#collections) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [List of responses/invitation](employer_negotiations.md#negotiations-list) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [View the response/invitation](employer_negotiations.md#get-negotiation) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Work with messages in the response/invitation](employer_negotiations.md#get-messages) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Sending a message in the response/invitation](employer_negotiations.md#add-messages) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Inviting an applicant for a vacancy](employer_negotiations.md#add-invite) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Response/invitation actions (status change)](employer_negotiations.md#actions) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Message templates](negotiation_message_templates.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Assessments](assessment.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />


<a name="dictionaries"></a>
### Directories

* [Region directory](areas.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Specialization directory](specializations.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Metro directory](metro.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Language directory](languages.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Company branches](industries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Educational institutions](/educational_institutions.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Basic information about educational institutions](university.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of educational institution faculties](faculties.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Employer directories](employer_dictionaries.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Address directory](employer_addresses.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Types of managers and their rights](employer_managers.md#dict) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Employer's managers](employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Department directory](employer_departments.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Test directory](employer_tests.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of regions with active vacancies](employer_vacancy_areas_active.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of branded vacancy templates](employer_vacancy_branded_templates.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Key skills](/docs/key_skills.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Other directories](dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="suggests"></a>
### Suggestions (autosuggest, autocomplete)

* [Suggestions (autosuggest, autocomplete)](suggests.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by university](suggests.md#educational_institutions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by organization](suggests.md#companies) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by specialist area](suggests.md#specializations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by key skill](suggests.md#key-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by position](suggests.md#positions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by region](suggests.md#areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [by job search keyword](suggests.md#vacancy-search-keyword) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="salary"></a>
### Salary Database

* [Reports of the Salary Database](/docs/salary_reports.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Salary assessment without forecasts](/docs/salary_reports.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Salary Database Dictionaries](/docs/salary_dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Industries](/docs/salary_dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Competency levels](/docs/salary_dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Professions and specialist areas](/docs/salary_dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Regions and cities](/docs/salary_dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


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

