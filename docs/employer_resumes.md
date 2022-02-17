# Резюме

* [Просмотр резюме](#item)
  * [Дополнительные поля для работодателя](#additional-employer-fields)
  * [Платные услуги для работодателя, связанные с резюме](#paid-services)
* [Короткое представление резюме](#resume-nano)
* [Сокращенное представление резюме](#resume-short)
* [Ссылки на скачивание резюме в нескольких форматах](#download-links)
* [Скрытые поля в резюме](#hidden-fields)


<a name="item"></a>
## Просмотр резюме

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Для работодателя данный метод требует наличия [платного доступа](/docs/payable/employer_methods.md)

`GET /resumes/{resume_id}`

где `resume_id` – идентификатор резюме.

>!! Внимание произошли изменения в доступе к контактной информации. Прочитайте внимательно информацию про [поконтактный доступ к резюме](payable/resume.md#contact-data)

Для работодателя, если просмотр полных данных по резюме недоступен при текущей
авторизации, в некоторых полях будет `null`, а поле `can_view_full_info` будет
иметь значение `false`.

После вызова этого урла, если у работодателя есть отклик/приглашение на это резюме, отклик будет считаться просмотренным.

<a name="item-response"></a>
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
    "marked": false,
    "professional_roles": [
        {
            "id": 5,
            "name": "Автослесарь, автомеханик"
        }
    ]
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
professional_roles | [array](#professional-role-object) | Массив объектов профролей


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

<a name="professional-role-object"></a>
Объект с именем и идентификатором

Имя | Тип | Описание
-----|-----|---------
id | string | Идентификатор поля.
name | string | Название поля.


### Ошибки

* `403 Forbidden` - неверная авторизация. Ожидается авторизация пользователя.
* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `429 Too Many Requests` - если превышен лимит просмотров резюме в сутки
  (при авторизации работодателем).

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#resumes).


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
[запроса на получение резюме](employer_resumes.md#item) передан дополнительный параметр
`with_negotiations_history`. В этом случае GET запрос должен иметь вид:

`GET /resumes/{resume_id}?with_negotiations_history=true`

Формат поля `negotiations_history.vacancies` подробно описан на странице
[полной истории откликов/приглашений по резюме](resume_negotiations_history.md#response) и различается лишь тем, что
в данном случае список будет ограничен 3-мя вакансиями данного работодателя и последним изменением состояния
отклика/приглашения по каждой из этих вакансий.

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

<a name="hidden-fields"></a>
## Скрытые поля в анонимном резюме

В поле `hidden_fields` содержится список скрытых соискателем полей анонимного резюме. Скрытые поля заменяются на `null`.

Скрываемые поля в зависимости от значения в поле:
* `names_and_photo` — заменяет на `null` значение полей `first_name`, `last_name`, `middle_name` и `photo`.
* `phones` — заменяет на `null` значение поля `contact[].value` с полем `contact[].type`, равным `cell`, `work` или `home`
* `email` — заменяет на `null` значение поля `contact[].value` с полем `contact[].type`, равным `email`
* `other_contacts` — заменяет на `null` значение полей `site[].url`
* `experience` — заменяет на `null` поля `experience[].company`, `experience[].company_id`, `experience[].company_url`, `experience[].employer`; заменяет значение поля `recommendation` на пустой список
