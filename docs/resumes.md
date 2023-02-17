# Резюме

* [Список резюме авторизованного пользователя](#mine)
* [Просмотр резюме](#item)
  * [Дополнительные поля для автора резюме](#additional-author-fields)
  * [Платные услуги для соискателя, связанные с резюме](#applicant-paid-services)
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
* [Статусы резюме](#status)
* [Видимость резюме](#access_type)
  * [Списки видимости резюме](#visibility_lists)
  * [Получение списка типов видимости резюме](#get_access_types)
* [История просмотра резюме](#views)
* [Поиск по вакансиям, похожим на резюме](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume)

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
            "next_publish_at": "2021-07-02T21:29:45+0300",
            "contact":[    
                {
                    "value": {
                        "country":"7",
                        "city":"926",
                        "number":"2222222",
                        "formatted":"+7 (926) 222-22-22"
                    },
                    "type": {
                        "id":"cell",
                        "name":"Мобильный телефон"
                    },
                    "preferred":true,
                    "comment":"Mobile",
                    "verified":false
                },
                {
                  "type": {
                    "id":"email",
                    "name":"Эл. почта"
                  },
                  "value":"test@gmail.com",
                  "preferred":false
                }
            ],
            "platform": {
              "id": "headhunter"
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
contact | array | [список контактов соискателя](employer_resumes.md#contact-object)
<a name="item"></a>
## Просмотр резюме

`GET /resumes/{resume_id}`

где `resume_id` – идентификатор резюме.

Для авторизованного автора возвращается
[более детальная информация](#additional-author-fields), включая тип
видимости, комментарии модераторов и статус.
Если резюме - анонимное, автору выдаются актуальные [данные](employer_resumes#hidden-fields) 

### Ответ
[Пример ответа](employer_resumes.md#item-response)

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
[в справочнике `resume_moderation_note`](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

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
* `gender` — пол. Элемент справочника [gender](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
* `photo` — фотография пользователя. см. [артефакты](https://api.hh.ru/openapi/redoc#tag/Rabota-s-artefaktami);
* `portfolio` — портфолио пользователя. см. [артефакты](https://api.hh.ru/openapi/redoc#tag/Rabota-s-artefaktami);
* `area` — город проживания. Элемент справочника [areas](areas.md);
* `metro` — ближайшая станция метро. Элемент справочника [metro](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-metro-stations). Если передать метро не принадлежащее переданной `area`, поле проигнорируется
  Имеет смысл указывать только для `area` с метро;
* `relocation` — возможен ли переезд в другой город. Состоит из полей:
    * `type` — элемент справочника [relocation_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
    * `area` — город, в который возможен переезд (список). Имеет смысл
      только с соответствующим полем `type`. Элемент справочника
      [areas](areas.md);
* `business_trip_readiness` — готовность к командировкам. Элемент справочника
  [business_trip_readiness](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `contact` — контактная информация (список). 
Про обязательность полей и данных смотрите в [условиях заполнения контактов](#conditions-contacts). 
Состоит из полей:
    * `type` — элемент справочника [preferred_contact_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
    * `value` — значение контакта. Для телефона состоит из четырех полей (`country `, `city`, `number`, `formatted`),
      для электронного адреса — строка.
    * `preferred` — предпочитаемый вид связи (`true` или `false`);
    * `comment` — комментарий к контакту;
* `site` — присутствие на других сайтах. Состоит из полей:
    * `type` — тип сайта. Элемент справочника
      [resume_contacts_site_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
    * `url` — ссылка на профиль, либо идентификатор на стороннем сайте/сервисе;
* `title` — желаемая должность;
* `professional_roles` — профессиональные роли соискателя (список). Элемент справочника
  [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary);
* `salary` — желаемая зарплата. Состоит из полей:
    * `amount` — сумма;
    * `currency` — идентификатор [валюты](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
* `employments` — занятость. Элементы справочника [employment](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `schedules` — график работы. Список из элементов справочника [schedule](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
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
          [справочника факультетов](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-educational-institutions-dictionary);
        * `result` — специальность / специализация;
        * `result_id` — идентификатор специальности / специализации, можно
          получить из
          [подсказок по специализациям](suggests.md#specializations);
        * `year` — год окончания;
    * `level` — уровень образования. Элемент справочника
      [education_level](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `language` — владение языками (список). 
    * `id` - значение из справочника [languages](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-languages) 
    * `level` - значение из справочника [language_level](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `experience` — опыт работы (список). Состоит из полей:
    * `company` — организация;
    * `company_id` — идентификатор организации, можно получить из
      [подсказок по организациям](suggests.md#companies);
    * `area` — регион расположения организации. Элемента справочника
      [areas](areas.md);
    * `company_url` — сайт компании;
    * `industries` — отрасли компании. Элемент справочника
      [/industries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-industries)
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
  [travel_time](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
* `recommendation` — рекомендации (список). Состоит из полей:
    * `name` — имя;
    * `position` — должность;
    * `organization` — организация;
* `resume_locale` — локаль резюме. Элемент справочника [локали резюме](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-locales-for-resume).
* `driver_license_types` - cписок категорий водительских прав соискателя. Элемент справочника [тип водительских прав](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
* `has_vehicle` - наличие личного автомобиля у соискателя
* `hidden_fields` - [скрытые поля](#hidden-fields) в резюме (список). Элемент справочника [resume_hidden_fields](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
* `access` - [видимость резюме](#access_type)
    * `type` - тип видимости. Элемент справочника [resume_access_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)

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
not_available | недопустимое значение

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
  * не заполнены обязательные поля (чтобы понять, что именно не заполнено, можно вызвать урл [получения резюме](#item) и посмотреть поле `mandatory`),
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
 
<a name="status"></a>
## Статус резюме

Ключ `status` определяет текущее состояние резюме и содержит элемент
справочника [resume_status](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). После создания нового резюме оно
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
элемент справочника [resume_access_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

<a name="access_type_restrictions"></a>
‼️ С первого сентября 2021 года тип видимости с id `everyone` (видно всему интернету) стал недоступен для сохранения из-за ограничений законодательства.

 Код | Описание
 --- | --------
 no_one | Резюме такого типа никому не видно. Но им можно откликнуться на вакансию, при этом резюме сменит тип на `whitelist`.
 whitelist | Резюме не видно никому, кроме указанных компаний. Если откликнуться на вакансию компании, которая не входит в список, компания автоматически в него попадёт. См. [списки видимости резюме](#visibility_lists).
 blacklist | Резюме доступно для поиска и просмотра всем компаниям, за исключением указанных. Если откликнуться на вакансию компании из черного списка, то компания вычеркивается из него автоматически. См. [списки видимости резюме](#visibility_lists).
 clients | Резюме доступно всем зарегистрированным компаниям на hh.ru.
 everyone | Резюме доступно всем без исключения (всему интернету). Этот тип [не доступен для сохранения](#access_type_restrictions).
 direct | Резюме доступно только по прямой ссылке (ссылка указана в ключе `alternate_url`).

<a name="visibility_lists"></a>
### Списки видимости резюме

Некоторые типы видимости, например `whitelist` и `blacklist`, подразумевают наличие списка работодателей,
для которых резюме должно быть видимо или скрыто. См. [управление списками видимости резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti).


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


См. также [управление списками видимости резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti).


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
 resume | объект | [Короткое представление резюме](employer_resumes.md#resume-nano)

В элементе `items` содержатся данные о откликах:

 Имя | Тип | Описание
 --- | --- | ---
 created_at | строка | Дата создания записи, дата просмотра резюме работодателем
 viewed | логический | отметка о просмотре записи (при запросе данного ресурса все запросы помечаются просмотренными)
 employer | объект | информация о компании (см. ниже)

Объект `employer` возвращает краткие данные о компании, является
«подмножеством» объекта [компания/работодатель](https://api.hh.ru/openapi/redoc#tag/Rabotodatel).

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

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume)
