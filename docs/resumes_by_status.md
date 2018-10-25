# Резюме, сгруппированные по возможности отклика на данную вакансию

### Запрос

```
GET /vacancies/{vacancy_id}/resumes_by_status
```

где `vacancy_id` – идентификатор вакансии.

Вернутся резюме пользователя, сгруппированные на четыре списка в зависимости от возможности отклика на вакансию.

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит четыре списка [сокращенных
представлений](resumes.md#resume-short) резюме пользователя:

* `suitable` — резюме, которыми возможно откликнуться на данную вакансию
* `not_published` — неопубликованные резюме (в [статусе](resumes.md#status) `not_published` либо `blocked`)
* `already_applied` — резюме, уже использовавшиеся для отклика на данную вакансию
* `unavailable` — резюме, которыми невозможно откликнуться на данную вакансию (конфликтующие настройки видимости резюме и т.п.)

```json
{
    "suitable": [
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
                ],
                "level": {
                    "id": "higher",
                    "name": "Высшее"
                }
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

Описание полей смотрите в [выдаче полного резюме](resumes.md#resume-fields).

Дополнительно для каждого резюме выдается поле `requires_completion`, зависящее от наличия флага «принимать неполные резюме» в требуемой вакансии.

Имя | Тип | Описание
---- | --- | --------
requires_completion | boolean | Требуется ли дозаполнить [обязательные поля](resumes.md#author-progress) резюме для отклика на вакансию. Принимает значение `true` только в случае, если в вакансии не установлен флаг «принимать неполные резюме» и резюме является неполным; в противном случае — `false`.

В ключе `counters` выдается информация о количестве элементов в коллекциях:

Имя | Тип | Значение
---- | --- | --------
suitable | number | количество резюме, которыми возможно откликнуться на данную вакансию
not_published | number | количество неопубликованных резюме (в [статусе](resumes.md#status) `not_published` либо `blocked`)
already_applied | number | количество резюме, которыми пользователь уже откликался на эту вакансию
unavailable | number | количество резюме, которыми по другим причинам невозможно откликнуться (конфликтующие настройки видимости резюме и т.п.)

### Ошибки

* `403 Forbidden` – при запросе не от имени соискателя
