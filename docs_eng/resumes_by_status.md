# Resumes grouped by the possibility of responding to a given job

### Request

```
GET /vacancies/{vacancy_id}/resumes_by_status
```

`vacancy_id` – vacancy ID.

The response will include the user's resumes grouped into four lists depending on the ability to respond to a job.

### Response

A successful response contains the `200 OK` code and four lists [resume summaries](resumes.md#resume-short) of the user's resumes:

* `suitable` — List of resumes that can be used to apply for this job
* `not_published` — Unpublished ([status](resumes.md#status) `not_published` or `blocked`) resumes
* `already_applied` — Resumes that have already been used to respond to this job
* `unavailable` — Resumes that cannot be used to apply for this job (because of conflicting resume visibility settings, etc.)

```json
{
    "suitable": [
        {
            "id": "14831542000d1f366b4c5a6a751b329b70039e",
            "title": "Resume designer",
            "url": "https://api.hh.ru/resumes/14831542000d1f366b4c5a6a751b329b70039e",
            "created_at": "2013-11-03T00:43:20+0400",
            "updated_at": "2013-11-22T12:25:18+0400",
            "alternate_url": "https://hh.ru/resume/14831542000d1f366b4c5a6a751b329b70039e",
            "access": {
                "type": {
                    "id": "clients",
                    "name": "is visible to all companies registered on Headhunter"
                }
            },
            "status": {
                "id": "published",
                "name": "published"
            },
            "first_name": "Ivan",
            "last_name": "Ivanov",
            "middle_name": "Ivanovich",
            "age": 19,
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
            "negotiations_history": {
                "url": "https://api.hh.ru/resumes/14831542000d1f366b4c5a6a751b329b70039e/negotiations_history"
            },
            "download": {
                "pdf": {
                    "url": "https://hh.ru/api_resume_converter/14831542000d1f366b4c5a6a751b329b70039e/IvanovIvanIvanovich.pdf?type=pdf"
                },
                "rtf": {
                    "url": "https://hh.ru/api_resume_converter/14831542000d1f366b4c5a6a751b329b70039e/IvanovIvanIvanovich.rtf?type=rtf"
                }
            },
            "requires_completion": false
        }
    ],
    "not_published": [],
    "already_applied": [],
    "unavailable": [],
    "counters": {
        "suitable": 1,
        "not_published": 0,
        "already_applied": 0,
        "unavailable": 0
    }
}
```

Please see the [full resume](resumes.md#resume-fields) for a description of the fields.

Additionally, the `requires_completion` field is displayed for each resume; this field depends on the presence of the "accept incomplete resumes" flag in the corresponding job.

Имя | Тип | Описание
---- | --- | --------
requires_completion | boolean | Whether additional information is required in the [required fields](resumes.md#author-progress) of the resume to apply for this job. This parameter is set to `true` only if the "accept incomplete resumes" flag is not set for the job, and the resume is incomplete; otherwise, the value is set to `false`.

The `counters` key displays information about the number of items in collections:

Имя | Тип | Значение
---- | --- | --------
suitable | number | number of resumes that can be used to apply for this job
not_published | number | number of unpublished ([status](resumes.md#status) `not_published` or `blocked`) resumes 
already_applied | number | number of resumes that have already been used by the user to respond to this job
unavailable | number | number of resumes that cannot be used to apply for this job for other reasons (conflicting resume visibility settings, etc.)

### Errors

* `403 Forbidden` – When the request is not from the applicant
