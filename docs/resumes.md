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
* [Скрытые поля в резюме](#hidden-fields)


<a name="mine"></a>
## Список резюме авторизованного пользователя

`GET /resumes/mine` возвращает список резюме в [сокращенном представлении](#resume-short) для авторизованного пользователя. 
Без авторизации вернёт `403 Forbidden`.

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
            "blocked": false,
            "finished": false,
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
            ],
            "hidden_fields": [
                {
                    "id": "phones",
                    "name": "Все указанные в резюме телефоны"
                }
            ],
            "can_publish_or_update": false,
            "next_publish_at": "2021-07-02T21:29:45+0300"
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
Дополнительно к [сокращенному представлению](#resume-short) ответ содержит:

Имя | Тип | Описание
--- | --- | --------
finished | boolean | флаг о заполненности резюме ([подробнее](#author-progress))
blocked | boolean | флаг заблокированности резюме ([подробнее](#status))
access | object | [видимость резюме](#access_type)
total_views | number | число просмотров резюме
new_views | number | число новых просмотров. Данный счетчик сбрасывается при получении [детальной истории просмотров](#views).
views_url | string | url, по которому необходимо сделать GET запрос для получения [детальной истории просмотров](#views)
status | object | [статус резюме](#status)
similar_vacancies | object | информация о вакансиях, похожих на это резюме
similar_vacancies.url | string | url, по которому необходимо сделать GET запрос, для получения [вакансий, похожих на данное резюме](#similar)
similar_vacancies.counters.total | number | общее количество похожих вакансий
paid_services | object | [платные услуги по резюме для автора](#applicant-paid-services)
can_publish_or_update | boolean или null | Можно ли обновить данное резюме (заполняется только для опубликованных резюме, содержит null для неопубликованных)
next_publish_at | string или null | Дата и время следующего возможного обновления (заполняется только для опубликованных резюме, содержит null для неопубликованных)

<a name="item"></a>
## Просмотр резюме

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Для работодателя данный метод требует наличия [платного доступа](/docs/payable/employer_methods.md)

`GET /resumes/{resume_id}`

где `resume_id` – идентификатор резюме.

>!! Внимание произошли изменения в доступе к контактной информации. Прочитайте внимательно информацию про [поконтактный доступ к резюме](payable/resume.md#contact-data)

Для авторизованного автора возвращается
[более детальная информация](#additional-author-fields), включая тип
видимости, комментарии модераторов и статус.

Для работодателя, если просмотр полных данных по резюме недоступен при текущей
авторизации, в некоторых полях будет `null`, а поле `can_view_full_info` будет
иметь значение `false`.

После вызова этого урла, если у работодателя есть отклик/приглашение на это резюме, отклик будет считаться просмотренным.

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
            "verified": true,
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
                "id": "b2",
                "name": "B2 — Средне-продвинутый"
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
    },
    "actions": {
        "download": {
              "pdf": {
                  "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.pdf?type=pdf"
              },
              "rtf": {
                  "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.rtf?type=rtf"
              }
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
    ],
    "hidden_fields": [
        {
            "id": "phones",
            "name": "Все указанные в резюме телефоны"
        }
    ],
    "marked": false
}
```
<a name="resume-fields"></a>

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор резюме.
last_name | string или null | Фамилия.
first_name | string или null | Имя.
middle_name | string или null | Отчество.
age | number или null | Возраст.
birth_date | string или null | День рождения (в формате `ГГГГ-ММ-ДД`).
gender | [object](#id-name-object) или null | Пол. Элемент справочника [gender](dictionaries.md).
area | [object](#id-name-url-object) или null | Город проживания. Элемент справочника [areas](areas.md).
metro | [object](#metro-object) или null | Ближайшая станция метро. Элемент справочника [metro](metro.md).
relocation | [object](#relocation-object) | Информация о возможности переезда в другой город.
business_trip_readiness | [object](#id-name-object) | Готовность к командировкам. Элемент справочника [business_trip_readiness](dictionaries.md#business_trip_readiness).
contact | [array](#contact-object) | Список контактов соискателя.
photo | [object](#photo-object) или null | Фотография пользователя.
portfolio | [array](#portfolio-object) | Список изображений в портфолио пользователя.
site | [array](#site-object) | Профили в соц. сетях и других сервисах.
title | string или null | Желаемая должность.
specialization | [array](#specialization-object) | Специализации соискателя. Элементы справочника [specializations](specializations.md).
salary | [object](#salary-object) или null | Желаемая зарплата.
employments | [array](#id-name-object) | Список подходящих соискателю типов занятостей. Элементы справочника [employment](dictionaries.md).
schedules | [array](#id-name-object) | Список подходящих соискателю графиков работы. Элементы справочника [schedule](dictionaries.md).
education | [object](#education-object) | Образование.
language | [array](#language-object) | Список языков, которыми владеет соискатель. Элементы справочника [languages](languages.md).
experience | [array](#experience-object) | Опыт работы.
total_experience | [object](#total-experience-object) или null | Общий опыт работы.
skills | string или null | Дополнительная информация, описание навыков в свободной форме.
skill_set | array | Ключевые навыки (список уникальных строк).
citizenship | [array](#id-name-url-object) | Список гражданств соискателя. Элементы [справочника регионов](areas.md).
work_ticket | [array](#id-name-url-object) | Список регионов, в который соискатель имеет разрешение на работу. Элементы [справочника регионов](areas.md).
travel_time | [object](#id-name-object) | Желательное время в пути до работы. Элемент справочника [travel_time](dictionaries.md).
recommendation | [array](#recommendation-object) | Список рекомендаций. 
resume_locale | [object](#id-name-object) | Язык, на котором составлено резюме (локаль). Элемент справочника [локали резюме](locales.md).
certificate | [array](#certificate-object) | Список сертификатов соискателя. 
alternate_url | string | URL резюме на сайте.
created_at | string | Дата и время создания резюме.
updated_at | string | Дата и время обновления резюме.
*download* | [object](#download-object) | Устаревшее (используйте `actions`).
actions | [object](#actions-object) | Дополнительные действия
has_vehicle | boolean или null| Наличие личного автомобиля у соискателя.
driver_license_types | [array](#driver-license-types-object) | Список категорий водительских прав соискателя.
hidden_fields | [array](#id-name-object) | [Список скрытых полей](#hidden-fields). Элемент справочника [resume_hidden_fields](dictionaries.md).
can_view_full_info | boolean или null | Наличие права просмотра контактной информации в резюме.
marked | boolean | Наличие "Яркое резюме"

<a name="id-name-object"></a>
Объект с именем и идентификатором

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор поля.
name | string | Название поля.

<a name="id-name-url-object"></a>
Объект с именем, идентификатором и URL

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор поля.
name | string | Название поля.
url | string | URL получения информации о поле.

<a name="metro-object"></a>
Объект `metro`

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор станции.
name | string | Название станции.
lat | number | Широта расположения станции (число с плавающей запятой).
lng | number | Долгота расположения станции (число с плавающей запятой).
order | number | Порядковый номер станции на линии метро, начиная с 0.

<a name="relocation-object"></a>
Объект `relocation`

Имя | Тип | Описание
-----|-----|---------
type | [object](#id-name-object) | Готовность к переезду. Элемент справочника [relocation_type](dictionaries.md).
areas | [array](#id-name-url-object) | Список городов, в которые возможен переезд. Содержит элементы [справочника регионов](areas.md).

<a name="contact-object"></a>
Объект `contact`

Имя | Тип | Описание
-----|-----|---------
type | [object](#id-name-object) | Тип контакта. Элемент справочника [preferred_contact_type](dictionaries.md).
value | string или [object](#value-object) или null | Значение контакта. Для телефона  – [объект](#value-object), для email — строка.
preferred | boolean | Является ли данный способ связи предпочитаемым (обязательно указать один контакт как предпочитаемый `"preferred": true`, в случае если preferred не передан, считаем, что передано значение `false`).
comment | string или null | Комментарий к контакту.
verified | boolean или null | Является ли телефон подтвержденным (при указании телефона).

<a name="value-object"></a>
Объект `value`

Имя | Тип | Описание
-----|-----|---------
country | string | Код страны (при указании телефона).
city | string | Код города (при указании телефона).
number | string | Номер (при указании телефона).
formatted | string | Отформатированный номер телефона (при указании телефона).

<a name="photo-object"></a>
Объект `photo`

Имя | Тип | Описание
-----|-----|---------
id | string | Уникальный идентификатор изображения.
small | string | URL уменьшенного изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
medium | string | URL среднего по размеру изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.

<a name="portfolio-object"></a>
Объект `portfolio`

Имя | Тип | Описание
-----|-----|---------
id | string | Уникальный идентификатор изображения.
small | string | URL уменьшенного изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
medium | string | URL среднего по размеру изображения. Изображение по данному url доступно ограниченное время, после получения ответа. Приложение должно быть готово к тому, что на запрос изображения вернётся `404 Not Found`.
description | string или null | Описание изображения в портфолио.

<a name="site-object"></a>
Объект `site`

Имя | Тип | Описание
-----|-----|---------
type | [object](#id-name-object) | Тип профиля. Элемент справочника [resume_contacts_site_type](dictionaries.md).
url | string или null | Ссылка на профиль или идентификатор.

<a name="specialization-object"></a>
Объект `specialization`

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор специализации.
name | string | Название специализации.
profarea_id | string | Идентификатор профессиональной области, в которую входит специализация.
profarea_name | string | Название профессиональной области, в которую входит специализация.
laboring | boolean | Относится ли специализация к списку рабочих специальностей.

<a name="salary-object"></a>
Объект `salary`

Имя | Тип | Описание
-----|-----|---------
amount | number | Сумма.
currency | string | Идентификатор [валюты](dictionaries.md).

<a name="education-object"></a>
Объект `education`

Имя | Тип | Описание
-----|-----|---------
elementary | [array](#elementary-object) | Среднее образование. Обычно заполняется только при отсутствии высшего образования.
additional | [array](#additional-education-object) | Список куров повышения квалификации.
attestation | [array](#additional-education-object) | Список пройденных тестов или экзаменов.
primary | [array](#primary-object) | Список образований выше среднего. 
level | [object](#id-name-object) | Уровень образования. Элемент справочника [education_level](dictionaries.md).

Особенности сохранения образования:
* Если передать и высшее и среднее образование и уровень образования "средний", то сохранится только среднее образование.
* Если передать и высшее и среднее образование и уровень образования "высшее", то сохранится только высшее образование.

<a name="elementary-object"></a>
Объект `elementary`

Имя | Тип | Описание
-----|-----|---------
year | number | Год окончания.
name | string | Название учебного заведения.

<a name="additional-education-object"></a>
Объект с полями дополнительного образования 

Имя | Тип | Описание
-----|-----|---------
organization | string | Организация, проводившая курс / тест.
name | string | Название курса / теста.
result | string или null | Специальность / специализация.
year | number | Год окончания / сдачи.

<a name="primary-object"></a>
Объект `primary`

Имя | Тип | Описание
-----|-----|---------
name | string | Название учебного заведения.
name_id | string или null | Идентификатор учебного заведения.
organization | string или null| Факультет.
organization_id | string или null | Идентификатор факультета.
result | string или null | Специальность / специализация.
result_id | string или null | Идентификатор специальности / специализации.
year | number | Год окончания.

<a name="language-object"></a>
Объект `language`

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор языка.
name | string | Название языка.
level | [object](#id-name-object) | Уровень знания языка. Элемент справочника [language_level](dictionaries.md).

<a name="experience-object"></a>
Объект `experience`

Имя | Тип | Описание
-----|-----|---------
company | string или null | Организация.
company_id | string или null | Уникальный идентификатор организации.
area | [object](#id-name-url-object) или null | Регион расположения организации. Элемент [справочника регионов](areas.md).
company_url | string или null | Cайт компании.
industries | [array](#id-name-object) | Cписок отраслей компании. Элементы [справочника индустрий](industries.md).
position | string | Должность.
start | string | Начало работы (дата в формате `ГГГГ-ММ-ДД`).
end | string или null | Окончание работы (дата в формате `ГГГГ-ММ-ДД`).
description | string | Обязанности, функции, достижения.

<a name="total-experience-object"></a>
Объект `total_experience`

Имя | Тип | Описание
-----|-----|---------
months | number | Целое число, количество месяцев общего опыта работы с округлением до месяца.

<a name="recommendation-object"></a>
Объект `recommendation`

Имя | Тип | Описание
-----|-----|---------
name | string | Имя выдавшего рекомендацию.
position | string | Должность.
organization | string | Организация.

<a name="certificate-object"></a>
Объект `certificate`

Имя | Тип | Описание
-----|-----|---------
title | string | Название сертификата.
achieved_at | string | Дата получения (в формате `ГГГГ-ММ-ДД`).
type | string | Тип сертификата. Доступные значения: `custom`, `microsoft`.
owner | string или null | На кого выдан сертификат, актуально только для сертификатов с `type = microsoft`.
url | string или null | Ссылка на страницу с описанием сертификата.

<a name="actions-object"></a>
Объект `actions`

Имя | Тип | Описание
-----|-----|---------
download | [object](#download-object) | Ссылки для скачивания резюме в нескольких форматах ([подробнее](#download-links)).

<a name="download-object"></a>
Объект `download`

Имя | Тип | Описание
-----|-----|---------
pdf | object | pdf-версия резюме.
pdf.url | string | ссылка для получения pdf-версии резюме.
rtf | object | rft-версия резюме.
rtf.url | string | ссылка для получение rft-версии резюме.

<a name="driver-license-types-object"></a>
Объект `driver_license_types`

Имя | Тип | Описание
-----|-----|---------
id | string | Категория водительских прав соискателя. Элемент справочника [тип водительских прав](dictionaries.md).

### Ошибки

* `403 Forbidden` - неверная авторизация. Ожидается авторизация пользователя.
* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `429 Too Many Requests` - если превышен лимит просмотров резюме в сутки
  (при авторизации работодателем).

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#resumes).


<a name="additional-author-fields"></a>
### Дополнительные поля для автора резюме

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
        "name": "не опубликовано"
    },
    "can_publish_or_update": false,
    "next_publish_at": "2013-05-31T14:27:04+0400",
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

Поля `access`, `blocked`, `finished`, `total_views`, `new_views`, `status`, `views_url`
аналогичны полям в [списке резюме текущего пользователя](#resumes-mine-author-fields).


#### Информация о публикации/обновлении резюме

 Имя | Тип | Описание
 ---- | ----| --------
 can_publish_or_update | boolean | Можно ли [опубликовать или обновить данное резюме](#publish)
 next_publish_at | string | Дата и время следующей возможной публикации/обновления
 publish_url | string | URL для публикации или обновления резюме

<a name="author-progress"></a>
#### Информация о заполненности резюме

Автору резюме выдается информация о заполненности резюме в поле
`progress`:

 Имя | Тип | Описание
 ---- | ----| --------
 percentage | number | Процент заполненности резюме
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
    "actions": {
        "download": {
            "pdf": {
                "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.pdf?type=pdf"
            },
            "rtf": {
                "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.rtf?type=rtf"
            }
        },
        "download_with_contact": {
            "pdf": {
                "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.pdf?type=pdf&with_contact=2703892fa808bc3"
            },
            "rtf": {
                "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/ФамилияИмяОтчество.rtf?type=rtf&with_contact=2703892fa808bc3"
            }
        },
        "get_with_contact": {
            "url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef?with_contact=2703892fa808bc3"
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
            },
            "description": "Для просмотра скрытых контактов и фотографий кандидата необходимо приобрести доступ к базе резюме."
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
    },
    "viewed": true
}
```


<a name="actions-object-for-employer"></a>
Объект `actions` (дополнительные действия)

Имя | Тип | Описание
-----|-----|---------
download | [object](#download-object) | Ссылки для скачивания резюме в нескольких форматах ([подробнее](#download-links)).
download_with_contact | [object](#download-object) или null | Ссылки для скачивания резюме с контактами (происходит трата услуги) в нескольких форматах ([подробнее](#download-links)).
get_with_contact | object или null | Ссылка для получения резюме с контактами (происходит трата услуги).
get_with_contact.url | строка | Ссылка для получения резюме с контактами. Возвращает объект аналогичный [просмотру резюме](#item)

При просмотре контактов через `download_with_contact` и `get_with_contact` возможна ситуация, когда пользователь скрыл контактные данные([подробнее](/docs/payable/resume.md#contact-data)), тогда просмотр спишется, а в теле ответа придут null в соответствующих полях контактных данных, чтобы защитится от этого, необходимо смотреть на наличие интересующих вас полей в [hidden_fields](#hidden-fields) в резюме.
URL в полях `download_with_contact` и `get_with_contact` генерируется автоматически и каждый раз разный.

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
description | строка, null | примечание к использованию услуги

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

<a name="viewed-field"></a>
#### Флаг, который показывает было ли резюме просмотрено работодателем

Поле `viewed` выдается всегда и может принимать значение `true` или `false`. 


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
                "id": "l1",
                "name": "Родной"
            }
        }
     ]
   }
```

Для того, чтобы добавить английский с уровнем знания «B2 — Средне-продвинутый», необходимо отправить следующий JSON:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Русский",
            "level": {
                "id": "l1",
                "name": "родной"
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

Первый элемент списка — это русский, который у нас уже был в языках, а второй —
это новый элемент, английский, который мы хотим добавить. Поля `language.name` и
`language.level.name`, в данном случае, не мешают, но и не несут полезную
информацию.

При отправке данные заменяют уже существующие данные указанного параметра.
Каждый параметр можно отправлять отдельно от остальных.

<a name="resume-keys"></a>
> Также ознакомьтесь с правилами заполнения параметров резюме в разделе [Условия заполнения полей резюме](#conditions)

<a name="resume-edit-params"></a>
Параметры:

* `last_name` — фамилия;
* `first_name` — имя;
* `middle_name` — отчество;
* `birth_date` — день рождения (ГГГГ-ММ-ДД);
* `gender` — пол. Элемент справочника [gender](dictionaries.md);
* `photo` — фотография пользователя. см. [артефакты](artifacts.md);
* `portfolio` — портфолио пользователя. см. [артефакты](artifacts.md);
* `area` — город проживания. Элемент справочника [areas](areas.md);
* `metro` — ближайшая станция метро. Элемент справочника [metro](metro.md). Если передать метро не принадлежащее переданной `area`, поле проигнорируется
  Имеет смысл указывать только для `area` с метро;
* `relocation` — возможен ли переезд в другой город. Состоит из полей:
    * `type` — элемент справочника [relocation_type](dictionaries.md);
    * `area` — город, в который возможен переезд (список). Имеет смысл
      только с соответствующим полем `type`. Элемент справочника
      [areas](areas.md);
* `business_trip_readiness` — готовность к командировкам. Элемент справочника
  [business_trip_readiness](dictionaries.md#business_trip_readiness)
* `contact` — контактная информация (список). 
Про обязательность полей и данных смотрите в [условиях заполнения контактов](#conditions-contacts). 
Состоит из полей:
    * `type` — элемент справочника [preferred_contact_type](dictionaries.md)
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
* `language` — владение языками (список). 
    * `id` - значение из справочника [languages](languages.md) 
    * `level` - значение из справочника [language_level](dictionaries.md)
* `experience` — опыт работы (список). Состоит из полей:
    * `company` — организация;
    * `company_id` — идентификатор организации, можно получить из
      [подсказок по организациям](suggests.md#companies);
    * `area` — регион расположения организации. Элемента справочника
      [areas](areas.md);
    * `company_url` — сайт компании;
    * `industries` — отрасли компании. Элемент справочника
      [/industries](industries.md)
    * `position` — должность;
    * `start` — начало работы (ГГГГ-ММ-ДД);
    * `end` — окончание работы (ГГГГ-ММ-ДД);
    * `description` — обязанности, функции, достижения;
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
* `resume_locale` — локаль резюме. Элемент справочника [локали резюме](locales.md).
* `driver_license_types` - cписок категорий водительских прав соискателя. Элемент справочника [тип водительских прав](dictionaries.md.md).
* `has_vehicle` - наличие личного автомобиля у соискателя
* `hidden_fields` - [скрытые поля](#hidden-fields) в резюме (список). Элемент справочника [resume_hidden_fields](dictionaries.md).
* `access` - [видимость резюме](#access_type)
    * `type` - тип видимости. Элемент справочника [resume_access_type](dictionaries.md)


Параметры, берущиеся из [подсказок](suggests.md) (`name_id`, `organization_id`,
`result_id`, `company_id`), являются опциональными. При этом, если
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
* `400 Bad Request` - ошибка в полях резюме. Дополнительно придет 
[расширенная информация](#resume-validation) по ошибкам.
* `404 Not Found` – резюме не найдено или недоступно текущему пользователю
  (при обновлении)
* `400 Bad Request` - превышено допустимое количество резюме (при создании).
  Дополнительно [будет указана ошибка](errors.md#resumes)
  с `type=resumes`, `value=total_limit_exceeded`.


<a name="resume-validation"></a>
### Ошибки в использовании полей при создании и редактировании резюме

При создании и редактировании резюме значения в полях проходят проверки (валидация) - формат использования полей и 
значений (см. [Параметры](#resume-edit-params)), существование данных, бизнес правила. 

При ошибках в ответ придет `400 Bad Request` с телом:
```json
{
    "errors": [
        {
            "type": "bad_json_data",
            "value": "year",
            "reason": "min_value",
            "description": "Значение ниже допустимого",
            "pointer": "/education/additional/1/year"
        },
        {
            "type": "bad_json_data",
            "value": "access",
            "reason": "required",
            "description": "Идентификатор доступа к резюме является обязательным полем",
            "pointer": "/access/type/id"
        }
    ]
}
```

Имя | Тип | Описание
--- | --- | ---
type | string | Класс ошибки (всегда принимает значение `bad_json_data`)
reason | string | Причина ошибки
value | string | Поле, в котором обнаружена ошибка
description | string | Описание ошибки для пользователя
pointer | string | [Указатель на данные](#error-pointer) с ошибкой во входящем сообщении

Ошибка валидации расширяет [стандартную ошибку API](errors.md#general-errors).

Возможные причины ошибок:

Код | Пояснение
--- | ---
required | поле является обязательным для заполнения
not_found | не найдено значение по переданному id
faculty_without_university | нельзя установить факультет без университета
not_in_dictionary | не найдено значение по переданному id в справочнике
not_a_leaf | значение не должно содержать потомков
end_date_before_start_date | значение `end` меньше `start`
not_country | значение area должно быть страной (см. [справочник стран](areas.md#countries))
more_than_one_native_language | указано более одного родного языка
must_contain_unique | переданные значения должны быть уникальны
from_different_profareas | переданные значения из разных отраслей
duplicate | значение уже было использовано
bad_image_type | переданное значение неправильного типа (для portfolio необходимы значения из `get /artifacts/portfolio`, для photo - `get /artifacts/photo`) 
processing | объект в процессе обработки
preferred_must_be_unique | предпочитаемый тип связи должен быть уникальным 
preferred_contact_not_specified | предпочитаемый тип связи не указан или не указано значение контакта
need_country_city_number_or_formatted | телефон в контактах указан в неверном формате (см. [условия заполнения контактов в резюме](#conditions-contacts))
invalid | ошибка в значении поля (поля должны соответствовать [условиям заполнения](resumes.md#conditions))
greater_than_max | значение больше максимума 
less_than_min | значение меньше минимума
earlier_than_min | указанная дата раньше минимально возможной
later_than_max | указанная дата позже максимально возможной
length_less_than_min | количество символов в поле меньше минимума
length_greater_than_max | количество символов в поле больше максимума
size_less_than_min | количество элементов меньше минимума
size_greater_than_max | количество элементов больше максимума
send_metro_without_area | не передано значение поля `area` при заполненном метро
not_belong_this_city | указанного метро нет в указанном городе
required_with_not_started_career | необходимо отправлять опыт работы, если специализация не начало карьеры
not_match_regexp | значение не соответствует регулярному выражению
more_than_one | передано более одного email

<a name="error-pointer"></a>
`pointer` для указания использует формат JsonPointer [RFC 6901](https://tools.ietf.org/html/rfc6901).
Например, `/education/additional/1/year` значит, что ошибка в поле из сообщения (`year` - должно быть числом):
```json
{
    "title": "Программист Python",
    "education": {
        "additional": [
            {
                "name": "Курс начальной подготовки",
                "organization": "Проводившая организация",
                "result": "Общие знания Python",
                "year": 2006
            },
            {
                "name": "Курс повышения квалификации",
                "organization": "Проводившая организация",
                "result": "Углубленные знания Python",
                "year": "2012 - ошибка"
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
            "level": {
                "required": true
            },
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
                //...
            }
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

<a name="condition-rules"></a>
Правила
-------

Имя | Тип | Описание
--- | --- | ---
required | логический | Поле резюме или поле объекта является необходимым. Для строковых значений поле не должно быть `null` или "".
min_length | целое или `null` | Минимальная длина для текстовых полей. Рассчитывается для текста без символов `\r\n`. `null` – если количество не ограничено.
max_length | целое или `null` | Максимальная длина для текстовых полей. Рассчитывается для текста без символов `\r\n`. `null` – если количество не ограничено.
not_in | массив | Список недопустимых значений
min_count | целое или `null` | Минимальное количество объектов, для полей, где необходимо передавать список. `null` – если нижняя граница не определена.
max_count | целое или `null` | Максимально количество объектов, для полей, где необходимо передавать список. `null` – если верхняя граница не определена.
min_value | целое или `null` | Нижняя граница диапазона числовых значений, включительно. `null` – если нижняя граница не определена.
max_value | целое или `null` | Верхняя граница диапазона числовых значений, включительно. `null` – если верхняя граница не определена.
min_date | строка с датой или `null` | Нижняя граница диапазона значений дат, включительно. `null` – если нижняя граница даты не определена.
max_date | строка с датой или `null` | Верхняя граница диапазона значений дат, включительно. `null` – если верхняя граница даты не определена.
regexp | строка или `null` | Регулярное выражение, которому должно соответствовать строковое поле. `null` – если ограничения отсутствуют.


<a name="init-conditions"></a>
## Условия заполнения полей нового резюме

`GET /resume_conditions` — возвращает список требований для полей нового резюме аналогичный [требованиям заполнения существующего резюме](#conditions).

### Ответ
`200 OK` - условия заполнения полей получены успешно

### Ошибки
`403 Forbidden` - авторизованный пользователь не соискатель


<a name='conditions-contacts'></a>
## Условия заполнения контактов в резюме
При заполнении контактов в резюме необходимо учитывать следующие условия:

 * В резюме обязательно должен быть указан email (и он может быть только один).

 * В резюме должен быть указан хотя бы один телефон, причём можно указывать
   только один телефон каждого типа.
   
 * Комментарий можно указывать только для телефонов, для email комментарий
   не сохранится.

 * В контакте типа 'email' value — это email, а для телефонов — объект.


Пример сообщения для изменения контактов в резюме:
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
                "formatted": "+7(499)9078456"
            },
            "comment": "Звонить до 21:00"
        }
    ]
}
```

Обязательно указать либо телефон полностью в поле `formatted`, либо все три части телефона по отдельности в
полях `country`, `city` и `number`. Если указано и то, и то, используются данные из разделенного телефона.
В поле `formatted` допустимо указание дополнительных символов: пробелов, скобок, дефисов.
В раздельных полях допустимы только цифры.


<a name='conditions-other'></a>
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

Отличается от полного представления отсутствием некоторых полей. Например, если указано более одно среднего образования - вернется только уровень образования. 

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
        "primary": [],
        "level": {
            "id": "secondary",
            "name": "Среднее"
        },
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
Соискатель может скачать свои резюме.  
Название скачиваемого файла может содержать имя соискателя или его желаемую должность.

### Запрос

Для скачивания резюме нужно использовать полученный из ответа API url, передавая [стандартные для API заголоки](general.md#request-requirements).

```
GET https://....(ссылка, полученная в полной или сокращенной выдаче резюме API)
```

### Ответ

Успешный ответ приходит с кодом 200 и содержит в теле запрашиваемый файл.

### Ошибки

* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `429 Too Many Requests` - если превышен лимит просмотров резюме в сутки (при авторизации работодателем).
* `403 Forbidden` - Не хватает услуг для скачивания резюме с контактами

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

#### Запрос

```
GET /resumes/{resume_id}/access_types
```

где:
* `resume_id` — идентификатор резюме

#### Ответ

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

#### Ошибки

* `403 Forbidden` — пользователь не является соискателем.
* `404 Not Found` — резюме с указанным идентификатором не найдено или недоступно текущему пользователю.


См. также [управление списками видимости резюме](/docs/resume_visibility.md).


<a name="views"></a>
## История просмотра резюме

`GET /resumes/{resume_id}/views` вернёт историю просмотров резюме. На основном
сайте это доступно при клике на кол-во просмотров резюме на странице со списком
резюме текущего пользователя
([https://hh.ru/applicant/resumes](https://hh.ru/applicant/resumes)).

Количество просмотров (в том числе, новых) выдаётся при запросе конкретного
резюме и списка резюме. Счетчик новых просмотров обнуляется при запросе данного
ресурса.

### Ответ

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
    "found": 1,
    "resume": {
        "id": "502ff8b100018bddf30039ed1f63735f4dda66",
        "title": "консультант",
        "url": "https://api.hh.ru/resumes/502ff8b100018bddf30039ed1f63735f4dda66"
    }
}
```

где:

 Имя | Тип | Описание
 --- | --- | --------
 found | число | Количество записей о просмотре резюме ( ≥ 0 )
 pages | число | Количество страниц ( ≥ 0 )
 per_page | число | Количество элементов на страницу ( > 0 )
 page | число | Номер текущей страницы ( ≥ 0 )
 resume | объект | [Короткое представление резюме](#resume-nano)

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

### Ошибки

* `403 Forbidden` — пользователь не является соискателем.
* `404 Not Found` — резюме с указанным идентификатором не найдено или недоступно текущему пользователю.

<a name="similar"></a>
## Поиск по вакансиям, похожим на резюме

Данные доступны только автору резюме.


### Запрос

`GET /resumes/{resume_id}/similar_vacancies`

где `resume_id` - идентификатор резюме.

Принимает те же параметры, что и [поиск по вакансиям](vacancies.md#search-params).

При указании параметров пагинации (page, per_page) работает ограничение: глубина
возвращаемых результатов не может быть больше 2000. Например, возможен запрос
`per_page=10&page=199` (выдача с 1991 по 2000 вакансию), но запрос с
`per_page=10&page=200` вернёт ошибку (выдача с 2001 до 2010 вакансию).

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело в том же виде, 
что и [поиск по вакансиям](vacancies.md#search-results)

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой
* `404 Not Found` - резюме с идентификатором `resume_id` не существует или недоступно


<a name="hidden-fields"></a>
## Скрытые поля в анонимном резюме

В поле `hidden_fields` содержится список скрытых соискателем полей анонимного резюме. Скрытые поля заменяются на `null`. Автору резюме выдаются актуальные данные.

Скрываемые поля в зависимости от значения в поле:
* `names_and_photo` — заменяет на `null` значение полей `first_name`, `last_name`, `middle_name` и `photo`.
* `phones` — заменяет на `null` значение поля `contact[].value` с полем `contact[].type`, равным `cell`, `work` или `home`
* `email` — заменяет на `null` значение поля `contact[].value` с полем `contact[].type`, равным `email`
* `other_contacts` — заменяет на `null` значение полей `site[].url`
* `experience` — заменяет на `null` поля `experience[].company`, `experience[].company_id`, `experience[].company_url`, `experience[].employer`; заменяет значение поля `recommendation` на пустой список
