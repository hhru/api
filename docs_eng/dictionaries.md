# Directories

> Attention! The values in the directories may change at any time. Do not address them directly.

`GET /dictionaries` returns the object with the directories of fields and entities used in our service.
Most often, each directory consists of a list of objects containing an `id` and a `name`.

Example: [https://api.hh.ru/dictionaries?locale=EN](https://api.hh.ru/dictionaries?locale=EN)

<a name="resume"></a>
## Directories for fields used in CVs

* `education_level` - education
* `gender` - gender
* `language_level` - language level
* `preferred_contact_type` - preferred method of communication
* `relocation_type` - willingness to relocate
* `travel_time` - travel time to work
* `resume_access_type` - CV access level
* `business_trip_readiness` - willingness to travel
* `resume_contacts_site_type` - website type in the "contacts" field
* `resume_status` - CV status
* `resume_moderation_note` - moderator's comment
* `driver_license_types` — driver license types
* `resume_hidden_fields` — resume fields that can be [hidden](resumes.md#hidden-fields)


## Directories for vacancy fields

* `employment` - employment type
* `experience` - work experience
* `schedule` - work schedule
* `vacancy_type` - vacancy type
* `vacancy_label` - vacancy tags
* `vacancy_relation` - types of vacancy connection to the user
* `vacancy_billing_type` - vacancy placement options with relation to billing
* `working_days` - working days
* `working_time_intervals` - working time intervals
* `working_time_modes` - working time modes


## Directories for vacancy search parameters

* `vacancy_search_fields` - vacancy search field
* `vacancy_search_order` - vacancy sorting type
* `vacancy_cluster` - cluster type


## Directories for sorting employer's vacancies

* `employer_active_vacancies_order` - sorting type of the published vacancy list
* `employer_archived_vacancies_order` - sorting type of the archived vacancy list

<a name="negotiations"></a>
## Directories for applications and invitations (messaging)

* `negotiations_order` - application display order types
* `negotiations_state` - application state types
* `messaging_status` - status of the message sending possibility in messaging
* `negotiations_participant_type` - types of messaging participants

<a name="etc"></a>
## Other directories

* `currency` - currency directory
* `employer_type` - employer type
* `employer_relation` - methods of contacting applicants
* `applicant_comments_order` - sorting type of the 
  [applicant comment list](applicant_comments.md#list)
* `vacancy_not_prolonged_reason` – the reasons why 
  [prolongation](employer_vacancies.md#prolongate-info) not available

Each list item contains the following fields:

Name | Type | Description
----|-----|---------
id | string | Id
name | string | Name

List item of element `currency` contains the following fields:

Name | Type | Description
----|-----|---------
code | string | Code
abbr | string | Short designation
name | string | Name
default | boolean | Is it used as default currency
rate | int | Course against ruble
in_use | boolean | Can I use on this host?
