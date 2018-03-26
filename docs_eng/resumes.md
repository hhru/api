# CV

* [List of CVs for current user](#mine)
* [View a CV](#item)
* [Paid services related to CVs](#paid-services)
* [CV creation & editing](#create_edit)
* [CV publication & prolongation](#publish)
* [CV status & readiness for publication](#status-and-publication)
* [CV cloning](#clone)
* [CV fields conditions for editing](#conditions)
* [CV fields conditions for creating](#init-conditions)
* [CV contact fields conditions](#conditions-contacts)
* [Additional CV conditions](#conditions-other)
* [CV minimal representation](#resume-nano)
* [CV short representation](#resume-short)
* [CV status](#status)
* [CV access type](#access_type)
* [CV view history](#views)
* [Search for vacancies similar to the CV](#similar)


<a name="mine"></a>
## List of CVs for current user
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#mine)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="item"></a>
## View a CV

`GET /resumes/{resume_id}` returns an indicated CV. If the CV visibility is set
to "visible to entire Internet" or "by direct link" (`everyone` and `direct`
respectively), it is possible to request the CV without being authorized.

If the user is authorized, more detailed information is available, including
visibility type and moderators' comments.

If the CV doesn't exist or unavailable for the user, `404 Not Found` will be
returned.

If the full info of the CV is unavailable with the current authorization,
the corresponding fields will have `null` and field `can_view_full_info`
will have `false` value.

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
            "name": "Частичная занятость"
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
    "download": {
        "pdf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/LastNameFirstNameMiddleName.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/LastNameFirstNameMiddleName.rtf?type=rtf"
        }
    },
    "alternate_url": "https://hh.ru/resume/12345678901234567890123456789012abcdef",
    "created_at": "2013-05-31T14:27:04+0400",
    "updated_at": "2013-10-17T15:22:55+0400",
    "blocked": false,
    "total_views": 0,
    "new_views": 0,
    "finished": false,
    "status": {
        "id": "not_published",
        "name": "not published"
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
    "can_view_full_info": true,
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

### Errors

* `403 Forbidden` – authorization is failed.

Documentation translation for this section is in progress.
For all information see
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#item)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="paid-services"></a>
### Paid services related to CVs
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#paid-services)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


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
## CV status & readiness for publication
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#status-and-publication)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="clone"></a>
## CV cloning
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#clone)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


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
## CV short representation
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#resume-short)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


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

<a name="views"></a>
## CV view history
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#views)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="similar"></a>
## Search for vacancies similar to the CV

Data are available only for the CV author.

### Request

`GET /resumes/{resume_id}/similar_vacancies`

where `resume_id` – ID of the resume.

Accepts the same parameters as [vacancy search](vacancies.md#search-params) and
returns the same results as [vacancy search](vacancies.md#search-results)

Additionally if CV with `resume_id` does not exist or not available
`404 Not Found` will be returned in response.

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` – resume is not found or not available.
