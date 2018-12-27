# List of resumes suitable for application

> :bulb: You can also use the [resumes_by_status](resumes_by_status.md) method. All resumes suitable for application for a selected vacancy can be found in the "suitable" collection.

### Request

```
GET /vacancies/{vacancy_id}/suitable_resumes
```

where `vacancy_id` – vacancy ID

It will return information about which resumes the user can use to
apply for the job.

### Response

A successful response contains a code `200 OK` and a list of user's
brief resumes that can be used to apply for this
job:

```json
{
    "found": 1,
    "per_page": 1,
    "page": 1,
    "pages": 1,
    "items": [
        {
            "id": "14831542000d1f366b4c5a6a751b329b70039e",
            "title": "Designer",
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
                        "name": "Russian State Social University, Moscow",
                        "name_id": "39420",
                        "organization": "Faculty of Information Technology",
                        "organization_id": null,
                        "result": "Computer science",
                        "result_id": null,
                        "year": 2012
                    }
                ]
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
                            "id": "51.643",
                            "name": "Improvement and cleaning of territories and buildings"
                        },
                        {
                            "id": "29.503",
                            "name": "Farming, plant growing, animal husbandry"
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
                        "name": "Moscow",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "industries": [
                        {
                            "id": "7.513",
                            "name": "internet"
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
                "name": "male"
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
    "overall": {
        "not_published": 2,
        "already_applied": 1,
        "unavailable": 3
    }
}
```

Please see the [full resume](resumes.md#resume-fields) for a description of the fields.

In addition, the `requires_completion` field is displayed for each resume; this field depends on the presence 
of the "accept incomplete resumes" flag in the corresponding job.

Name | Type | Description
---- | --- | --------
requires_completion | boolean | `true` if a resume is incomplete (only for vacancies without flagged "accept incomplete resumes"). In this case, you must complete mandatory fields (available in [full resume](resumes.md#author-progress)) before applying for this job. Otherwise — `false`. 

If the list is empty, it is impossible to know if the user has resumes, but none of them is suitable or if
he or she does not have any at all. For this, there is additional information in the `overall` key:

Name | Type | Value
---- | --- | --------
not_published | number | number of unpublished resumes
already_applied | number | number of resumes that have already been used by the user to apply for this job
unavailable | number | number of resumes that cannot be used to apply for this job for other reasons (conflicting resume visibility settings, etc.)


### Errors

* `403 Forbidden` – when the request is not from the applicant
