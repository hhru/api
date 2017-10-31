# Резюме

* [Список резюме авторизованного пользователя](#mine)
* [Просмотр резюме](#item)
  * [Дополнительные поля для автора резюме](#additional-author-fields)
  * [Платные услуги для соискателя, связанные с резюме](#applicant-paid-services)
  * [Дополнительные поля для работодателя](#additional-employer-fields)
  * [Платные услуги для работодателя, связанные с резюме](#paid-services)
* [Создание и редактирование резюме](#create_edit)
* [Публикация и продление резюме](#publish)
* [Информация о статусе резюме и готовности резюме к публикации](#status-and-publication)
* [Клонирование резюме](#clone)
* [Удаление резюме](#delete)
* [Проверка возможности создания резюме](#availability)
* [Условия заполнения полей резюме](#conditions)
  * [Условия заполнения полей нового резюме](#init-conditions)
  * [Условия заполнения контактов в резюме](#conditions-contacts)
  * [Дополнительные правила заполнения полей резюме](#conditions-other)
* [Короткое представление резюме](#resume-nano)
* [Сокращенное представление резюме](#resume-short)
* [Ссылки на скачивание резюме в нескольких форматах](#download-links)
* [Статусы резюме](#status)
* [Видимость резюме](#access_type)
  * [Списки видимости резюме](#visibility_lists)
  * [Получение списка типов видимости резюме](#get_access_types)
* [История просмотра резюме](#views)
* [Поиск по вакансиям, похожим на резюме](#similar)


<a name="mine"></a>
## Список резюме авторизованного пользователя

`GET /resumes/mine` возвращает список резюме авторизованного пользователя. Без
авторизации вернёт `403 Forbidden`.

```json
{
    "items": [
        {
            "access": {
                "type": {
                    "id": "clients",
                    "name": "видно всем компаниям, зарегистрированным на HeadHunter"
                }
            },
            "total_views": 0,
            "new_views": 0,
            "status": {
                "id": "published",
                "name": "опубликовано"
            },
            "views_url": "https://api.hh.ru/resumes/0123456789abcdef/views",
            "id": "0123456789abcdef",
            "title": "Начинающий специалист",
            "url": "https://api.hh.ru/resumes/0123456789abcdef",
            "first_name": "Иван",
            "last_name": "Иванов",
            "middle_name": "Иванович",
            "age": 19,
            "alternate_url": "https://hh.ru/resume/0123456789abcdef",
            "created_at": "2015-02-06T12:00:00+0300",
            "updated_at": "2015-04-20T16:24:15+0300",
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
            "similar_vacancies": {
                "url": "https://api.hh.ru/resumes/0123456789abcdef/similar_vacancies",
                "counters": {
                    "total": 1507
                }
            },
            "download": {
                "pdf": {
                    "url": "https://hh.ru/api_resume_converter/0123456789abcdef/ИвановИванИванович.pdf?type=pdf"
                },
                "rtf": {
                    "url": "https://hh.ru/api_resume_converter/0123456789abcdef/ИвановИванИванович.rtf?type=rtf"
                }
            }
        }
    ],
    "page": 0,
    "per_page": 1,
    "pages": 1,
    "found": 1
}
```

<a name="resumes-mine-author-fields"></a>
Описание полей смотрите в [выдаче полного резюме](#resume-fields).
Дополнительно ответ содержит:

Имя | Тип | Описание
--- | --- | --------
total_views | number | число просмотров резюме
new_views | number | число новых просмотров. Данный счетчик сбрасывается при получении [детальной истории просмотров](#views).
views_url | string | url, по которому необходимо сделать GET запрос для получения [детальной истории просмотров](#views)
status | object | [статус резюме](#status)
similar_vacancies | object | информация о вакансиях, похожих на это резюме
similar_vacancies.url | string | url, по которому необходимо сделать GET запрос, для получения [вакансий, похожих на данное резюме](#similar)
similar_vacancies.total | number | общее количество похожих вакансий

<a name="item"></a>
## Просмотр резюме

`GET /resumes/{resume_id}`

где `resume_id` – идентификатор резюме.

Если в резюме указан тип видимости «видно всему интернету» или «по прямой
ссылке» (`everyone` и `direct` соответственно), возможен запрос без
авторизации.

Для авторизованного автора возвращается
[более детальная информация](#additional-author-fields), включая тип
видимости, комментарии модераторов и статус.

Для работодателя, если просмотр полных данных по резюме недоступен при текущей
авторизации, в некоторых полях будет `null`, а поле `can_view_full_info` будет
иметь значение `false`.

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "id": "12345678901234567890123456789012abcdef",
    "last_name": "Фамилия",
    "first_name": "Имя",
    "middle_name": "Отчество",
    "age": 36,
    "birth_date": "1980-05-08",
    "gender": {
        "id": "male",
        "name": "Мужской"
    },
    "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Москва"
    },
    "metro": {
        "lat": 55.658147,
        "lng": 37.540957,
        "order": 19,
        "id": "6.41",
        "name": "Калужская"
    },
    "relocation": {
        "type": {
            "id": "relocation_possible",
            "name": "готов к переезду"
        },
        "area": [
            {
                "url": "https://api.hh.ru/areas/2",
                "id": "2",
                "name": "Санкт-Петербург"
            },
            {
                "url": "https://api.hh.ru/areas/76",
                "id": "76",
                "name": "Ростов-на-Дону"
            }
        ]
    },
    "business_trip_readiness": {
        "id": "ready",
        "name": "Готов к командировкам"
    },
    "contact": [
        {
            "comment": null,
            "type": {
                "id": "cell",
                "name": "Мобильный телефон"
            },
            "preferred": true,
            "value": {
                "country": "7",
                "city": "123",
                "number": "4567890",
                "formatted": "+71234567890"
            }
        },
        {
            "type": {
                "id": "email",
                "name": "Эл. почта"
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
    "title": "Программист Python",
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
            "name": "Программирование, Разработка",
            "profarea_id": "1",
            "profarea_name": "Информационные технологии, интернет, телеком",
            "laboring": false
        },
        {
            "id": "1.89",
            "name": "Интернет",
            "profarea_id": "1",
            "profarea_name": "Информационные технологии, интернет, телеком",
            "laboring": false
        },
        {
            "id": "1.9",
            "name": "Web инженер",
            "profarea_id": "1",
            "profarea_name": "Информационные технологии, интернет, телеком",
            "laboring": false
        }
    ],
    "salary": {
        "amount": 100500,
        "currency": "RUR"
    },
    "employments": [
        {
            "id": "full",
            "name": "Полная занятость"
        },
        {
            "id": "part",
            "name": "Частичная занятость"
        }
    ],
    "schedules": [
        {
            "id": "fullDay",
            "name": "Полный день"
        },
        {
            "id": "flexible",
            "name": "Гибкий график"
        }
    ],
    "education": {
        "elementary": [
            {
                "name": "Школа №1923",
                "year": 2003
            }
        ],
        "additional": [
            {
                "name": "Курс повышения квалификации",
                "organization": "Проводившая организация",
                "result": "Специализация",
                "year": 2006
            }
        ],
        "attestation": [
            {
                "name": "Тест на IQ",
                "organization": "IQ центр",
                "result": "Интеллект квалификейшн",
                "year": 2005
            }
        ],
        "primary": [
            {
                "name": "Московская государственная академия ветеринарной медицины и биотехнологии имени К.И. Скрябина, Москва",
                "name_id": "39464",
                "organization": "Факультет зоотехнологий и агробизнеса",
                "organization_id": "25181",
                "result": "Социальная психология",
                "result_id": null,
                "year": 2000
            }
        ],
        "level": {
            "id": "higher",
            "name": "Высшее"
        }
    },
    "language": [
        {
            "id": "rus",
            "name": "Русский",
            "level": {
                "id": "native",
                "name": "родной"
            }
        },
        {
            "id": "eng",
            "name": "Английский",
            "level": {
                "id": "can_read",
                "name": "читаю профессиональную литературу"
            }
        }
    ],
    "experience": [
        {
            "company": "Название работодателя",
            "company_id": null,
            "area": {
                "url": "https://api.hh.ru/areas/113",
                "id": "113",
                "name": "Россия"
            },
            "company_url": "http://www.rbc.ru",
            "industries": [
                {
                    "id": "7.540",
                    "name": "Разработка программного обеспечения"
                },
                {
                    "id": "9.399",
                    "name": "Мобильная связь"
                }
            ],
            "position": "Должность",
            "start": "2005-04-01",
            "end": "2013-01-01",
            "description": "Описание деятельности в компании"
        }
    ],
    "total_experience": {
        "months": 94
    },
    "skills": "Дополнительная информация: ключевые навыки",
    "skill_set": [
        "HTML",
        "CSS"
    ],
    "citizenship": [
        {
            "url": "https://api.hh.ru/areas/113",
            "id": "113",
            "name": "Россия"
        }
    ],
    "work_ticket": [
        {
            "url": "https://api.hh.ru/areas/113",
            "id": "113",
            "name": "Россия"
        }
    ],
    "travel_time": {
        "id": "any",
        "name": "Не имеет значения"
    },
    "recommendation": [
        {
            "name": "Петров Петр",
            "position": "старший научный сотрудник",
            "organization": "Роскосмос"
        }
    ],
    "resume_locale": {
        "id": "RU",
        "name": "Русский"
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
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.rtf?type=rtf"
        }
    }
}
```

<a name="resume-fields"></a>

Поле | Тип | Описание
-----|-----|---------
id | string | Идентификатор резюме
last_name | string или null | Фамилия
first_name | string или null | Имя
middle_name | string или null | Отчество
age | number или null | Возраст
birth_date | string или null | День рождения (в формате `ГГГГ-ММ-ДД`)
gender | object или null | Пол. Элемент справочника [gender](dictionaries.md)
gender.id | string | Идентификатор пола
gender.name | string | Название пола
area | object или null | Город проживания. Элемент справочника [areas](areas.md)
area.id | string | Идентификатор города
area.name | string | Название города
area.url | string | Url получения информации о городе
metro | object или null | Ближайшая станция метро. Элемент справочника [metro](metro.md)
metro.id | string | Идентификатор станции
metro.name | string | Название станции
metro.lat | number | Широта расположения станции (число с плавающей запятой)
metro.lng | number | Долгота расположения станции (число с плавающей запятой)
metro.order | number | Порядковый номер станции на линии метро, начиная с 0
relocation | object | Информация о возможности переезда в другой город
relocation.type | object | Готовность к переезду. Элемент справочника [relocation_type](dictionaries.md)
relocation.type.id | string | Идентификатор типа готовности к переезду
relocation.type.name | string | Название типа готовности к переезду
relocation.areas | array | Список городов, в которые возможен переезд. Может быть пустым. Содержит элементы [справочника регионов](areas.md).
relocation.areas[].id | string | Идентификатор региона
relocation.areas[].name | string | Название региона
relocation.areas[].url | string | Url получения информации о регионе
business_trip_readiness | object | Готовность к командировкам. Элемент справочника [resume_trip_readiness](dictionaries.md#resume_trip_readiness)
business_trip_readiness.id | string | Идентификатор типа готовности к командировкам
business_trip_readiness.name | string | Название типа готовности к командировкам
contact | array | Список контактов соискателя. Может быть пустым, например, для работодателя, если просмотр контактов недоступен.
contact[].type | object | Тип контакта. Элемент справочника [prefered_contact_type](dictionaries.md)
contact[].type.id | string | Идентификатор типа контакта
contact[].type.name | string | Название типа контакта
contact[].value | string или object | Значение контакта. Для телефона  – объект из четырех полей `country `, `city`, `number`, `formatted`, для email — строка.
contact[].value.country | string | Код страны (при указании телефона)
contact[].value.city | string | Код города (при указании телефона)
contact[].value.number | string | Номер (при указании телефона)
contact[].value.formatted | string | Отформатированный номер телефона (при указании телефона)
contact[].preferred | boolean | Является ли данный способ связи предпочитаемым
contact[].comment | string | Комментарий к контакту
photo | object или null | Фотография пользователя
photo.id | string | Уникальный идентификатор изображения
photo.small | string | Url уменьшенного изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
photo.medium | string | Url среднего по размеру изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
portfolio | array | Список изображений в портфолио пользователя. Может быть пустым.
portfolio[].id | string | Уникальный идентификатор изображения
portfolio[].small | string | Url уменьшенного изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
portfolio[].medium | string | Url среднего по размеру изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
portfolio[].description | string | Описание изображения в портфолио
site | array | Профили в соц. сетях и других сервисах
site[].type | object | Тип профиля. Элемент справочника [resume_contacts_site_type](dictionaries.md)
site[].type.id | string | Идентификатов типа профиля
site[].type.name | string | Название типа профиля
site[].url | string | Ссылка на профиль или идентификатор
title | string или null | Желаемая должность
specialization | array | Специализации соискателя. Элементы справочника [specializations](specializations.md)
specialization[].id | string | Идентификатор специализации
specialization[].name | string | Название специализации
specialization[].profarea_id | string | Идентификатор профессиональной области, в которую входит специализация
specialization[].profarea_name | string | Название профессиональной области, в которую входит специализация
specialization[].laboring | boolean | Относится ли специализация к списку рабочих специальностей
salary | object или null | Желаемая зарплата
salary.amount | number | Сумма
salary.currency | string | Идентификатор [валюты](dictionaries.md)
employments | array | Список подходящих соискателю типов занятостей. Может быть пустой. Элементы справочника [employment](dictionaries.md)
employments[].id | string | Идентификатор типа занятости
employments[].name | string | Название типа занятости
schedules | array | Список подходящих соискателю графиков работы. Элементы справочника [schedule](dictionaries.md)
schedules[].id | string | Идентификатор графика работы
schedules[].name | string | Название графика работы
education | object | Образование
education.elementary | array | Среднее образование. Обычно заполняется только при отсутствии высшего образования. Может быть пустым.
education.elementary[].year | number | Год окончания
education.elementary[].name | string | Название учебного заведения
education.additional | array | Список куров повышения квалификации. Может быть пустым
education.additional[].organization | string | Организация, проводившая курс
education.additional[].name | string | Название курса
education.additional[].result | string | Специальность / специализация
education.additional[].year | number | Год окончания
education.attestation | array | Список пройденных тестов или экзаменов
education.attestation[].organization | string | Организация, проводившая тест или экзамен
education.attestation[].name | string | Название теста или экзамена
education.attestation[].result | string | Специальность / специализация
education.attestation[].year | number | Год сдачи
education.primary | array | Список образований выше среднего
education.primary[].name | string | Название учебного заведения
education.primary[].name_id | string или null | Идентификатор учебного заведения
education.primary[].organization | string | Факультет
education.primary[].organization_id | string или null | Идентификатор факультета
education.primary[].result | string | Специальность / специализация
education.primary[].result_id | string или null | Идентификатор специальности / специализации
education.primary[].year | number | Год окончания
education.level | object | Уровень образования. Элемент справочника [education_level](dictionaries.md)
education.level.id | string | Идентификатор уровня образования
education.level.name | string | Название уровня образования
language | array | Список языков, которыми владеет соискатель. Элементы справочника [languages](languages.md). Может быть пустым.
language[].id | string | Идентификатор языка
language[].name | string | Название языка
language[].level | object | Уровень знания языка. Элемент справочника [language_level](dictionaries.md)
language[].level.id | string | Идентификатор уровня знания языка
language[].level.name | string | Название уровня знания языка
experience | array | Опыт работы. Список элементов, который может быть пустым.
experience[].company | string | Организация
experience[].company_id | string или null | Уникальный идентификатор организации. null – если организация неизвестна.
experience[].area | object или null | Регион расположения организации. Элемент [справочника регионов](areas.md). null – если регион не был указан.
experience[].area.id | string | Идентификатор региона
experience[].area.name | string | Название региона
experience[].area.url | string | Url получения информации о регионе
experience[].company_url | string | Cайт компании
experience[].industries | array | Cписок отраслей компании. Элементы [справочника индустрий](industries.md)
experience[].industries[].id | string | Идентификатор отрасли
experience[].industries[].name | string | Название отрасли
experience[].position | string | Должность
experience[].start | string | Начало работы (дата в формате `ГГГГ-ММ-ДД`)
experience[].end | string или null | Окончание работы (дата в формате `ГГГГ-ММ-ДД`). `null` - если работает по настоящее время.
experience[].description | string | Обязанности, функции, достижения
total_experience | object или null | Общий опыт работы. `null` - если опыта работы нет
total_experience.months | number | Целое число, количество месяцев общего опыта работы с округлением до месяца
skills | string или null | Дополнительная информация, описание навыков в свободной форме
skill_set | array | Ключевые навыки (список уникальных строк). Список может быть пустым.
citizenship | array | Список гражданств соискателя. Элементы [справочника регионов](areas.md)
citizenship[].id | string | Идентификатор страны
citizenship[].name | string | Название страны
citizenship[].url | string | Url получения информации о стране
work_ticket | array | Список регионов, в который соискатель имеет разрешение на работу. Элементы [справочника регионов](areas.md)
work_ticket[].id | string | Идентификатор региона
work_ticket[].name | string | Название региона
work_ticket[].url | string | Url получения информации о регионе
travel_time | object | Желательное время в пути до работы. Элемент справочника [travel_time](dictionaries.md);
travel_time.id | string | Идентификатор желательного времени в пути до работы
travel_time.name | string | Название желательного времени в пути до работы
recommendation | array | Список рекомендаций. Может быть пустым.
recommendation[].name | string | Имя выдавшего рекомендацию
recommendation[].position | string | Должность
recommendation[].organization | string | Организация
resume_locale | object | Язык, на котором составлено резюме (локаль). Элемент справочника [локали резюме](locales.md)
resume_locale.id | string | Идентификатор языка
resume_locale.name | string | Название языка
certificate | array | Список сертификатов соискателя. Может быть пустой.
certificate[].title | string | Название сертификата
certificate[].achieved_at | string | Дата получения (в формате `ГГГГ-ММ-ДД`)
certificate[].type | string | Тип сертификата. Доступные значения: `custom`, `microsoft`.
certificate[].owner | string или null | На кого выдан сертификат, актуально только для сертификатов с `type = microsoft`
certificate[].url | string или null | Ссылка на страницу с описанием сертификата
alternate_url | string | Url резюме на сайте
created_at | string | Дата и время создания резюме
updated_at | string | Дата и время обновления резюме
download | object | Ссылки для скачивания резюме в нескольких форматах ([подробнее](#download-links))
download.pdf | object | pdf-версия резюме
download.pdf.url | string | ссылка для получения pdf-версии резюме
download.rtf | object | rft-версия резюме
download.rtf.url | string | ссылка для получение rft-версии резюме



### Ошибки

* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `429 Too Many Requests` - если превышен лимит просмотров резюме в сутки
  (при авторизации работодателем).

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#resumes).


<a name="additional-author-fields"></a>
### Дополнительные поля для автора резюме

```json
{
    "blocked": false,
    "finished": false,
    "total_views": 0,
    "new_views": 0,
    "views_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/views",
    "status": {
        "id": "not_published",
        "name": "не опубликовано"
    },
    "can_publish_or_update": false,
    "publish_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/publish", 
    "progress": {
        "percentage": 42,
        "mandatory": [
            {
                "id": "citizenship",
                "name": "Гражданство"
            },
            {
                "id": "language",
                "name": "Язык"
            },
            {
                "id": "area",
                "name": "Город проживания"
            },
            {
                "id": "skills",
                "name": "Ключевые навыки"
            },
            {
                "id": "contact",
                "name": "Контакты"
            },
            {
                "id": "education",
                "name": "Образование"
            },
            {
                "id": "specialization",
                "name": "Специализация"
            }
        ],
        "recommended": [
            {
                "id": "salary",
                "name": "Заработная плата"
            },
            {
                "id": "middle_name",
                "name": "Отчество"
            },
            {
                "id": "work_ticket",
                "name": "Разрешение на работу"
            },
            {
                "id": "site",
                "name": "Сайт"
            },
            {
                "id": "recommendation",
                "name": "Рекомендации"
            },
            {
                "id": "birth_date",
                "name": "Дата рождения"
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

Поля `blocked`, `finished`, `total_views`, `new_views`, `status`, `views_url`
аналогичны полям в
[списке резюме текущего пользователя](#resumes-mine-author-fields).


<a name="author-progress"></a>
#### Информация о заполненности резюме

Автору резюме выдается информация о заполненности резюме в поле
`progress`:

 Поле | Тип | Описание
 ---- | ----| --------
 percentage | number | Процент заполненности резюме
 can_publish_or_update | boolean | Можно ли [опубликовать или обновить данное резюме](#publish)
 publish_url | string | Url для публикации или обновления резюме
 mandatory | array | Список полей, которые обязательны, но еще не заполнены
 mandatory[].id | string | Id поля
 mandatory[].name | string | Название поля
 recommended | array | Список полей, которые рекомендованы к заполнению, но ещё не заполнены
 recommended[].id | string | Id поля
 recommended[].name | string | Название поля


<a name="author-moderation-notes"></a>
#### Замечания модератора

Если при модерации резюме к нему возникли замечания, они будут выданы в списке
`moderation_note`. В некоторых случаях замечания могут привести к
[блокировке резюме](#status). Полный список замечаний доступен
[в справочнике `resume_moderation_note`](dictionaries.md).

По замечанию выдаются поля:

Имя | Тип | Описание
--- | --- | ---
id | string | идентификатор замечания
name | string | описание замечания
field | string или отсутствует | поле резюме с которым связано замечание


<a name="applicant-paid-services"></a>
#### Платные услуги по резюме для автора

Автору резюме выводится список платных услуг в поле `paid_services`.

По каждой услуге выдаются поля:

Имя | Тип | Описание
--- | --- | ---
id | строка | идентификатор услуги
name | строка | название услуги
active | логический | активна ли в данный момент услуга
expires | строка (дата) | время окончания действия услуги, если услуга активна


<a name="additional-employer-fields"></a>
### Дополнительные поля для работодателя

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
            "name": "Доступ к базе резюме",
            "price_list": {
                "alternate_url": "https://hh.ru/price#dbaccess"
            },
            "quick_purchase": {
                "alternate_url": "https://hh.ru/employer/invoice/purchase?code=FA&hhAreaId=1&period=1&profAreaIds=0",
                "currency": {
                    "abbr": "руб.",
                    "code": "RUR",
                    "name": "Рубли"
                },
                "name": "Купить за 5000 руб.",
                "price": 5000
            }
        }
    ],
    "negotiations_history": {
        "url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/negotiations_history",
        "vacancies": [
            {
                "id": "321",
                "name": "Тестовая вакансия",
                "url": "https://api.hh.ru/vacancies/321",
                "archived": false,
                "items": [
                    {
                        "employer_state": {
                            "id": "offer",
                            "name": "Предложение о работе"
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
#### Платные услуги по резюме для работодателя

Работодателю может быть предложен список платных услуг по резюме.

Например, если полные данные по резюме недоступны, то будет выдано
предложение покупки рекомендованной услуги, чтобы такой доступ получить.

Список услуг выдаётся в поле `paid_services`. По каждой услуге выдаются поля:

Имя | Тип | Описание
--- | --- | ---
id | строка | идентификатор услуги
name | строка | название услуги
price_list.alternate_url | строка | ссылка на сайт, по которой доступен полный прайс на услугу
quick_purchase | объект, null | описание быстрой покупки услуги, если доступно
quick_purchase.alternate_url | строка | ссылка на сайт, по которой будет предложено купить услугу
quick_purchase.name | строка | название действия по заказу услуги
quick_purchase.price | число | цена услуги
quick_purchase.currency | объект | валюта услуги

<a name="owner-field"></a>
#### Информация о владельце резюме

В поле `owner` содержится следующая информация о владельце резюме:

Имя | Тип | Описание
--- | --- | ---
id | string | id владельца резюме
comments | object | [комментарии к владельцу резюме](applicant_comments.md#list)
comments.url | string | url, GET-запрос на который возвращает список комментариев
comments.counters | object | информация о количестве комментариев
comments.counters.total | number | общее количество комментариев

<a name="negotiations-history-field"></a>
#### Краткая история откликов/приглашений по резюме

Поле `negotiations_history.url` выдается всегда и содержит url, на который необходимо делать GET запрос для получения
[подробной истории откликов/приглашений по данному резюме](resume_negotiations_history.md).

Поле `negotiations_history.vacancies` выдается только в том случае, когда при выполнении
[запроса на получение резюме](resumes.md#item) передан дополнительный параметр
`with_negotiations_history`. В этом случае GET запрос должен иметь вид:

`GET /resumes/{resume_id}?with_negotiations_history=true`

Формат поля `negotiations_history.vacancies` подробно описан на странице
[полной истории откликов/приглашений по резюме](resume_negotiations_history.md#response) и различается лишь тем, что
в данном случае список будет ограничен 3-мя вакансиями данного работодателя и последним изменением состояния
отклика/приглашения по каждой из этих вакансий.


<a name="create_edit"></a>
## Создание и редактирование резюме

`POST /resumes` — добавление резюме.

`PUT /resumes/{resume_id}` — редактирование существующего. В качестве тела
запроса используется json в том же формате, что отдается при GET запросе. При
этом для полей с данными справочников из передаваемой JSON-структуры
используются только id передаваемых данных. Например, в резюме в поле владения
языками, указан русский как родной:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Русский",
            "level": {
                "id": "native",
                "name": "родной"
            }
        }
     ]
   }
```

Для того, чтобы добавить английский с уровнем знания «читаю профессиональную
литературу», необходимо отправить следующий JSON:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Русский",
            "level": {
                "id": "native",
                "name": "родной"
            }
        },
        {
            "id": "eng",
            "level": {
                "id": "can_read"
            }
        }
    ]
  }
```

Первый элемент списка — это русский, который у нас уже был в языках, а второй —
это новый элемент, английский, который мы хотим добавить. Поля `language.name` и
`language.level.name`, в данном случае, не мешают, но и не несут полезную
информацию.

При отправке данные заменяют уже существующие данные указанного параметра.
Каждый параметр можно отправлять отдельно от остальных.

<a name="resume-keys"></a>
Параметры:

* `last_name` — фамилия;
* `first_name` — имя;
* `middle_name` — отчество;
* `birth_date` — день рождения (ГГГГ-ММ-ДД);
* `gender` — пол. Элемент справочника [gender](dictionaries.md);
* `photo` — фотография пользователя. см. [артефакты](artifacts.md);
* `portfolio` — портфолио пользователя. см. [артефакты](artifacts.md);
* `area` — город проживания. Элемент справочника [areas](areas.md);
* `metro` — ближайшая станция метро. Элемент справочника [metro](metro.md).
  Имеет смысл указывать только для `area` с метро;
* `relocation` — возможен ли переезд в другой город. Состоит из полей:
    * `type` — элемент справочника [relocation_type](dictionaries.md);
    * `areas` — город, в который возможен переезд (список). Имеет смысл
      только с соответствующим полем `type`. Элемент справочника
      [areas](areas.md);
* `business_trip_readiness` — готовность к командировкам. Элемент справочника
  [resume_trip_readiness](dictionaries.md#resume_trip_readiness)
* `contact` — контактная информация (список). Состоит из полей:
    * `type` — элемент справочника [prefered_contact_type](dictionaries.md)
    * `value` — значение контакта. Для телефона состоит из четырех полей (`country `, `city`, `number`, `formatted`),
      для электронного адреса — строка.
    * `preferred` — предпочитаемый вид связи (`true` или `false`);
    * `comment` — комментарий к контакту;
* `site` — присутствие на других сайтах. Состоит из полей:
    * `type` — тип сайта. Элемент справочника
      [resume_contacts_site_type](dictionaries.md);
    * `url` — ссылка на профиль, либо идентификатор на стороннем сайте/сервисе;
* `title` — желаемая должность;
* `specialization` — специализация соискателя (список). Элемент справочника
  [specializations](specializations.md);
* `salary` — желаемая зарплата. Состоит из полей:
    * `amount` — сумма;
    * `currency` — идентификатор [валюты](dictionaries.md);
* `employments` — занятость. Элементы справочника [employment](dictionaries.md)
* `schedules` — график работы. Список из элементов справочника [schedule](dictionaries.md)
* `education` — образование. Состоит из полей:
    * `elementary` — среднее образование (список). Обычно заполняется только
       при отсутствии высшего образования. Состоит из полей:
        * `year` — год окончания;
        * `name` — название учебного заведения;
    * `additional` — курсы повышения квалификации (список). Состоит из полей:
        * `organization` — организация, проводившая курс;
        * `name` — название курса;
        * `result` — специальность / специализация;
        * `year` — год окончания;
    * `attestation` — тесты, экзамены (список):
        * `organization` — организация, проводившая тест или экзамен;
        * `name` — название тест или экзамена;
        * `result` — специальность / специализация;
        * `year` — год сдачи;
    * `primary` — образование выше среднего (список). Состоит из полей:
        * `name` — название учебного заведения;
        * `name_id` — идентификатор учебного заведения, можно получить из
          [подсказок по названиям вузов](suggests.md#universities);
        * `organization` — факультет;
        * `organization_id` — идентификатор факультета, можно получить из
          [справочника факультетов](faculties.md);
        * `result` — специальность / специализация;
        * `result_id` — идентификатор специальности / специализации, можно
          получить из
          [подсказок по специализациям](suggests.md#specializations);
        * `year` — год окончания;
    * `level` — уровень образования. Элемент справочника
      [education_level](dictionaries.md)
* `language` — владение языками (список). Состоит из элемента справочника
  [languages](languages.md) с добавлением [language_level](dictionaries.md)
  в поле `level`;
* `experience` — опыт работы (список). Состоит из полей:
    * `company` — организация;
    * `company_id` — идентификатор организации, можно получить из
      [подсказок по организациям](suggets.md#companies);
    * `area` — регион расположения организации. Элемента справочника
      [areas](areas.md);
    * `company_url` — сайт компании;
    * `industries` — отрасли компании. Элемент справочника
      [/industries](industries.md)
    * `position` — должность;
    * `start` — начало работы (ГГГГ-ММ-ДД);
    * `end` — окончание работы (ГГГГ-ММ-ДД);
    * `description` — обязанности, функции, достижения;
* `total_experience` — общий опыт работы. `null` - если опыта работы нет. Если
  опыт есть - объект из полей:
    * `months` — целое число, количество месяцев общего опыта работы с округлением до месяца;
* `skills` — дополнительная информация, описание навыков в свободной форме;
* `skill_set` — ключевые навыки (список уникальных строк).
* `citizenship` — гражданство (список). Элемента справочника [areas](areas.md);
* `work_ticket` — разрешение на работу (список). Элемента справочника
  [areas](areas.md);
* `travel_time` — желательное время в пути до работы. Элемент справочника
  [travel_time](dictionaries.md);
* `recommendation` — рекомендации (список). Состоит из полей:
    * `name` — имя;
    * `position` — должность;
    * `organization` — организация;
* `resume_locale` — локаль резюме. Элемент справочника
  [локали резюме](locales.md).

Параметры, берущиеся из [подсказок](suggests.md) (`name_id`, `organization_id`,
`result_id`, `faculty_id`, `company_id`), являются опциональными. При этом, если
данные параметры указаны, то в момент сохранения происходят проверки на их
корректность. В случае ошибок заполнения, таких как передача несуществующих
идентификаторов или не связанных друг с другом идентификаторов университета и
факультета, будет возвращён статус `HTTP 400 Bad Request` с указанием
родительского поля, в котором произошла ошибка (`education`, `experience`).
Дополнительно, при указании в опыте работы `company_id` название компании будет
подменено на название компании из подсказок.

### Ответ

Успешный ответ на создание резюме приходит с кодом `201 Created`, в заголовке
Location при этом будет url созданного резюме:

```
Location: /resumes/0123456789abcdef
```

Успешный ответ на обновление резюме приходит с кодом `204 No Content` и не
содержит тела.


### Ошибки

* `403 Forbidden` – запрос не от соискателя.
* `400 Bad Request` - ошибка в полях резюме. Дополнительно будут указаны поля,
  в которых присутствует ошибка.
* `404 Not Found` – резюме не найдено или недоступно текущему пользователю
  (при обновлении)
* `400 Bad Request` - превышено допустимое количество резюме (при создании).
  Дополнительно [будет указана ошибка](errors.md#resumes)
  с `type=resumes`, `value=total_limit_exceeded`.


<a name="publish"></a>
## Публикация резюме

`POST /resumes/{resume_id}/publish`

При первой публикации резюме оно становится доступно для использования.

Повторная публикация означает обновление даты резюме. Ключ `next_publish_at`
у резюме указывает время, когда можно обновить резюме.

### Ответ

В случае успешной публикации вернётся код ответа `204 No Content` без тела.

### Ошибки

* `429 Too Many Requests` - если обновление ещё недоступно.
* `400 Bad Request` - если публикация или продление невозможны. Возможные причины:
  * не заполнены обязательные поля,
  * не отредактированы поля после блокировки модератором,
  * резюме находится на проверке у модератора.
* `403 Forbidden` - если операция публикации резюме недоступна из-за отсутствия
  прав (например, для работодателя).


<a name="status-and-publication"></a>
## Информация о статусе резюме и готовности резюме к публикации

Метод доступен только для автора резюме и возвращает информацию о статусе резюме (поля `blocked`, `finished`, `status`) и его [готовности к публикации](#author-progress) (в том числе процент заполненности резюме, обязательные и рекомендуемые к заполнению поля), а также [замечания модератора](#author-moderation-notes) по выбранному резюме. Поля аналогичны таковым в списке [дополнительных полей для автора резюме](#additional-author-fields).

```
GET /resumes/{resume_id}/status
```

### Успешный ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "blocked" : false,
    "finished" : false,
    "status" : {
        "id" : "not_published",
        "name" : "не опубликовано"
    },
    "can_publish_or_update": false,
    "publish_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/publish", 
    "progress": {
        "percentage": 42,
        "mandatory": [
            {
                "id": "citizenship",
                "name": "Гражданство"
            },
            {
                "id": "language",
                "name": "Язык"
            },
            {
                "id": "area",
                "name": "Город проживания"
            },
            {
                "id": "skills",
                "name": "Ключевые навыки"
            },
            {
                "id": "contact",
                "name": "Контакты"
            },
            {
                "id": "education",
                "name": "Образование"
            },
            {
                "id": "specialization",
                "name": "Специализация"
            }
        ],
        "recommended": [
            {
                "id": "salary",
                "name": "Заработная плата"
            },
            {
                "id": "middle_name",
                "name": "Отчество"
            },
            {
                "id": "work_ticket",
                "name": "Разрешение на работу"
            },
            {
                "id": "site",
                "name": "Сайт"
            },
            {
                "id": "recommendation",
                "name": "Рекомендации"
            },
            {
                "id": "birth_date",
                "name": "Дата рождения"
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

### Ошибки

* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `403 Forbidden` - пользователь не является соискателем.


<a name="clone"></a>
## Клонирование резюме

`POST /resumes?source_resume_id={resume_id}`

В случае успешного клонирования вернётся код ответа `201 Created`, а в заголовке
`Location` ответа будет содержаться ссылка на новое резюме.

Для клонирования можно использовать только собственные резюме, иначе код ответа
будет `404 Not Found`.


<a name="delete"></a>
## Удаление резюме

```
DELETE /resumes/{resume_id}
```

где `resume_id` – идентификатор резюме.

Метод доступен только для соискателей. Резюме удаляется без возможности
восстановления. Все связанные с ним отклики исчезают.

### Ответ

В случае успешного удаления вернётся код ответа `204 No Content` без тела.

### Ошибки

* `403 Forbidden` – запрос не от соискателя.
* `404 Not Found` – резюме не найдено или недоступно текущему пользователю.


<a name="availability"></a>
## Проверка возможности создания резюме

### Запрос

```
GET /resumes/creation_availability
```

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "is_creation_available": true,
    "max": 20,
    "created": 2,
    "remaining": 18
}
```

где:

Имя  | Тип    | Описание
---- | ------ | ---
is_creation_available  | boolean | Флаг, который показывает, доступно ли создание новых резюме для данного пользователя
max | number | Максимально возможное количество резюме
created  | number | Количество уже созданных резюме
remaining  | number | Количество доступных для создания резюме

### Ошибки

* `403 Forbidden` – запрос не от соискателя.


<a name="conditions"></a>
## Условия заполнения полей резюме

`GET /resumes/{resume_id}/conditions` — возвращает список требований для полей
резюме.

Условия к резюме доступны только его автору, в противном случае вернётся код
ответа `403 Forbidden`.

Если резюме недоступно — код ответа `404 Not Found`.

Если условия получены успешно — код ответа `200 OK`.

Пример:

```javascript
{
    "last_name": {
        "required": true,
        "max_length": 100,
        "min_length": 1
    },
    "title": {
        "max_length": 100,
        "min_length": 2,
        "required": true,
        "not_in": [
            "Бухгалтер"
        ]
    },
    "citizenship": {
        "required": true,
        "min_count": 1,
        "max_count": 3
    },
    "resume_locale": {
        "required": true
    },
    "education": {
        "required": true,
        "fields": {
            "elementary": {
                "required": false,
                "min_count": 0,
                "max_count": 64,
                "fields": {
                    "name": {
                        "required": true,
                        "min_length": 1,
                        "max_length": 512
                    },
                    "year": {
                        "required": true,
                        "min_value": 1950,
                        "max_value": 2023
                    }
                }
            },
            "primary": {
                "required": true,
                "min_count": 1,
                "max_count": 64,
                "fields": {
                    "result": {
                        "required": false,
                        "min_length": 1,
                        "max_length": 128
                    },
                    "organization": {
                        "required": true,
                        "min_length": 1,
                        "max_length": 128
                    },
                    "name": {
                        "required": true,
                        "min_length": 1,
                        "max_length": 512
                    },
                    "year": {
                        "required": true,
                        "min_value": 1950,
                        "max_value": 2023
                    }
                },
            },
            "level": {
                "required": true
            },
            //...
        }
    },
    "salary": {
        "required": false,
        "fields": {
            "currency": {
                "required": true,
                "min_length": 3,
                "max_length": 3
            },
            "amount": {
                "required": true,
                "min_value": 0,
                "max_value": null
            }
        }
    },
    "birth_date": {
        "required": false,
        "min_date": "1900-01-01",
        "max_date": "1999-10-21"
    },
    //...
}
```

Каждое конечное поле описано объектом правил. Если поле в резюме состоит из
объекта с несколькими полями, эти поля описаны в `fields`.

Для всех полей и их частей указано, являются ли они необходимыми (`required`).
Может быть так, что поле, представленное объектом с полями, само по себе не
является необходимым, но если заполнено хотя бы одно поле объекта, необходимо
заполнить и другие его поля. Пример — желаемая зарплата (`salary`) может быть не
указана, либо указана, но обязательно с валютой.

Правила
-------

Имя | Тип | Описание
--- | --- | ---
required | логический | Поле резюме или поле объекта является необходимым.
min_length | целое | Минимальная длина для текстовых полей.
max_length | целое | Максимальная длина для текстовых полей.
not_in | массив | Список недопустимых значений
min_count | целое | Минимальное количество объектов, для полей, где необходимо передавать список.
max_count | целое или `null` | Максимально количество объектов, для полей, где необходимо передавать список. `null` – если количество не ограничено.
min_value | целое | Нижняя граница диапазона числовых значений, включительно.
max_value | целое или `null` | Верхняя граница диапазона числовых значений, включительно. `null` – если верхняя граница не определена.
min_date | строка с датой | Нижняя граница диапазона значений дат, включительно.
max_date | строка с датой | Верхняя граница диапазона значений дат, включительно.


<a name="init-conditions"></a>
## Условия заполнения полей нового резюме

`GET /resume_conditions` — возвращает список требований для полей нового резюме.
Если авторизованный пользователь не соискатель — вернётся код ответа
`403 Forbidden`, иначе `200 OK`.


<a name='conditions-contacts' />
## Условия заполнения контактов в резюме
При заполнении контактов в резюме необходимо учитывать следующие условия:

 * В резюме обязательно должен быть указан email (и он может быть только один).

 * В резюме должен быть указан хотя бы один телефон, причём можно указывать
   только один телефон каждого типа.

 * Комментарий можно указывать только для телефонов, для email комментарий
   не сохранится.

 * В контакте типа 'email' value — это email, а для телефонов — объект.


Формат поля value для телефона:

```json
{
    "formatted": "+7(123)456-78-90",
    "country": "7",
    "city": "123",
    "number": "4567890"
}
```

здесь:

 * formatted - номер телефона целиком
 * country — код города;
 * city — код города;
 * number — номер телефона.

Обязательно указать либо телефон полностью в поле `formatted`, либо все три части телефона по отдельности в
полях `country`, `city` и `number`. Если указано и то, и то, используются данные из разделенного телефона.
В поле `formatted` допустимо указание дополнительных символов: пробелов, скобок, дефисов.
В раздельных полях допустимы только цифры.


<a name='conditions-other' />
## Дополнительные правила заполнения полей резюме

Существует ещё несколько правил заполнения резюме, которые не укладываются в
представленный выше формат:

 * Нельзя создавать несколько резюме с одинаковым title.

 * Специализации должны быть из одной профессиональной области.

 * Город проживания должен быть из справочника `/areas` и при этом у выбранного
   города не должно быть потомков, т.е. нельзя указать город проживания
   «Россия».

 * Ближайшая станция метро должна находиться в городе проживания.

 * Для специализаций из профессиональной области *Начало карьеры, студенты*
   (id=15) можно не указывать опыт работы и навыки. Для остальных профобластей
   данные поля должны содержать хотя бы по одной записи.

 * Часть полей резюме являются read-only, их нельзя изменить при помощи
   POST/PUT на /resumes.


<a name="resume-nano"></a>
## Короткое представление резюме

Самое короткое представление резюме:

```json
{
    "id": "502ff8b100018bddf30039ed1f63735f4dda66",
    "title": "консультант",
    "url": "https://api.hh.ru/resumes/502ff8b100018bddf30039ed1f63735f4dda66"
}
```

где:

 Имя  | Тип    | Описание
 ---- | ------ | ---
 id   | строка | Идентификатор резюме
 title | строка | Желаемая должность
 url  | строка | Ссылка на получение полной версии резюме


<a name="resume-short"></a>
## Сокращенное представление резюме

Отличается от полного представления отсутствием некоторых полей.

```json
{
    "id": "0123456789abcdef",
    "title": "Начинающий специалист",
    "url": "https://api.hh.ru/resumes/0123456789abcdef",
    "first_name": "Иван",
    "last_name": "Иванов",
    "middle_name": "Иванович",
    "can_view_full_info": true,
    "age": 19,
    "alternate_url": "https://hh.ru/resume/0123456789abcdef",
    "created_at": "2015-02-06T12:00:00+0300",
    "updated_at": "2015-04-20T16:24:15+0300",
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
            "url": "https://hh.ru/api_resume_converter/0123456789abcdef/ИвановИванИванович.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/0123456789abcdef/ИвановИванИванович.rtf?type=rtf"
        }
    }
}
```



<a name="download-links"></a>
## Ссылки на скачивание резюме

В настоящий момент резюме доступны для скачивания в форматах PDF и RTF.
Соискатель может скачать свои резюме, работодатель - резюме соискателей (без купленного доступа к базе резюме в файлах буду отсутствовать контакты). Название скачиваемого файла может содержать имя соискателя или его желаемую должность.

### Запрос

Для скачивания резюме нужно использовать полученный из ответа API url, передавая [стандартные для API заголоки](general.md#request-requirements).

```
GET https://....(ссылка, полученная в полной или сокращенной выдаче резюме API)
```

### Ответ

Успешный ответ приходит с кодом 200 и содержит в теле запрашиваемый файл.

### Ошибки

* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `429 Too Many Requests` - если превышен лимит просмотров резюме в сутки
  (при авторизации работодателем).

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#resumes).


<a name="status"></a>
## Статус резюме

Ключ `status` определяет текущее состояние резюме и содержит элемент
справочника [resume_status](dictionaries.md). После создания нового резюме оно
находится в статусе 'not_published'. В этом статусе резюме никому не видно,
пользователь начинает его наполнять и сохранять (незаполненные обязательные поля
можно увидеть в списке `progress.mandatory`). 

После того, как все обязательные поля будут заполнены, флаг `can_publish_or_update` 
будет установлен в `true`, и резюме можно будет
[опубликовать](#publish). Публикация резюме переводит его в статус `published`.
В этом статусе резюме доступно для поиска, если это позволяет
[видимость резюме](#access_type).

После перехода в статус `published`, резюме попадает в поле зрения модераторов и
может быть заблокировано (статус `blocked`), если поля резюме некорректно или
малоинформативно заполнены. Причины блокировки резюме можно найти в
[ключе `moderation_note`](#author-moderation-notes). Заблокированное резюме
пропадает из поиска и не может быть использовано для отклика на вакансию.

После исправления, резюме можно отправить на повторное рассмотрение модератору.
В этом случае резюме переходит в статус `on_moderation`, откуда может снова
перейти в `blocked` или `published`, в зависимости от решения модератора.

После публикации резюме (статус установлен в `published`) его нельзя перевести
обратно в `not_published`, но можно скрыть, настроив
[видимость резюме](#access_type).

В статусе `published` резюме можно использовать для
[отклика на вакансию](negotiations.md), а так же оно появится в
[списке подходящих для отклика](suitable_resumes.md), если им еще не откликались
на эту вакансию.


<a name="access_type"></a>
## Видимость резюме

У каждого резюме есть настройка видимости `access`, которая определяет, кому будет доступно резюме
в поиске и по прямой ссылке. Формат поля в резюме:

```json
{
    "access": {
        "type": {
            "id": "clients",
            "name": "видно всем компаниям, зарегистрированным на HeadHunter"
        }
    }
}
```

После публикации резюме доступно для поиска всем работодателям. Чтобы это изменить
(например, работа найдена и нужно скрыть резюме из поиска), следует поменять
видимость резюме. За это отвечает ключ `access.type`. Тип видимости —
элемент справочника [resume_access_type](dictionaries.md).

 Код | Описание
 --- | --------
 no_one | Резюме такого типа никому не видно. Но им можно откликнуться на вакансию, при этом резюме сменит тип на `whitelist`.
 whitelist | Резюме не видно никому, кроме указанных компаний. Если откликнуться на вакансию компании, которая не входит в список, компания автоматически в него попадёт. См. [списки видимости резюме](#visibility_lists).
 blacklist | Резюме доступно для поиска и просмотра всем компаниям, за исключением указанных. Если откликнуться на вакансию компании из черного списка, то компания вычеркивается из него автоматически. См. [списки видимости резюме](#visibility_lists).
 clients | Резюме доступно всем зарегистрированным компаниям на hh.ru.
 everyone | Резюме доступно всем без исключения (всему интернету).
 direct | Резюме доступно только по прямой ссылке (ссылка указана в ключе `alternate_url`).

<a name="visibility_lists"></a>
### Списки видимости резюме

Некоторые типы видимости, например `whitelist` и `blacklist`, подразумевают наличие списка работодателей,
для которых резюме должно быть видимо или скрыто. См. [управление списками видимости резюме](/docs/resume_visibility.md).


<a name="get_access_types"></a>
### Получение списка типов видимости резюме

```
GET /resumes/{resume_id}/access_types
```

где:
* `resume_id` — идентификатор резюме

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "items": [
        {
            "id": "everyone",
            "name": "видно всему интернету"
        },
        {
            "id": "no_one",
            "name": "не видно никому"
        },
        {
            "id": "clients",
            "name": "видно всем компаниям, зарегистрированным на HeadHunter"
        },
        {
            "id": "whitelist",
            "name": "видно выбранным компаниям",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/whitelist",
            "total": 3,
            "limit": 2000
        },
        {
            "id": "blacklist",
            "name": "скрыто от выбранных компаний",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/blacklist",
            "total": 5,
            "limit": 2000,
            "active": true
        },
        {
            "id": "direct",
            "name": "доступно только по прямой ссылке"
        }
    ]
}
```

Имя | Тип | Описание
----|-----|---------
items | array | Доступные типы видимости резюме.
items[].id | string | Идентификатор типа видимости.
items[].name | string | Имя типа видимости.
items[].active | boolean или null | Выбран ли тип видимости.
items[].list_url | string | Адрес списка (только для типов `blacklist` и `whitelist`).
items[].total | number | Количество компаний, добавленных в соответствующий список видимости (только для типов `blacklist` и `whitelist`).
items[].limit | number | Максимальное количество компаний в списке видимости (только для типов `blacklist` и `whitelist`).

Возможные ошибки:

* `403 Forbidden` — пользователь не является соискателем.
* `404 Not Found` — резюме с указанным идентификатором не найдено или недоступно текущему пользователю.


См. также [управление списками видимости резюме](/docs/resume_visibility.md).


<a name="views"></a>
## История просмотра резюме

`GET /resumes/{resume_id}/views` вернёт историю просмотров резюме. На основном
сайте это доступно при клике на кол-во просмотров резюме на странице со списком
резюме текущего пользователя
([https://hh.ru/applicant/resumes](https://hh.ru/applicant/resumes)).

Без авторизации или же при обращении к чужому резюме вернёт `403 Forbidden`.

Количество просмотров (в том числе, новых) выдаётся при запросе конкретного
резюме и списка резюме. Счетчик новых просмотров обнуляется при запросе данного
ресурса.

```json
{
    "per_page": 20,
    "items": [
        {
            "created_at": "2014-02-05T19:05:58+0400",
            "viewed": true,
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer/logo/1455",
                },
                "vacancies_url": "https://api.hh.ru/vacancies?employer_id=1455",
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455"
            }
        }
    ],
    "page": 0,
    "pages": 1,
    "found": 1
}
```

где:

 Имя | Тип | Описание
 --- | --- | --------
 found | число | Количество записей о просмотре резюме ( ≥ 0 )
 pages | число | Количество страниц ( ≥ 0 )
 per_page | число | Количество элементов на страницу ( > 0 )
 page | число | Номер текущей страницы ( ≥ 0 )

В элементе `items` содержатся данные о откликах:

 Имя | Тип | Описание
 --- | --- | ---
 created_at | строка | Дата создания записи, дата просмотра резюме работодателем
 viewed | логический | отметка о просмотре записи (при запросе данного ресурса все запросы помечаются просмотренными)
 employer | объект | информация о компании (см. ниже)

Объект `employer` возвращает краткие данные о компании, является
«подмножеством» объекта [компания/работодатель](employers.md).

В случаях, когда просмотр совершен анонимным работодателем, либо резюме было
просмотрено из откликов к анонимной вакансии `employer` может содержать лишь
один ключ `name`.

`logo_urls` — изображения логотипа компании разных размеров. Клиент должен
предусмотреть вероятность отсутствия ресурса по указанной ссылке
(`404 Not Found`).


<a name="similar"></a>
## Поиск по вакансиям, похожим на резюме

Данные доступны только автору резюме.


### Запрос

`GET /resumes/{resume_id}/similar_vacancies`

где `resume_id` - идентификатор резюме.

Принимает те же параметры, что и
[поиск по вакансиям](vacancies.md#search-params),
и возвращает результаты в том же виде, что и
[поиск по вакансиям](vacancies.md#search-results)

Дополнительно, если резюме с идентификатором `resume_id` не существует или
недоступно, то в ответ вернется `404 Not Found`.
