# CV

* [List of CVs for current user](#mine)
* [View a CV](#item)
  * [Additional fields for the resume publisher](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
  * [Resume-related paid services for the resume publisher](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
  * [Additional fields for the employer](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
  * [Resume-related paid services for the resume publisher (field paid_services)](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume)
* [Creating and editing a resume](#create_edit)
* [Publishing a resume](#publish)
* [Information on a resume's status and readiness for publication](#status-and-publication)
* [Cloning a resume](#clone)
* [Deleting a resume](#delete)
* [Checking for the ability to create a resume](#availability)
* [Conditions to fill in the fields of a resume](#conditions)
  * [Conditions to fill in the fields of a new resume](#init-conditions)
  * [Conditions for contacts in a resume](#conditions-contacts)
  * [Additional rules for resume fields](#conditions-other)
* [Resume abstract](#resume-nano)
* [Resume summary](#resume-short)
* [Resume download links](#download-links)
* [CV status](#status)
* [CV access type](#access_type)
  * [Resume visibility lists](#visibility_lists)
  * [Retrieving a list of resume visibility types](#get_access_types)
* [Resume viewing history](#views)
* [Searching for jobs similar to a resume](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume)
* [CV hidden fields](#hidden-fields)


<a name="mine"></a>
## List of CVs for current user

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-mine-resumes)

<a name="item"></a>
## View a CV

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](/docs_eng/payable/employer_payable_methods.md)

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume)

<a name="create_edit"></a>
## Creating and editing a resume

`POST /resumes` — adding a resume

`PUT /resumes/{resume_id}` — editing an existing resume. JSON of the same format as sent for a GET request
                             is used as a request body. In this case, only id of transferred data is used
                             for the fields with the directory data from the transferred JSON structure. 
                             For example, in a resume, in the languages field, Russian is indicated as the native language:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Russian",
            "level": {
                "id": "native",
                "name": "native"
            }
        }
     ]
   }
```

To add English with "B2 - upper intermediate" level send the following JSON:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Russian",
            "level": {
                "id": "l1",
                "name": "native"
            }
        },
        {
            "id": "eng",
            "level": {
                "id": "b2"
            }
        }
    ]
  }
```

The first element is Russian, which we already have in languages, the second is
the new element, English, that we want to add. Fields `language.name` and
`language.level.name` in this case are not in the way but also do not carry useful information.

Sending data replaces existing data for the selected parameter.
Each parameter can be sent separately.

<a name="resume-keys"></a>
> Also, read the rules for filling the fields in the [Conditions to fill in the fields of a resume](#conditions)

<a name="resume-edit-params"></a>
Parameters:

* `last_name` — second name;
* `first_name` — first name;
* `middle_name` — middle name;
* `birth_date` — date of birth (YYYY-MM-DD);
* `gender` — gender. Directory entries [gender](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
* `photo` — user photo. see. [artifacts](https://api.hh.ru/openapi/en/redoc#tag/Artifact-managing);
* `portfolio` — user portfolio. see [artifacts](https://api.hh.ru/openapi/en/redoc#tag/Artifact-managing);
* `area` — place of residence. Directory entries [areas](areas.md);
* `metro` — nearest metro station. Directory entries [metro](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-metro-stations). If you submit a metro station that does not exist in submitted area, the field will be ignored;
  It makes sense to show only for `area` with metro;
* `relocation` — possible relocation. Consists of the fields:
    * `type` — Directory entries [relocation_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
    * `area` — relocation city (list). Makes sense only with the corresponding `type` field. Directory entries
      [areas](areas.md);
* `business_trip_readiness` — agree to go on business trips. Directory entries
  [business_trip_readiness](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
* `contact` — contact info (list). 
Mandatory of the contact fields see in [conditions to fill in the fields of a resume](#conditions)
Consists of the fields:
    * `type` — Directory entries [preferred_contact_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
    * `value` — contact value. For phone number, consists of four fields (`country`, `city`, `number`, `formatted`); 
    for email: a string.
    * `preferred` — preferred type of communication (`true` or `false`);
    * `comment` — comment to the contact;
* `site` — presence on other websites. Consists of the fields:
    * `type` — type of website. Directory entries [resume_contacts_site_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
    * `url` — a link to a profile or an ID on a third-party website/service;
* `title` — desired position;
* `professional_roles` — candidate's professional roles (list). Directory entries
      [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary)
* `salary` — Desired salary. It consists of the following fields:
    * `amount` — total;
    * `currency` — [currency](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) ID;
* `employments` — Employment. [employment](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entries.
* `schedules` — work schedule. List of directory [schedule](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) entries
* `education` — education. Consists of the fields:
    * `elementary` — secondary education (list). This field is usually only completed in the absence of higher education.
     It consists of the following fields:
        * `year` — year graduated;
        * `name` — name of educational institution;
    * `additional` — further training courses (list). It consists of the following fields:
        * `organization` — the organisation that conducted the course;
        * `name` — name of the course;
        * `result` — profession / specialist area;
        * `year` — year graduated;
    * `attestation` — tests, exams (list):
        * `organization` — the organisation that conducted the test or exam;
        * `name` — name of the test or exam;
        * `result` — profession / specialist area;
        * `year` — year the test/exam was passed;
    * `primary` — education higher than secondary (list). It consists of the following fields:
        * `name` — name of educational institution;
        * `name_id` — the id of the educational institution can be found in the [tips for college names](https://api.hh.ru/openapi/en/redoc#tag/Suggestions/operation/get-educational-institutions-suggests);
        * `organization` — faculty;
        * `organization_id` — faculty ID can be found in the [faculties directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-faculties);
        * `result` — profession / specialist area;
        * `result_id` — specialisation id can be found in the [tips for specialisations](suggests.md#specializations);
                        education level;
        * `year` — year graduated;
    * `level` — education level. Directory entries [education_level](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
* `language` — languages (list):
    * `id` - value from [languages](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-languages)
    * `level` - value from [language_level](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
* `experience` — work experience (list). It consists of the following fields:
    * `company` — company;
    * `company_id` — company id, can be found in the [tips for companies](suggests.md#companies);
    * `area` — region of the company. Directory entries [areas](areas.md);
    * `company_url` — company website;
    * `industries` — A list of the company's industries. Entries of the [directory of industries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-industries)
    * `position` — position;
    * `start` — started work (YYYY-MM-DD);
    * `end` — finished work (YYYY-MM-DD);
    * `description` — responsibilities, functions, achievements;
* `skills` — additional information, a free-form description of skills;
* `skill_set` — key skills (a list of unique strings).
* `citizenship` — citizenship (list). Directory entries [areas](areas.md);
* `work_ticket` — work permit (list). Directory entries [areas](areas.md);
* `travel_time` — acceptable travel time to the place of work. Directory entries [travel_time](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
* `recommendation` — recommendations (list). It consists of the following fields:
    * `name` — name;
    * `position` — position;
    * `organization` — company;
* `resume_locale` — resume locale. Directory entries [локали резюме](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-locales-for-resume).
* `driver_license_types` - A list of applicant's driving license categories. [driver_license_types](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
* `has_vehicle` - Does the applicant have their own car;
* `hidden_fields` - [hidden fields](#hidden-fields) in the resume (list). Directory entry
* `access` - [resume visibility](#access_type)
    * `type` - visibility type. Directory entry [resume_access_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)

Parameters taken from [tips](suggests.md) (`name_id`, `organization_id`, `result_id`, `company_id`) 
are optional. In this case, if these parameters are indicated, then when saved they are checked for
being correct. In case of errors, such as non-existent
ids or unconnected university and faculty ids, it will return `HTTP 400 Bad Request` with an indication
of the parent field containing the error.
Additionally, when writing `company_id` in the work experience, the company name will
be changed to the company name from the tips.

### Response

A successful response to resume creation comes with a code `201 Created`, and
the Location header will contain the URL of the created resume:

```
Location: /resumes/0123456789abcdef
```

A successful response to resume update comes with a code and does not have a body.


### Errors

* `403 Forbidden` – The request is not from the applicant.
* `400 Bad Request` - Errors in resume fields. You will receive additional [extended information](#resume-validation) on errors.
* `404 Not Found` – The resume was not found or is not available to the current user (during an update)
* `400 Bad Request` - The allowable number of resumes is exceeded (during creation)
In addition, an [error will be specified](errors.md#resumes) with `type=resumes`, `value=total_limit_exceeded`.


<a name="resume-validation"></a>
### Errors in using fields when creating and editing resumes

When creating and editing resumes, the values in the fields are validated to check the format of used fields and values (see [Parameters](#resume-edit-params)), existence of data, and business rules.

In the event of errors, the response will be `400 Bad Request` with the following body:
```json
{
   "errors": [
        {
            "type": "bad_json_data",
            "value": "year",
            "reason": "min_value",
            "description": "Value is too low",
            "pointer": "/education/additional/1/year"
        },
        {
            "type": "bad_json_data",
            "value": "access",
            "reason": "required",
            "description": "ID for access to resume is a required field",
            "pointer": "/access/type/id"
        }
    ]
}
```
Name | Type | Description
--- | --- | ---
type | string | Error class (always takes the value of `bad_json_data`)
reason | string | Error reason
value | string | Field where the error was found
description | string | Error description for user
pointer | string | [Data pointer](#error-pointer) with error in incoming message

Validation error extends [standard API error](errors.md#general-errors).

Possible causes of errors:

Code | Explanation
--- | ---
required | this field is required
not_found | no value found for submitted id
faculty_without_university | you cannot set the faculty without the university
not_in_dictionary | no value was found in the directory for submitted id
not_a_leaf | value cannot include any leaf node
end_date_before_start_date | `end` less than `start`
not_country | 'area' must be a country (see [country directory](areas.md#countries))
more_than_one_native_language | more than one native language
must_contain_unique | submitted values must be unique
from_different_profareas | submitted values are from different industries
duplicate | value was already used
bad_image_type | submitted value is of bad type (`portfolio` requires values from `GET /artifacts/portfolio`, `photo` requires values from `GET /artifacts/photo`)
processing | object is being processed
preferred_must_be_unique | preferred method of communication must be unique
preferred_contact_not_specified | preferred method of communication is not specified or contact is not specified
need_country_city_number_or_formatted | wrong telephone format in contact details (see [conditions for completing the contact details in the resume](#conditions-contacts))
invalid | error in field value (fields must comply with [conditions for completing the fields](resumes.md#conditions))
greater_than_max | value is greater than the maximum value
less_than_min | value is less than the minimum value
earlier_than_min | date is earlier than allowed
later_than_max | date is later than allowed
length_less_than_min | character number in the field is less than the minimum
length_greater_than_max | character number in the field is greater than the maximum
size_less_than_min | number of items is less than the minimum
size_greater_than_max | number of items is greater than the maximum
send_metro_without_area | no `area` specified for submitted metro station
not_belong_this_city | this metro station is not in the specified city
required_with_not_started_career | submit work experience if the specialty was not the career start
not_match_regexp | value does not match regular expression
more_than_one | more than one email sent
not_available | provided not available value

<a name="error-pointer"></a>
`pointer` for identifying the value uses JsonPointer format [RFC 6901](https://tools.ietf.org/html/rfc6901).
For example, `/education/additional/1/year` means that that the error in the field comes from the message (`year` must be a number):
```json
{
    "title": "Python programmer",
    "education": {
        "additional": [
            {
                "name": "Initial training course",
                "organization": "Training organization",
                "result": "General knowledge of Python",
                "year": 2006
            },
            {
                "name": "Further training course",
                "organization": "Training organization",
                "result": "In-depth knowledge of Python",
                "year": "2012 - error"
            }
        ]
   },
   "salary": {
        "amount": 100500,
        "currency": "RUR"
   }
}
```


<a name="publish"></a>
## Publishing a resume

`POST /resumes/{resume_id}/publish`

The resume can be used as soon as it is first published.

Subsequent publications will update the renewal date of the resume. `next_publish_at` key
in the resume indicates when the resume can be updated.


### Response

A successful response contains a code `204 No Content` and is body-less.


### Errors

* `429 Too Many Requests` - If the update is not available yet.
* `400 Bad Request` - If publication/extension is not possible. The possible causes are:
  * Mandatory fields are empty (to understand what exactly is not filled in, you can call the url [get resume](#item) and look at the `mandatory` field),
  * The fields have not been not edited after banning by a moderator,
  * The resume is being checked by a moderator.
* `403 Forbidden` - If the resume cannot be published because of a lack of necessary privileges (for example, for an employer).


<a name="status-and-publication"></a>
## Information on a resume's status and readiness for publication

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-information/operation/get-resume-status)

<a name="clone"></a>
## Cloning a resume

`POST /resumes?source_resume_id={resume_id}`

Successful cloning will return the response code `201 Created` and the header
`Location` of the response will contain the link to the new resume.

You can only clone your own resumes, otherwise the response code
will be `404 Not Found`.

<a name="delete"></a>
## Deleting a resume

```
DELETE /resumes/{resume_id}
```

where `resume_id` – resume ID.

This method is only available to applicants. The resume is deleted without the possibility of
restoration. All responses associated with this resume are also deleted.

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – The request is not from the applicant.
* `404 Not Found` – The resume was not found or is not available to the current user.

<a name="availability"></a>
## Checking for the ability to create a resume

### Request

```
GET /resumes/creation_availability
```

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "is_creation_available": true,
    "max": 20,
    "created": 2,
    "remaining": 18
}
```

where:

Name | Type | Description
---- | ------ | ---
is_creation_available  | boolean | This is a flag that indicates whether the creation of new resumes is available to this user
max | number | Maximum number of resumes
created  | number | The number of previously created resumes
remaining  | number | The number of resumes that can be created

### Errors

* `403 Forbidden` – The request is not from the applicant.

<a name="conditions"></a>
## Conditions to fill in the fields of a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-resume-conditions)

<a name="init-conditions"></a>
## Conditions to fill in the fields of a new resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-new-resume-conditions)

<a name="conditions-contacts"></a>
## Conditions for contacts in a resume
When filling out contacts in a resume, take the following into account:

 * The resume must contain an email address (and only one).

 * The resume must contain a phone number, and there can be only one number for each type.
   
 * Comments are only available for phone numbers, a comment for an email will not be saved.

 * In the `email` contact, the value is email, for phone it is the object.


Example message for changing contacts in the resume:

```json
{
    "contact": [
        {
            "type": {
                "id": "email"
            },
            "value": "box@test.ru"
        },
        {
            "type": {
                "id": "cell"
            },
            "value": {
                "country": "7",
                "city": "123",
                "number": "4567890",
                "preferred": true
            }
        },
        {
            "type": {
                "id": "home"
            },
            "value": {
                "formatted": "7(499)9078456"
            },
            "comment": "On phone before 9 PM"
        }
    ]
}
```

You must provide either the whole phone number in the `formatted` field or all three parts of the phone number separately in 
the fields `country`, `city` and `number`. If both options are available, the system uses data from the separate fields.
The `formatted` field may contain additional symbols: spaces, brackets, and hyphens.
The separate fields may only contain numbers.


<a name="conditions-other"></a>
## Additional rules for resume fields

There are other rules for filling out a resume outside of the
above-described format:

 * It is not allowed to create several resumes with the same title.

 * Specialisation must be from the same area of profession.

 * The place of residence must be obtained from the `/areas` directory and the selected city cannot
      contain daughter objects, for example, the user cannot indicate
      "Russia" as the place of residence.

 * The nearest metro station must be located in the place of residence.

 * For specialisations from the area *Start of career, students* (id=15) it is not necessary to specify work experience. 
 For other areas of profession these fields must contain at least one entry.

 * Some of the fields of the resume are read-only and cannot be changed with POST/PUT at /resumes.
   

<a name="resume-nano"></a>
## Resume abstract

The briefest resume abstract:

```json
{
    "id": "502ff8b100018bddf30039ed1f63735f4dda66",
    "title": "manager",
    "url": "https://api.hh.ru/resumes/502ff8b100018bddf30039ed1f63735f4dda66"
}
```

where:

 Name  | Type    | Description
 ---- | ------ | ---
 id   | string | Resume ID
 title | string | Desired position
 url  | string | Link to the full resume


<a name="resume-short"></a>
## Resume summary

This option differs from the detailed display in the absence of some fields.

```json
{
    "id": "0123456789abcdef",
    "title": "Resume",
    "url": "https://api.hh.ru/resumes/0123456789abcdef",
    "first_name": "Ivan",
    "last_name": "Ivanov",
    "middle_name": "Ivanovich",
    "can_view_full_info": true,
    "age": 19,
    "alternate_url": "https://hh.ru/resume/0123456789abcdef",
    "created_at": "2015-02-06T12:00:00+0300",
    "updated_at": "2015-04-20T16:24:15+0300",
    "area": {
        "id": "1",
        "name": "Moscow",
        "url": "https://api.hh.ru/areas/1"
    },
    "certificate": [
        {
            "achieved_at": "2015-01-01",
            "owner": null,
            "title": "test",
            "type": "custom",
            "url": "http://example.com/"
        }
    ],
    "education": {
        "primary": [
            {
                "name": "National Research Nuclear University, Moscow",
                "name_id": "39420",
                "organization": "Faculty of Information Technologies",
                "organization_id": null,
                "result": "Computer science",
                "result_id": null,
                "year": 2012
            }
        ],
        "level": {
            "id": "higher",
            "name": "Higher"
        }
    },
    "total_experience": {
        "months": 118
    },
    "experience": [
        {
            "position": "shepherd",
            "start": "2010-01-01",
            "end": null,
            "company": "Horns and hooves",
            "industries": [
                {
                    "id": "51.671",
                    "name": "Landscaping, Cleaning of Buildings and Outdoor Areas"
                },
                {
                    "id": "29.531",
                    "name": "Agriculture, Crop Production, Livestock Breeding"
                }
            ],
            "company_url": "http://example.com/",
            "area": {
                "id": "1",
                "name": "Moscow",
                "url": "https://api.hh.ru/areas/1"
            },
            "company_id": null,
            "employer": null
        },
        {
            "start": "2005-01-01",
            "end": "2009-03-01",
            "company": "HeadHunter",
            "area": {
                "id": "1",
                "name": "Москва",
                "url": "https://api.hh.ru/areas/1"
            },
            "industries": [
                {
                    "id": "7.541",
                    "name": "Internet Company (Search Engines, Payment Systems, Social Networks, Information and Educational, Entertainment Resources, Website Promotion etc.)"
                }
            ],
            "company_url": "https://hh.ru",
            "company_id": "1455",
            "employer": {
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455",
                "logo_urls": {
                    "90": "https://hh.ru/employer/logo/1455"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455"
            }
        }
    ],
    "gender": {
        "id": "male",
        "name": "Male"
    },
    "salary": {
        "amount": 1000000,
        "currency": "RUR"
    },
    "photo": {
        "medium": "https://hh.ru/...",
        "small": "https://hh.ru/...",
        "id": "1337"
    },
    "owner": {
        "id": "123456",
        "comments": {
            "url": "https://api.hh.ru/applicant_comments/123456",
            "counters": {
                "total": 7
            }
        }
    },
    "negotiations_history": {
        "url": "https://api.hh.ru/resumes/0123456789abcdef/negotiations_history"
    },
    "download": {
        "pdf": {
            "url": "https://hh.ru/api_resume_converter/0123456789abcdef/FirstLastMiddle.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/0123456789abcdef/FirstLastMiddle.rtf?type=rtf"
        }
    }
}
```

<a name="download-links"></a>
## Resume download links

At the moment, resumes can be downloaded in the following formats: PDF and RTF.
Applicants can download their resumes. 
The name of the downloaded file may contain the applicant's name or desired position.

### Request

To download a resume, you need to use the URL obtained from the API response, while passing [standard API headers](general.md#request-requirements).

```
GET https://....(a link obtained in the full or shortened resume from the API)
```

### Response

A successful response comes with a code and contains the requested file in its body.

### Errors

* `404 Not Found` - If the resume does not exist or is not available to the user.
* `429 Too Many Requests` - If the daily limit of resume views is exceeded (when the user is authorized as an employer).
* `403 Forbidden` - Services not sufficient to download resume with contacts

In addition to the HTTP code, the server can return a description of the [error cause](errors.md#resumes).


<a name="status"></a>
## CV status

The `status` key determines the current status of the resume and contains an entry from the
[resume_status](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory. After creating a new resume, it
gets the `not_published` status. No one can see a resume with this status,
the user begins to fill in and save the resume (empty mandatory fields
are present in the `progress.mandatory` list). 

After all mandatory fields are filled in, the `can_publish_or_update` flag 
will become `true`, and the resume will be available for
[publication](#publish). After publication, the resume gets the `published` status.
A resume with this status is searchable if permitted by the settings for
[resume visibility](#access_type).

After receiving the `published` status, the resume is available for moderators and
can be banned (the `blocked` status), if the fields are invalid or
contain insufficient information. Reasons for banning a resume can be found in
the [`moderation_note` key](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-information/Resume-status). A banned resume
is not searchable and cannot be used to respond to a job.

After editing, the resume can be sent to the moderator for secondary revision.
In this case, the resume status changes to `on_moderation` and from there it can
go to `blocked` again or to `published`, depending on the moderator's decision.

Once the resume is published (status changed to `published`) it cannot be changed back to
`not_published` but it can be hidden in the [resume visibility](#access_type) settings.

In `published` status, the resume can be used to [apply for jobs](negotiations.md) and it will appear on the
[list of suitable vacancies](suitable_resumes.md) if it has not been used yet to apply for this job.


<a name="access_type"></a>
## CV access type

Each resume has the `access` visibility setting that determines to whom the resume will be available
in the search results or using a direct link. The field's format in the resume:

```json
{
    "access": {
        "type": {
            "id": "clients",
            "name": "visible to all companies registered on HeadHunter"
        }
    }
}
```

After publication, the resume can be searched by all employers. Otherwise,
for example, when a job is found and you want to hide the resume in the search results, you should change
the resume visibility settings. The "access.type" key is responsible for this. Visibility type is a
[resume_access_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.

<a name="access_type_restrictions"></a>
‼️ Since September 1, 2021, the type of resume visibility with the id `everyone` (visible to entire internet) has become unavailable for saving due to legal restrictions.

 Code | Description
 --- | --------
 no_one | A resume of this type is not visible to anyone. However, it can be used to apply for a vacancy and the resume type will change to `whitelist`.
 whitelist | The resume is visible only to the specified companies. If you respond to a job of a company that is not listed, that company will be automatically included in the list. Please see [resume visibility lists](#visibility_lists).
 blacklist | РThe resume can be searched and viewed by all companies, except for ones specified. If you respond to a job of a company that is blacklisted, that company will be automatically excluded from the black list. Please see [resume visibility lists](#visibility_lists).
 clients | The resume is visible to all companies registered on hh.ru.
 everyone | The resume is visible to all users (everywhere on the Internet). This type [is not available for saving](#access_type_restrictions).
 direct |The resume is visible only with a direct link (link specified in the `alternate_url` key).


<a name="visibility_lists"></a>
### Resume visibility lists


Some types of visibility, such as `whitelist` and `blacklist`, imply the use of a list of employers
who can or cannot see the resume. Please see [managing resume visibility lists](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists).


<a name="get_access_types"></a>
### Retrieving a list of resume visibility types

#### Request

```
GET /resumes/{resume_id}/access_types
```

where:
* `resume_id` — resume ID

Successful server response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "id": "everyone",
            "name": "visible to entire internet"
        },
        {
            "id": "no_one",
            "name": "invisible"
        },
        {
            "id": "clients",
            "name": "is visible to all companies registered on Headhunter"
        },
        {
            "id": "whitelist",
            "name": "visible to selected companies",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/whitelist",
            "total": 3,
            "limit": 2000
        },
        {
            "id": "blacklist",
            "name": "hidden from selected companies",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/blacklist",
            "total": 5,
            "limit": 2000,
            "active": true
        },
        {
            "id": "direct",
            "name": "available only by direct link"
        }
    ],
    "auto_hide_time_options": [
        {
            "id": "month_12",
            "name": "1 year"
        },
        {
          "id": "month_10",
          "name": "10 months",
          "active": true
        },
        {
            "id": "month_8",
            "name": "8 months"
        }
    ]
}
```

#### Response

Name | Type | Description
----|-----|---------
items | array | Available resume visibility types.
items[].id | string | Visibility type ID.
items[].name | string | Visibility type name.
items[].active | boolean or null | Visibility type selection indicator.
items[].list_url | string | List address (only for "blacklist" and "whitelist" types).
items[].total | number | Number of companies in the corresponding visibility list (only for `blacklist` and `whitelist` types).
items[].limit | number | Maximum number of companies in the visibility list (only for `blacklist` and `whitelist` types).
auto_hide_time_options | array | Resume auto hide by user inactivity time options, this field is only available for rabota.by users.
auto_hide_time_options[].id | string | Auto hide option ID.
auto_hide_time_options[].name | string | Auto hide option name.
auto_hide_time_options[].active | boolean or null | Auto hide option selection indicator.

#### Errors

* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.


Please see also [managing resume visibility lists](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists).


<a name="views"></a>
## Resume viewing history

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume-view-history)

<a name="similar"></a>
## Searching for jobs similar to a resume

The information is available only to the resume publisher.

### Request

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume)

<a name="hidden-fields"></a>
## CV hidden fields

The `hidden_fields` field contains a list of search fields hidden by the applicant. Hidden fields are replaced by `null`. The CV author is provided with relevant data.

* `names_and_photo` enters `null` instead of the values of the `first_name`, `last_name`, `middle_name` and `photo` fields
* `phones`  enters `null` instead of the value of the `contact[].value` field, when `contact[].type` contains `cell,` `work,` or `home`
* `email`  enters `null` instead of the value of the `contact[].value` field, when `contact[].type` contains `email`
* `other_contacts` enters `null` instead of the value of the `site[].url` field
* `experience` enters `null` instead of the values of the `experience[].company`, `experience[].company_id`, `experience[].company_url`, `experience[].employer` fileds; enters an empty list instead of the value of the `recommendation` field

