# CV

* [List of CVs for current user](#mine)
* [View a CV](#item)
* [Paid services related to CVs](#paid-services)
* [CV creation & editing](#create_edit)
* [CV publication & prolongation](#publish)
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
    "birth_date": "1980-05-08",
    "gender": {
        "id": "male",
        "name": "Male"
    },
    "photo": {
        "small": "http://hh.ru/...",
        "medium": "http://hh.ru/...",
        "id": "1337"
    },
    "portfolio": [
        {
            "small": "http://hh.ru/...",
            "medium": "http://hh.ru/...",
            "id": "1337",
            "description": "..."
        }
    ],
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
    "employment": {
        "id": "full",
        "name": "Full time"
    },
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
    "total_experience": {
        "months": 94
    },
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
            "organization": "Roskosmos",
            "contact": "+7 495 123 45 67"
        }
    ],
    "alternate_url": "http://hh.ru/resume/12345678901234567890123456789012abcdef",
    "resume_locale": {
        "id": "RU",
        "name": "Russian"
    },
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
        "comments": {
            "url": "https://api.hh.ru/applicant_comments/123456",
            "counters": {
                "total": 7
            }
        }
    },
    "can_view_full_info": true,
    "_progress": {
        "percentage": 42,
        "mandatory": [
            "citizenship",
            "language",
            "area",
            "skills",
            "contact",
            "education",
            "specialization"
        ],
        "recommended": [
            "salary",
            "middle_name",
            "work_ticket",
            "site",
            "recommendation",
            "birth_date"
        ]
    }
}
```

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
