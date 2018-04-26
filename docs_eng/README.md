# HeadHunter API

[По-русски](../README.md) | **In english**

HeadHunter API is a free toolset for integration of
[HeadHunter](https://hh.ru/) with your product.

First of all, read the [general information](general.md) on work with API and
the [requirements](https://dev.hh.ru/articles/logos) for logos and application
names use.

To use services that require user authorization, you should register the
application at [https://dev.hh.ru](https://dev.hh.ru) and set up the
[authorization](authorization.md) process.


<a name="content"></a>
## Content

Article labels:

* <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> –
  for anonymous requests, authrization isn't required.
* <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> –
  for applicant requests, authrization is required.
* <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" /> –
  for employer requests, authrization is required.


<a name="general"></a>
### General information
* [General information](general.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [API Service Terms of Use](https://dev.hh.ru/admin/developer_agreement) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Logo use requirements](https://dev.hh.ru/articles/logos) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Application name requirements](https://dev.hh.ru/articles/apps) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Authorization](authorization.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Errors and response codes](errors.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resources"></a>
<a name="context"></a>
### Context

* [Current user](me.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Manager preferences](manager_settings.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Locales](locales.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Site choice](hosts.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resume"></a>
### CV

* [View a CV](resumes.md#item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Work with CVs for an applicant](resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [List of CVs for current user](resumes.md#mine) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV creation & editing](resumes.md#create_edit) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV publication & prolongation](resumes.md#publish) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [CV view history](resumes.md#views) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Artifacts (photos, portfolio)](artifacts.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Search for vacancies similar to the CV](resumes.md#similar) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />

<a name="vacancies"></a>
### Vacancies

* [Receiving vacancies](vacancies.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Search for vacancies](vacancies.md#search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [View a vacancy](vacancies.md#item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Search for vacancies similar to the vacancy](vacancies.md#similar) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Favorite vacancies](vacancies.md#favorited) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Hidden vacancies](blacklisted.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Vacancy seaved searches (autosearches)](saved_search.md#vacancies-saved-search-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Vacancies for the employer / manager](employer_vacancies.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy posting](employer_vacancies.md#creation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy editing](employer_vacancies.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Vacancy prolongation](employer_vacancies.md#prolongate) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Published vacancy list](employer_vacancies.md#active) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Storing vacancies](employer_vacancies.md#archive) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Archived vacancy list](employer_vacancies.md#archived) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleting vacancies](employer_vacancies.md#hide) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Deleted vacancy list](employer_vacancies.md#hidden) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="applicants"></a>
### Applicants

* [Applicant comments](applicant_comments.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="employers"></a>
### Employers / companies

* [Company search](employers.md#search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [View an employer/company](employers.md#item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="negotiations"></a>
### Messaging (applications/invitations)

* [Messaging for applicants](negotiations.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Receiving the list of responses](negotiations.md#get_negotiations) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Respond to the vacancy](negotiations.md#post_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [View the response/invitation](negotiations.md#get_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [View the list of messages in the response](negotiations.md#get_messages) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Sending new message](negotiations.md#send_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Suitable CVs for application on a concrete vacancy](suitable_resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Messaging for employers](employer_negotiations.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Processing model, terms and procedures](employer_negotiations.md#model) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [General description of processing responses/invitations](employer_negotiations.md#flow) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Collections and employer statuses for responses/invitations](employer_negotiations.md#collections) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of responses/invitation](employer_negotiations.md#negotiations-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [View the response/invitation](employer_negotiations.md#get-negotiation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Work with messages in the response/invitation](employer_negotiations.md#get-messages) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Inviting an applicant for a vacancy](employer_negotiations.md#add-invite) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Response/invitation actions (status change)](employer_negotiations.md#actions) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Message templates](negotiation_message_templates.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Assessments](assessment.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="dictionaries"></a>
### Directories

* [Region directory](areas.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Specialization directory](specializations.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Metro directory](metro.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Language directory](languages.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Company branches](industries.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Employer directories](employer_dictionaries.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Address directory](employer_addresses.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Manager directory](employer_managers.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Department directory](employer_departments.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Test directory](employer_tests.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of regions with active vacancies](employer_vacancy_areas_active.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [List of branded vacancy templates](employer_vacancy_branded_templates.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Other directories](dictionaries.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="suggests"></a>
### Suggestions (autosuggest, autocomplete)

* [Suggestions (autosuggest, autocomplete)](suggests.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [University name suggestions](suggests.md#educational_institutions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Organization suggestions](suggests.md#companies) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Specialization suggestions](suggests.md#specializations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Key skills suggestions](suggests.md#key-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Position suggestions](suggests.md#positions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Region tips](suggests.md#areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Tips for vacancy search key words](suggests.md#vacancy-search-keyword) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="feedback"></a>
## Support, feedback, news

Stay in touch with us via twitter [@apihhru](https://twitter.com/apihhru) or
email api@hh.ru.

If you found a bug in HeadHunter API or
[widgets](https://dev.hh.ru/admin/widgets), please look at
[issues](https://github.com/hhru/api/issues). We probably know and are fixing it
already. If we don't, it's better to report the bug there. There you can also
leave your wishes and suggestions.

You can follow the news by [commits](https://github.com/hhru/api/commits/master)
in this repository. [RSS](https://github.com/hhru/api/commits/master.atom).
