# CV

* [List of CVs for current user](#mine)
* [View a CV](#item)
  * [Additional fields for the resume publisher](#additional-author-fields)
  * [Resume-related paid services for the resume publisher](#applicant-paid-services)
  * [Additional fields for the employer](#additional-employer-fields)
  * [Resume-related paid services for the resume publisher](#paid-services)
* [CV creation & editing](#create_edit)
* [CV publication & prolongation](#publish)
* [Information on a resume's status and readiness for publication](#status-and-publication)
* [CV cloning](#clone)
* [Deleting a resume](#delete)
* [Checking for the ability to create a resume](#availability)
* [CV fields conditions for editing](#conditions)
  * [CV fields conditions for creating](#init-conditions)
  * [CV contact fields conditions](#conditions-contacts)
  * [Additional CV conditions](#conditions-other)
* [CV minimal representation](#resume-nano)
* [Resume summary](#resume-short)
* [Resume download links](#download-links)
* [CV status](#status)
* [CV access type](#access_type)
  * [Resume visibility lists](#visibility_lists)
  * [Retrieving a list of resume visibility types](#get_access_types)
* [CV view history](#views)
* [Searching for jobs similar to a resume](#similar)


<a name="mine"></a>
## List of CVs for current user

`GET /resumes/mine` returns CV list at [resume summary format](#resume-short) for authorized user.
Server returns `403 Forbidden` if authorization is failed.

```json
{
    "items": [
        {
            "access": {
                "type": {
                    "id": "clients",
                    "name": "is visible to all companies registered on Headhunter"
                }
            },
            "blocked": false,
            "finished": false,
            "total_views": 0,
            "new_views": 0,
            "status": {
                "id": "published",
                "name": "published"
            },
            "views_url": "https://api.hh.ru/resumes/0123456789abcdef/views",
            "id": "0123456789abcdef",
            "title": "First vacancy",
            "url": "https://api.hh.ru/resumes/0123456789abcdef",
            "first_name": "Ivan",
            "last_name": "Ivanov",
            "middle_name": "Ivanovich",
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
                        "name": "Москва",
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
            "similar_vacancies": {
                "url": "https://api.hh.ru/resumes/0123456789abcdef/similar_vacancies",
                "counters": {
                    "total": 1507
                }
            },
            "download": {
                "pdf": {
                    "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.pdf?type=pdf"
                },
                "rtf": {
                    "url": "https://hh.ru/api_resume_converter/0123456789abcdef/IvanovIvanIvanovich.rtf?type=rtf"
                }
            },
            "paid_services": [
                {
                    "id": "resume_autoupdating",
                    "name": "Автообновление резюме",
                    "active": false
                },
                {
                    "id": "resume_marked",
                    "name": "Яркое резюме",
                    "active": true,
                    "expires": "2016-06-08T18:25:25+0300"
                }
            ]
        }
    ],
    "page": 0,
    "per_page": 1,
    "pages": 1,
    "found": 1
}
```

<a name="resumes-mine-author-fields"></a>
Please see the [full resume](#resume-fields) for a description of the fields.
Additionally for [resume summary format](#resume-short) the response also contains the following additional information:

Name | Type | Description
--- | --- | --------
finished | boolean | mark for the resume completion percentage ([more info](#author-progress))
blocked | boolean | mark for CV is blocked by moderator ([more info](#status))
access | object | [CV access type](#access_type)
total_views | number | number of resume views
new_views | number | number of new views. This counter is reset when [detailed viewing history](#views) is received.
views_url | string | the URL to perform a GET request to obtain the [detailed viewing history](#views)
status | object | [resume's status](#status)
similar_vacancies | object | information on jobs similar to this resume
similar_vacancies.url | string | the URL to perform a GET request to obtain [jobs similar to this resume](#similar)
similar_vacancies.counters.total | number | total number of similar jobs
paid_services | object | [resume-related paid services for the resume publisher](#applicant-paid-services)

<a name="item"></a>
## View a CV

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](employer_payable_methods.md)

```
GET /resumes/{resume_id}
``` 

returns an indicated CV. If the CV visibility is set
to "visible to entire Internet" or "by direct link" (`everyone` and `direct`
respectively), it is possible to request the CV without being authorized.

An employer can only view a resume if the company has a response/invitation to that resume as part of an active job vacancy.

An authorized publisher receives more detailed information, including the type of
visibility, comments of moderators, and status.

As for the employer, if it is not possible to view the full information on the resume given the current
authorization, some fields will contain `null`, and the `can_view_full_info` field will be `false`.

```json
{
    "id": "12345678901234567890123456789012abcdef",
    "last_name": "Last Name",
    "first_name": "First Name",
    "middle_name": "Middle Name",
    "age": 36,
    "birth_date": "1980-05-08",
    "gender": {
        "id": "male",
        "name": "Male"
    },
    "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Moscow"
    },
    "metro": {
        "lat": 55.658147,
        "lng": 37.540957,
        "order": 19,
        "id": "6.41",
        "name": "Kaluzhskaya"
    },
    "relocation": {
        "type": {
            "id": "relocation_possible",
            "name": "ready to relocate"
        },
        "area": [
            {
                "url": "https://api.hh.ru/areas/2",
                "id": "2",
                "name": "St Petersburg"
            },
            {
                "url": "https://api.hh.ru/areas/76",
                "id": "76",
                "name": "Rostov-on-Don"
            }
        ]
    },
    "business_trip_readiness": {
        "id": "ready",
        "name": "Ready for business trips"
    },
    "contact": [
        {
            "verified": true,
            "comment": null,
            "type": {
                "id": "cell",
                "name": "Cellphone number"
            },
            "preferred": true,
            "value": {
                "country": "7",
                "city": "123",
                "number": "4567890"
            }
        },
        {
            "type": {
                "id": "email",
                "name": "Email"
            },
            "preferred": false,
            "value": "applicant@example.com"
        }
    ],
    "site": [
        {
            "url": "echo123",
            "type": {
                "id": "skype",
                "name": "Skype"
            }
        },
        {
            "url": "123456",
            "type": {
                "id": "icq",
                "name": "ICQ"
            }
        }
    ],
    "title": "Python programmer",
    "photo": {
        "small": "https://hh.ru/...",
        "medium": "https://hh.ru/...",
        "id": "1337"
    },
    "portfolio": [
        {
            "small": "https://hh.ru/...",
            "medium": "https://hh.ru/...",
            "id": "1337",
            "description": "..."
        }
    ],
    "specialization": [
        {
            "id": "1.221",
            "name": "Programming, Development",
            "profarea_id": "1",
            "profarea_name": "Information technology, Internet, telecom"
        },
        {
            "id": "1.89",
            "name": "Internet",
            "profarea_id": "1",
            "profarea_name": "Information technology, Internet, telecom"
        },
        {
            "id": "1.9",
            "name": "Web engineer",
            "profarea_id": "1",
            "profarea_name": "Information technology, Internet, telecom"
        }
    ],
    "salary": {
        "amount": 100500,
        "currency": "RUR"
    },
    "employments": [
        {
            "id": "full",
            "name": "Full time"
        },
        {
            "id": "part",
            "name": "Part time"
        }
    ],
    "schedules": [
        {
            "id": "fullDay",
            "name": "Full time"
        },
        {
            "id": "flexible",
            "name": "Flexible schedule"
        }
    ],
    "education": {
        "elementary": [
            {
                "name": "School №1923",
                "year": 2003
            }
        ],
        "additional": [
            {
                "name": "Refresher course",
                "organization": "Responsible organization",
                "result": "Specialization",
                "year": 2006
            }
        ],
        "attestation": [
            {
                "name": "IQ test",
                "organization": "IQ center",
                "result": "Intellect qualification",
                "year": 2005
            }
        ],
        "primary": [
            {
                "name": "K.I. Skryabin Moscow State Academy of Veterinary Medicine, Moscow",
                "name_id": "39464",
                "organization": "Faculty of Zootechnology and agrobusiness",
                "organization_id": "25181",
                "result": "Social Psychology",
                "result_id": null,
                "year": 2000
            }
        ],
        "level": {
            "id": "higher",
            "name": "Higher"
        }
    },
    "language": [
        {
            "id": "rus",
            "name": "Russian",
            "level": {
                "id": "native",
                "name": "native"
            }
        },
        {
            "id": "eng",
            "name": "English",
            "level": {
                "id": "can_read",
                "name": "I read professional literature"
            }
        }
    ],
    "experience": [
        {
            "company": "Employer name",
            "company_id": null,
            "area": {
                "url": "https://api.hh.ru/areas/113",
                "id": "113",
                "name": "Russia"
            },
            "company_url": "http://www.rbc.ru",
            "industries": [
                {
                    "id": "7.540",
                    "name": "Software development"
                },
                {
                    "id": "9.399",
                    "name": "Mobile communication"
                }
            ],
            "position": "Position",
            "start": "2005-04-01",
            "end": "2013-01-01",
            "description": "Description of activity in the company"
        }
    ],
    "total_experience": {
        "months": 94
    },
    "skills": "Additional information: key skills",
    "skill_set": [
        "HTML",
        "CSS"
    ],
    "citizenship": [
        {
            "url": "https://api.hh.ru/areas/113",
            "id": "113",
            "name": "Russia"
        }
    ],
    "work_ticket": [
        {
            "url": "https://api.hh.ru/areas/113",
            "id": "113",
            "name": "Russia"
        }
    ],
    "travel_time": {
        "id": "any",
        "name": "Doesn't matter"
    },
    "recommendation": [
        {
            "name": "Petrov Pyotr",
            "position": "senior research scientist",
            "organization": "Roskosmos"
        }
    ],
    "resume_locale": {
        "id": "RU",
        "name": "Russian"
    },
    "certificate": [
        {
            "title": "Oracle Certified Java Professional Programmer",
            "achieved_at": "2013-01-01",
            "type": "custom",
            "owner": null,
            "url": "https://example.com/certificate/123456"
        },
        {
            "title": "MCSE: Windows NT 4.0",
            "achieved_at": "1998-01-26",
            "owner": "JOHN DOE",
            "type": "microsoft",
            "url": null
        },
    ],
    "alternate_url": "https://hh.ru/resume/12345678901234567890123456789012abcdef",
    "created_at": "2013-05-31T14:27:04+0400",
    "updated_at": "2013-10-17T15:22:55+0400",
    "download": {
        "pdf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/LastNameFirstNameMiddleName.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/LastNameFirstNameMiddleName.rtf?type=rtf"
        }
    },
    "has_vehicle": true,
    "driver_license_types": [
        {
            "id": "A"
        },
        {
            "id": "B"
        }
    ]
}
```

<a name="resume-fields"></a>

Name | Type | Description
-----|-----|---------
id | string | Resume ID
last_name | string or null | Last name
first_name | string or null | First name
middle_name | string or null | Middle name
age | number or null | Age
birth_date | string or null | Birthday (`YYYY-MM-DD`)
gender | object or null | [Gender](dictionaries.md)
gender.id | string | Gender ID
gender.name | string | Gender name
area | object or null | City of residence. [areas](areas.md) directory entry
area.id | string | City ID
area.name | string | City name
area.url | string | URL for getting information on the city
metro | object or null | The nearest metro station. [metro](metro.md) directory entry
metro.id | string | Station ID
metro.name | string | Station name
metro.lat | number | Station latitude (a floating point number)
metro.lng | number | Station longitude (a floating point number)
metro.order | number | Sequence number of the station on the subway line (starting with 0)
relocation | object | Information on the possibility of moving to another city
relocation.type | object | Willingness to relocate. [relocation_type](dictionaries.md) directory entry
relocation.type.id | string | Relocation type ID
relocation.type.name | string | Relocation type name
relocation.areas | array | List of cities for potential relocation. This list may be empty. Contains entries of the [directory of regions](areas.md).
relocation.areas[].id | string | Region ID
relocation.areas[].name | string | Region name
relocation.areas[].url | string | URL for getting information on the region
business_trip_readiness | object | Readiness to go on business trips. [resume_trip_readiness](dictionaries.md#resume_trip_readiness) directory entry
business_trip_readiness.id | string | Business trip readiness type ID
business_trip_readiness.name | string | Business trip readiness type name
contact | array | Applicant's contact list. This list may be empty, for example, if the contact view is not available for the employer.
contact[].type | object | Contact type. [prefered_contact_type](dictionaries.md) directory entry
contact[].type.id | string | Contact type ID
contact[].type.name | string | Contact type name
contact[].value | string or object | Contact value. Phone number: a four-field object (`country`, `city`, `number`, `formatted`); email: a string.
contact[].value.country | string | Country code (when specifying a phone number)
contact[].value.city | string | City code (when specifying a phone number)
contact[].value.number | string | Number (when specifying a phone number)
contact[].value.formatted | string | Formatted number (when specifying a phone number)
contact[].preferred | boolean | Is this the preferred method of communication
contact[].comment | string | Comment to the contact
contact[].verified | boolean | Is the phone number confirmed (when specifying a phone number)
photo | object or null | User photo
photo.id | string | Unique image ID
photo.small | string | Small image URL. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
photo.medium | string | URL for a medium-sized image. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
portfolio | array | A list of images in the user's portfolio. This list may be empty.
portfolio[].id | string | Unique image ID
portfolio[].small | string | Small image URL. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
portfolio[].medium | string | URL for a medium-sized image. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
portfolio[].description | string | A description of the image in the portfolio
site | array | Profiles in social networks and other services
site[].type | object | Profile type. [resume_contacts_site_type](dictionaries.md) directory entry
site[].type.id | string | Profile type ID
site[].type.name | string | Profile type name
site[].url | string | A link to profile or ID
title | string or null | Desired position
specialization | array | Applicant's specialist areas. [specializations](specializations.md) directory entries
specialization[].id | string | Specialist area ID
specialization[].name | string | Specialist area name
specialization[].profarea_id | string | ID of the profession that includes this specialist area
specialization[].profarea_name | string | Name of the profession that includes this specialist area
specialization[].laboring | boolean | Is this specialist area associated with the list of blue-collar jobs
salary | object or null | Desired salary
salary.amount | number | Amount
salary.currency | string | [currency](dictionaries.md) ID
employments | array | List of types of employment that are suitable for the applicant. This list may be empty. [employment](dictionaries.md) directory entries
employments[].id | string | Employment type ID
employments[].name | string | Employment type name
schedules | array | List of working hours that are suitable for the applicant. [schedule](dictionaries.md) directory entries
schedules[].id | string | Working hours ID
schedules[].name | string | Working hours name
education | object | Education
education.elementary | array | Secondary education. This field is usually only completed in the absence of higher education. This list may be empty.
education.elementary[].year | number | Year graduated
education.elementary[].name | string | Name of educational institution
education.additional | array | List of training courses. This list may be empty.
education.additional[].organization | string | The organization that conducted the courses
education.additional[].name | string | Course name
education.additional[].result | string | Profession/specialist area
education.additional[].year | number | Year graduated
education.attestation | array | List of passed tests or exams
education.attestation[].organization | string | The organization that conducted the test or exam
education.attestation[].name | string | The name of the test or exam
education.attestation[].result | string | Profession/specialist area
education.attestation[].year | number | Year the test/exam was passed
education.primary | array | List of degrees higher than secondary education
education.primary[].name | string | Name of educational institution
education.primary[].name_id | string or null | Educational institution ID
education.primary[].organization | string | Faculty
education.primary[].organization_id | string or null | Faculty ID
education.primary[].result | string | Profession/specialist area
education.primary[].result_id | string or null | Profession/specialist area ID
education.primary[].year | number | Year graduated
education.level | object | УEducation level. [education_level](dictionaries.md) directory entry
education.level.id | string | Education level ID
education.level.name | string | Education level name
language | array | List of languages spoken by the applicant. [languages](languages.md) directory entries. This list may be empty.
language[].id | string | Language ID
language[].name | string | Language name
language[].level | object | Language proficiency. [language_level](dictionaries.md) directory entry
language[].level.id | string | Language proficiency ID
language[].level.name | string | Language proficiency name
experience | array | Work experience. A list of items that can be empty.
experience[].company | string | Organization
experience[].company_id | string or null | Unique identifier of the organization. If the organization is unknown, the value is null.
experience[].area | object or null | Region of the organization. An entry in the [directory of regions](areas.md). If the organization is not specified, the value is null.
experience[].area.id | string | Region ID
experience[].area.name | string | Region name
experience[].area.url | string | URL for getting information on the region
experience[].company_url | string | Company website
experience[].industries | array | A list of the company's industries. Entries of the [directory of industries](industries.md)
experience[].industries[].id | string | Industry ID
experience[].industries[].name | string | Industry name
experience[].position | string | Position
experience[].start | string | Start date (`YYYY-MM-DD`)
experience[].end | string or null | End date (`YYYY-MM-DD`). If the applicant is still working there, the value is null.
experience[].description | string | Responsibilities, functions, achievements
total_experience | object or null | Total years of service. If the applicant has no work experience, the value is null.
total_experience.months | number | An integer, the total months of service, rounded up to a month
skills | string or null | Additional information, a free-form description of skills
skill_set | array | Key skills (a list of unique strings). This list may be empty.
citizenship | array | Applicant's citizenship list. Entries of the [directory of regions](areas.md)
citizenship[].id | string | Country ID
citizenship[].name | string | Country name
citizenship[].url | string | URL for getting information on the country
work_ticket | array | A list of regions where the applicant has a work permit. Entries of the [directory of regions](areas.md)
work_ticket[].id | string | Region ID
work_ticket[].name | string | Region name
work_ticket[].url | string | URL for getting information on the region
travel_time | object | Acceptable travel time to the place of work. [travel_time](dictionaries.md) directory entry
travel_time.id | string | ID of the acceptable travel time to the place of work
travel_time.name | string | Name of the acceptable travel time to the place of work
recommendation | array | List of recommendations. This list may be empty.
recommendation[].name | string | Name of person providing recommendation
recommendation[].position | string | Position
recommendation[].organization | string | Organization
resume_locale | object | Resume language (locale). [resume locales](locales.md) directory entry
resume_locale.id | string | Language ID
resume_locale.name | string | Language name
certificate | array | Applicant's certificate list. This list may be empty.
certificate[].title | string | Certificate name
certificate[].achieved_at | string | Issue date (`YYYY-MM-DD`)
certificate[].type | string | Certificate type. Available values: `custom`, `microsoft`.
certificate[].owner | string or null | To whom the certificate is issued – only for certificates with `type = microsoft`
certificate[].url | string or null | A link to the page with the certificate description
alternate_url | string | URL for the resume on the website
created_at | string | Date and time resume was created
updated_at | string | Date and time resume was updated
download | object | Links to download the resume in several formats ([more info](#download-links))
download.pdf | object | PDF resume
download.pdf.url | string | A link to download a PDF resume
download.rtf | object | RTF resume
download.rtf.url | string | A link to download an RTF resume
has_vehicle | boolean | Does the applicant have their own car
driver_license_types | array | A list of applicant's driving license categories
driver_license_types[].id | string | Applicant's driver’s license category. [driver_license_types](dictionaries.md) directory entry


### Errors

* `404 Not Found` – If the resume does not exist or is not available to the user.
* `429 Too Many Requests` - If the daily limit of resume views is exceeded (when the user is authorized as an employer).

In addition to the HTTP code, the server can return a description of the [error cause](errors.md#resumes).


<a name="additional-author-fields"></a>
### Additional fields for the resume publisher

```json
{
    "access": {
        "type": {
            "id": "clients",
            "name": "видно всем компаниям, зарегистрированным на HeadHunter"
        }
    },
    "blocked": false,
    "finished": false,
    "total_views": 0,
    "new_views": 0,
    "views_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/views",
    "status": {
        "id": "not_published",
        "name": "not published"
    },
    "can_publish_or_update": false,
    "next_publish_at": "2013-05-31T14:27:04+0400",
    "publish_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/publish", 
    "progress": {
        "percentage": 42,
        "mandatory": [
            {
                "id": "citizenship",
                "name": "Citizenship"
            },
            {
                "id": "language",
                "name": "Languages"
            },
            {
                "id": "area",
                "name": "Area"
            },
            {
                "id": "skills",
                "name": "Skills"
            },
            {
                "id": "contact",
                "name": "Contacts"
            },
            {
                "id": "education",
                "name": "Education"
            },
            {
                "id": "specialization",
                "name": "Specialization"
            }
        ],
        "recommended": [
            {
                "id": "salary",
                "name": "Salary"
            },
            {
                "id": "middle_name",
                "name": "Middle name"
            },
            {
                "id": "work_ticket",
                "name": "Work ticket"
            },
            {
                "id": "site",
                "name": "Site"
            },
            {
                "id": "recommendation",
                "name": "Recommendation"
            },
            {
                "id": "birth_date",
                "name": "Birth date"
            }
        ]
    },
    "moderation_note": [
        {
            "id": "bad",
            "name": "Резюме составлено небрежно."
        },
        {
            "id": "block_no_education_place_or_date",
            "name": "Отсутствуют данные об учебном заведении и дате его окончания.",
            "field": "education"
        }
    ],
    "paid_services": [
        {
            "id": "resume_autoupdating",
            "name": "Автообновление резюме",
            "active": false
        },
        {
            "id": "resume_marked",
            "name": "Яркое резюме",
            "active": true,
            "expires": "2016-06-08T18:25:25+0300"
        }
    ]
}
```

The fields `access`, `blocked`, `finished`, `total_views`, `new_views`, `status`, `views_url`
 are similar to those in the [current user resume list](#resumes-mine-author-fields).


#### Information on the publication/renew CV

 Name | Type | Description
 ---- | ----| --------
 can_publish_or_update | boolean | Is it possible to [publish or update this resume](#publish)
 next_publish_at | string | Date and time for next CV renew possibility
 publish_url | string | An URL to publish or update the resume

<a name="author-progress"></a>
#### Information on the resume completion percentage

The resume publisher can see the information on the resume completion percentage in the `progress` field:

 Name | Type | Description
 ---- | ----| --------
 percentage | number | Resume completion percentage
 mandatory | array | A list of required fields that have not been filled in yet
 mandatory[].id | string | Field ID
 mandatory[].name | string | Field name
 recommended | array | A list of recommended fields that have not been filled in yet
 recommended[].id | string | Field ID
 recommended[].name | string | Field name


<a name="author-moderation-notes"></a>
#### Moderator's comments

The moderator can add comments to the resume to the following list:
`moderation_note`. In some cases, comments can lead to
[resume banning](#status). A full list of comments is available
[in the `resume_moderation_note` directory](dictionaries.md).


The following fields are available for comments:

Name | Type | Description
--- | --- | ---
id | string | comment ID
name | string | comment description
field | string or отсутствует | resume field associated with the comment

<a name="applicant-paid-services"></a>
#### Resume-related paid services for the resume publisher

Resume-related paid services for the resume publisher are displayed in the `paid_services` field.

The following fields are available for each service:

Name | Type | Description
--- | --- | ---
id | string | service ID
name | string | service name
active | logical | information on whether the service is currently enabled
expires | string (date) | service expiration time, if the service is enabled


<a name="additional-employer-fields"></a>
### Additional fields for the employer

```json
{
    "can_view_full_info": false,
    "owner": {
        "id": "123456",
        "comments": {
            "url": "https://api.hh.ru/applicant_comments/123456",
            "counters": {
                "total": 7
            }
        }
    },
    "paid_services": [
        {
            "id": "resume_database_access",
            "name": "Access to the resume database",
            "price_list": {
                "alternate_url": "https://hh.ru/price#dbaccess"
            },
            "quick_purchase": {
                "alternate_url": "https://hh.ru/employer/invoice/purchase?code=FA&hhAreaId=1&period=1&profAreaIds=0",
                "currency": {
                    "abbr": "руб.",
                    "code": "RUR",
                    "name": "Rubles"
                },
                "name": "Buy for 5000 rubles",
                "price": 5000
            }
        }
    ],
    "negotiations_history": {
        "url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/negotiations_history",
        "vacancies": [
            {
                "id": "321",
                "name": "Test vacancy",
                "url": "https://api.hh.ru/vacancies/321",
                "archived": false,
                "items": [
                    {
                        "employer_state": {
                            "id": "offer",
                            "name": "Offer"
                        },
                        "created_at": "2017-01-30T15:06:47+0300",
                        "with_message": true
                    }
                ],
                "negotiations_url": "https://api.hh.ru/negotiations/123",
                "messages_url": "https://api.hh.ru/negotiations/123/messages"
            }
        ]
    }
}
```

<a name="paid-services"></a>
### Resume-related paid services for the employer

An employer may be offered a list of paid resume-related services.

For example, if the full resume information is not available, the employer will receive
an offer to purchase a recommended service that allows such access.

The list of services is displayed in the `paid_services` list. The following fields are available for each service:

Name | Type | Description
--- | --- | ---
id | string | service ID
name | string | service name
price_list.alternate_url | string | link to the site where the full price for the service is available
quick_purchase | object, null | a quick service purchase, if available
quick_purchase.alternate_url | string | link to the site where you will be asked to buy a service
quick_purchase.name | string | name of the action for the service order
quick_purchase.price | nubmer | price of service
quick_purchase.currency | object | currency of service


<a name="owner-field"></a>
#### Information on the resume owner

The `owner` field contains the following information on the resume owner:

Name | Type | Description
--- | --- | ---
id | string | Resume owner ID
comments | object | [comments for the resume owner](applicant_comments.md#list)
comments.url | string | The URL to perform a GET request to obtain the list of comments
comments.counters | object | information on the number of comments
comments.counters.total | number | total number of comments

<a name="negotiations-history-field"></a>
#### Brief history of responses/invitations for a resume

The `negotiations_history.url` field is always available and contains the URL to perform a GET request to obtain the
[detailed history of responses/invitations for a resume](resume_negotiations_history.md).

The `negotiations_history.vacancies` is available only when
the following additional parameter was passed when executing the [request for resume](resumes.md#item):
`with_negotiations_history`. In this case, the GET request should look like this:

`GET /resumes/{resume_id}?with_negotiations_history=true`

The format of the `negotiations_history.vacancies` field is described on the
[detailed history of responses/invitations for a resume](resume_negotiations_history.md#response) page, and the only difference is that
in this case, the list will be limited to 3 jobs of this employer and the latest status change
for the response/invitation for each of these jobs.


<a name="create_edit"></a>
## CV creation & editing
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#create_edit)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="publish"></a>
## CV publication & prolongation
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#publish)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="status-and-publication"></a>
## Information on a resume's status and readiness for publication

This method is only available to the resume publisher and returns information on the status of the resume (the `blocked`, `finished`, and `status` fields) and its [readiness for publication](#author-progress) (including the resume completion percentage, mandatory and recommended fields), as well as [moderator comments](#author-moderation-notes) regarding the selected resume. The fields are similar to those in the [additional fields for the resume publisher](#additional-author-fields) list.

```
GET /resumes/{resume_id}/status
```

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "blocked" : false,
    "finished" : false,
    "status" : {
        "id" : "not_published",
        "name" : "not published"
    },
    "can_publish_or_update": false,
    "publish_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/publish", 
    "progress": {
        "percentage": 42,
        "mandatory": [
            {
                "id": "citizenship",
                "name": "Citizenship"
            },
            {
                "id": "language",
                "name": "Language"
            },
            {
                "id": "area",
                "name": "Area"
            },
            {
                "id": "skills",
                "name": "Key skills"
            },
            {
                "id": "contact",
                "name": "Contacts"
            },
            {
                "id": "education",
                "name": "Education"
            },
            {
                "id": "specialization",
                "name": "Specialization"
            }
        ],
        "recommended": [
            {
                "id": "salary",
                "name": "Salary"
            },
            {
                "id": "middle_name",
                "name": "Middle name"
            },
            {
                "id": "work_ticket",
                "name": "Work permit"
            },
            {
                "id": "site",
                "name": "Site"
            },
            {
                "id": "recommendation",
                "name": "Recommendation"
            },
            {
                "id": "birth_date",
                "name": "Date of Birth"
            }
        ]
    },
    "moderation_note": [
        {
            "id": "bad",
            "name": "Резюме составлено небрежно."
        },
        {
            "id": "block_no_education_place_or_date",
            "name": "Отсутствуют данные об учебном заведении и дате его окончания.",
            "field": "education"
        }
    ]
}
```

### Errors

* `404 Not Found` - If the resume does not exist or is not available to the user.
* `403 Forbidden` - The user is not an applicant.


<a name="clone"></a>
## CV cloning
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#clone)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).

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
## CV fields conditions for editing
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#conditions)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="init-conditions"></a>
## CV fields conditions for creating

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#init-conditions)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="conditions-contacts"></a>
## CV contact fields conditions
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#conditions-contacts)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="conditions-other"></a>
## Additional CV conditions
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#conditions-other)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="resume-nano"></a>
## CV minimal representation
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#resume-nano)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


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
An employer can only download an applicant's resume if the company has a response/invitation to that resume as part of an active job vacancy. 
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

In addition to the HTTP code, the server can return a description of the [error cause](errors.md#resumes).


<a name="status"></a>
## CV status
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#status)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="access_type"></a>
## CV access type
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#access_type)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="visibility_lists"></a>
### Resume visibility lists


Some types of visibility, such as `whitelist` and `blacklist`, imply the use of a list of employers
who can or cannot see the resume. Please see [managing resume visibility lists](resume_visibility.md).


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

#### Errors

* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.


Please see also [managing resume visibility lists](/docs/resume_visibility.md).


<a name="views"></a>
## CV view history
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#views)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="similar"></a>
## Searching for jobs similar to a resume

The information is available only to the resume publisher.

### Request

`GET /resumes/{resume_id}/similar_vacancies`

where `resume_id` – ID of the resume.

It takes the same parameters and returns the results in the same format as the [searching for jobs](vacancies.md#search-params)

In addition, if the resume with `resume_id` identifier does not exist or is unavailable, the response will be `404 Not Found`.
