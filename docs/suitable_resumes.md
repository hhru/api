# Список подходящих для отклика резюме

### Запрос

```
GET /vacancies/{vacancy_id}/suitable_resumes
```

где `vacancy_id` – идентификатор вакансии.

Вернётся информация о том, каким из своих резюме пользователь может
откликнуться на вакансию.

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит список сокращенных
представлений резюме пользователя, которыми возможно откликнуться на данную
вакансию:

```json
{
    "found": 1,
    "per_page": 1,
    "page": 1,
    "pages": 1,
    "items": [
        {
            "id": "14831542000d1f366b4c5a6a751b329b70039e",
            "title": "Дизайнер резюме",
            "url": "https://api.hh.ru/resumes/14831542000d1f366b4c5a6a751b329b70039e",
            "created_at": "2013-11-03T00:43:20+0400",
            "updated_at": "2013-11-22T12:25:18+0400",
            "alternate_url": "https://hh.ru/resume/14831542000d1f366b4c5a6a751b329b70039e",
            "access": {
                "type": {
                    "id": "clients",
                    "name": "видно всем компаниям, зарегистрированным на HeadHunter"
                }
            },
            "status": {
                "id": "published",
                "name": "опубликовано"
            },
            "first_name": "Иван",
            "last_name": "Иванов",
            "middle_name": "Иванович",
            "age": 19,
            "area": {
                "id": "1",
                "name": "Москва",
                "url": "https://api.hh.ru/areas/1"
            },
            "certificate": [
                {
                    "achieved_at": "2015-01-01",
                    "owner": null,
                    "title": "тест",
                    "type": "custom",
                    "url": "http://example.com/"
                }
            ],
            "education": {
                "primary": [
                    {
                        "name": "Российский государственный социальный университет, Москва",
                        "name_id": "39420",
                        "organization": "Факультет информационных технологий",
                        "organization_id": null,
                        "result": "Информатика",
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
                    "position": "пастух",
                    "start": "2010-01-01",
                    "end": null,
                    "company": "Рога и копыта",
                    "industries": [
                        {
                            "id": "51.643",
                            "name": "Благоустройство и уборка территорий и зданий"
                        },
                        {
                            "id": "29.503",
                            "name": "Земледелие, растениеводство, животноводство"
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
                            "id": "7.513",
                            "name": "Интернет-компания (поисковики, платежные системы, соц.сети, информационно-познавательные и развлекательные ресурсы, продвижение сайтов и прочее)"
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
                "name": "Мужской"
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
                    "url": "https://hh.ru/api_resume_converter/14831542000d1f366b4c5a6a751b329b70039e/ИвановИванИванович.pdf?type=pdf"
                },
                "rtf": {
                    "url": "https://hh.ru/api_resume_converter/14831542000d1f366b4c5a6a751b329b70039e/ИвановИванИванович.rtf?type=rtf"
                }
            }
        }
    ],
    "overall": {
        "not_published": 2,
        "already_applied": 1,
        "unavailable": 3
    }
}
```

Описание полей смотрите в [выдаче полного резюме](resumes.md#resume-fields).

При пустом списке невозможно понять, есть ли у пользователя резюме, но они все
не подходят, или же их нет. Для этого выдаётся дополнительная информация в
ключе `overall`:

Поле | Тип | Значение
---- | --- | --------
not_published | number | количество неопубликованных резюме
already_applied | number | количество резюме, которыми пользователь уже откликался на эту вакансию
unavailable | number | количество резюме, которыми по другим причинам невозможно откликнуться (конфликтующие настройки видимости резюме и т.п.)


### Ошибки

* `403 Forbidden` – при запросе не от имени соискателя
