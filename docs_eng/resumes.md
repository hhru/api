# CV

* [List of CVs for current user](#mine)
* [Search for a CV](#search)
* [View a CV](#item)
* [Paid services related to CVs](#paid-services)
* [CV creation & editing](#create_edit)
* [CV publication & prolongation](#publish)
* [CV cloning](#clone)
* [CV fields conditions for editing](#conditions)
* [CV fields conditions for creating](#init-conditions)
* [CV contact fields conditions](#conditions-contacts)
* [Additional CV conditions](#conditions-other)
* [CV short representation](#resume-nano)
* [CV status](#status)
* [CV access type](#access_type)
* [CV view history](#views)


<a name="mine" />
## List of CVs for current user
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#mine)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="search" />
## Search for a CV

`GET /resumes` will return the results of CV search.

------

<a name="resume-search-request" />
**CV search is available only when the authorized user is an employer and**
**the application is in the approved list.**

To include your application in this list, send a request in any format to
<api@hh.ru>. In the letter, describe:

* your application, its purpose and functions,
* Client ID of your application (you can get it
  [in your account](https://dev.hh.ru/admin)),
* the reasons why you need access to CV search, how you are going to use CV
  search results,
* if possible, attach models/screenshots/prototypes to your letter.

Inclusion in the list is free of charge. All the other API capabilities, except
CV search, are available immediately without the need of approval.

------

When the authorized user is an applicant or anonymous, a `403` error will return.

<a name="search-results" />

```json
{
    "found": 2099341,
    "per_page": 20,
    "page": 0,
    "pages": 250,
    "items": [
        {
            "id": "0123456789abcdef",
            "title": "Aspiring specialist",
            "url": "https://api.hh.ru/resumes/0123456789abcdef",
            "first_name": "Ivan",
            "last_name": "Ivanov",
            "middle_name": "Ivanovich",
            "can_view_full_info": true,
            "age": 19,
            "alternate_url": "http://hh.ru/resume/0123456789abcdef",
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
                    "company": "Horns and Hoofs",
                    "industries": [
                        {
                            "id": "51.643",
                            "name": "Land and building improvement and cleaning"
                        },
                        {
                            "id": "29.503",
                            "name": "Farming, plant cultivation, cattle breeding"
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
                            "name": "Internet company (search engines, payment systems, social networks, educational resources, website promotion, etc)"
                        }
                    ],
                    "company_url": "http://hh.ru",
                    "company_id": "1455",
                    "employer": {
                        "alternate_url": "http://hh.ru/employer/1455",
                        "id": "1455",
                        "logo_urls": {
                            "90": "http://hh.ru/employer/logo/1455"
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
                "medium": "http://hh.ru/...",
                "small": "http://hh.ru/...",
                "id": "1337"
            },
            "owner": {
                "comments": {
                    "url": "https://api.hh.ru/applicant_comments/123456"
                }
            }
        }
    ]
}
```

Field output settings in CV search don't affect output in the API.

CV is not fully displayed. The experience object lacks the description (the
`description` field), and the position (the `position` field) is available only
in the latest experience. Only the main education is displayed.

Contact information (full name) will be displayed only with paid access.

To obtain full information, you should request [the full CV](#item).
The applicant will have the CV request displayed in the view history.

CV fields are similar to the
[fields that are displayed when editing the CV](#resume-keys).

The employer will have an additional field `owner.comments.url`.
containing url. GET request on it will return
[applicant comment list of CV owner](applicant_comments.md#list).

When indicating paging parameters (page, per_page), a restriction takes effect:
the number of results returned can't exceed 2000. For instance, a request
`per_page=10&page=199` (displaying CVs from 1991 to 2000) is possible, but a
request with `per_page=10&page=200` will return an error (displaying CVs from
2001 to 2010).


<a name="search-params"/>
### Acceptable parameters

Some parameters take multiple values: `key=value&key=value`.

* `text` – search phrase. Finds CVs that have all the words from the set phrase.
  Several values can be indicated. Each additional
  `text` refines the search. You can use
  [search query language](http://hh.ru/article.xml?articleId=1175) as a search
  phrase. There is [autocompletion](suggests.md#resume-search-keyword) special
  for the field. To tune the phrase settings, you can use the following parameters:
  `text.logic`, `text.field`, `text.period`. When using extra `text.*` fields,
  you must indicate the whole set (triad) of parameters. If parameters are
  indicated incorrectly or there is an incorrect parameter set,
  `400 Bad request` will be returned.

* `text.logic` – describes how the search works. Directory with possible values:
  `resume_search_logic` in [/dictionaries](dictionaries.md).

* `text.field` – describes where words from the `text` search
  phrase should be found. In the text.field parameter you can
  indicate several values separated by commas, e.g.
  `?text.field=education,keywords`. Directory with possible values:
  `resume_search_fields` in [/dictionaries](dictionaries.md).

* `text.period` – a period for searching in work experience. The parameter
  works only when `text.field` equals one of: `experience`, `experience_company`,
  `experience_position`, `experience_description` parameters, but is must always
  be indicated when indicating other `text.*` parameters. In this case it can
  be empty.

---

For example:

* `GET /resumes?text=programmer` – will return all CVs that have the given word
  'programmer' in any place.
* `GET /resumes?text=programmer&text=java` – finds all CVs that have the words
  'programmer' and 'java' in any place.
* `GET /resumes?text=programmer%20java&text.logic=any&text.field=everywhere&text.period=all_time` –
  will find a CV that has a word from the given phrase in the `text` parameter
  ('programmer' or 'java') in any place. If extra fields are used, all of them
  must be indicated.
* `GET /resumes?text=Headhunter&text.logic=all&text.field=experience&text.period=last_three_years` –
  will find all CVs that have the word 'Headhunter' in the last 3 years' work experience.
* `GET /resumes?text=project%20manager&text.logic=all&text.field=experience%2Cskills&text.period=last_year&text=responsible&text.logic=all&text.field=everywhere&text.period=all_time` –
  will find all CVs that have the words 'project' and 'manager', and also
  'responsible' in any place of the work experience and key skills fields.
  It should be noted that extra parameters
  `text.logic=all&text.field=experience%2Cskills&text.period=last_year`
  are indicated for `text=project%20manager`, and
  `text.logic=all&text.field=everywhere&text.period=all_time` for the
  `text=responsible` parameter.

---

* `age_from`, `age_to` – the applicant's age in years, in the "from... to" range.
* `area` – a region. Directory with possible values: [/areas](areas.md).
  You can indicate several values.
* `relocation` – willingness to relocate. Directory with possible values:
  `resume_search_relocation` in [/dictionaries](dictionaries.md). You can
  indicate it only with `area` parameter.
* `period` – in days, searches CVs published in the given time period.
   If not indicated, the search is performed without any restrictions on
   the publication date.
* `date_from` – the date the search should start from. The value is indicated
  in the `dd.mm.yyyy` format. You can't indicate it with the `period` parameter.
* `date_to` – a date until which the search should be performed. The value is
  indicated in the `dd.mm.yyyy` format. You can indicate it only with the
  `date_from` parameter. You can't indicate it with the `period` parameter.
* `education_level` – a level of education. Directory with possible values:
  `education_level` in [/dictionaries](dictionaries.md). If not indicated,
  the search is performed without any restrictions on the education level.
* `employment` – employment type.
  Directory with possible values: `employment` in
  [/dictionaries](dictionaries.md). You can indicate several values.
* `experience` – work experience. Directory with possible values: `experience`
  in [/dictionaries](dictionaries.md).
* `skill` – key skills. At least one key skill identifier is indicated. You
  can get values from the `id` field in the
  [key skills suggestion](suggests.md#key-skills).
* `gender` – a gender. Directory with possible values: `gender` in
  [/dictionaries](dictionaries.md).
* `label` – an extra filter. Directory with possible values:
  `resume_search_label` in [/dictionaries](dictionaries.md). You can indicate
  several values.
* `language` – knowledge of a language. You can indicate several values. It is
  set in the language.level format, where:
    * `language` is a value from the [/languages](languages.md) directory,
    * `level` is a value from the `language_level`
      [/dictionaries](dictionaries.md) directory.
* `metro` – a metro line or station. Directory with possible values:
  [/metro](metro.md).
* `currency` – a currency code. Directory with possible values: `currency`
  (code key) in [/dictionaries](dictionaries.md).
* `salary_from`, `salary_to` – desired salary range, from...to.
* `schedule` – work schedule. Directory with possible values:
  `schedule` in [/dictionaries](dictionaries.md). You can indicate
  several values.
* `specialization` – a professional area or specialization. Directory with
  possible values: [/specializations](specializations.md). You can indicate
  several values.
* `order_by` – CV list sorting. Directory with possible values:
  `resume_search_order` in [/dictionaries](dictionaries.md).
* `per_page` – the number of results per page (cannot exceed 50).
* `page` – a page number.
* `citizenship` – a desired country of citizenship. You can find possible
  values in the directory of countries. Several values can be indicated.
* `work_ticket` – a country which the applicant is permitted to work in.
  You can find possible values in the directory of countries. Several
  values can be indicated.
* `educational_institution` – the applicant's educational institutions.
  Suggestions on university names are used as parameters:
  [/suggests/educational_institutions](suggests.md). Several values can be indicated.

If parameters contain an error, `400 Bad request` will be returned in response
with the error description in the body. Unknown parameters and parameters with
an error in the name are ignored.



<a name="item" />
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
        },
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
        "HTML", "CSS"
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
            "url": "https://api.hh.ru/applicant_comments/123456"
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


<a name="paid-services"/>
### Paid services related to CVs
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#paid-services)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="create_edit" />
## CV creation & editing
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#create_edit)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="publish" />
## CV publication & prolongation
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#publish)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="clone" />
## CV cloning
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#clone)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="conditions" />
## CV fields conditions for editing
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#conditions)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="init-conditions" />
## CV fields conditions for creating

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#init-conditions)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="conditions-contacts" />
## CV contact fields conditions
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#conditions-contacts)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="conditions-other" />
## Additional CV conditions
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#conditions-other)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="resume-nano" />
## CV short representation
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#resume-nano)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).

<a name="status" />
## CV status
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#status)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="access_type" />
## CV access type
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#access_type)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).

<a name="views" />
## CV view history
Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/resumes.md.html#views)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).
