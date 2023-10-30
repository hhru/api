# Переписка (отклики/приглашения) для работодателя

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Методы требуют наличия [платного доступа для работодателя](/docs/payable/employer_methods.md)

*Документация по переписке для соискателя доступна в [отдельной статье](negotiations.md).*

* [Модель работы, термины и процедуры](#model)
* [Общее описание процесса работы с откликами/приглашениями](#flow)
* [Коллекции и работодательские состояния откликов/приглашений](#collections)
* [Список откликов/приглашений](#negotiations-list)
* [Просмотр отклика/приглашения](#get-negotiation)
* [Просмотр списка сообщений в отклике/приглашении](#get-messages)
* [Отправка сообщения в отклике/приглашении](#add-messages)
* [Приглашение соискателя на вакансию](#add-invite)
* [Действия по отклику/приглашению (смена состояния)](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-negotiations-collection-to-next-state)
* [Просмотр предпочитаемой сортировки откликов](#get-preference-order)
* [Изменение предпочитаемой сортировки откликов](#update-preference-order)
* [Отметить отклики прочитанными](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/post-negotiations-topics-read) 


<a name="model"></a>
## Модель работы, термины и процедуры

Отклики и приглашения соответствуют модели, которая выражается в запросах и
ответах API. Если приложение использует модель правильно, то изменение
бизнес-логики откликов и приглашений не будет требовать переработки или
исправления.

В откликах и приглашениях используются понятия:

* *отклик* – объект, порождённый по инициативе соискателя (отклик на вакансию). 
  Отклик всегда происходит одним резюме на одну вакансию.

* *приглашение* – объект, порождённый по инициативе работодателя (приглашение на вакансию). 
  Приглашение всегда происходит к одному резюме на одну вакансию.

Кроме процесса появления объекта, работа с откликом или приглашением происходит
одинаково.

* <a name="term-collection"></a> *коллекция* – набор откликов/приглашений,
  объединённых по определённым критериям. Коллекции используются, когда в вашем
  приложении требуется **отобразить** список откликов/приглашений. Не стоит
  полагаться на то, что в определённые этапы обработки отклика/приглашения
  оно будет входить в известные коллекции, так как эта логика может изменяться.

* <a name="term-state"></a> *соискательское состояние отклика/приглашения* –
  статус отклика/приглашения ([поле `state`](#negotiations-list-item)), который **видит соискатель**. Возможные значения
  выдаются [в справочнике `negotiations_state`](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) и
  не зависят от вакансии в отклике/приглашении.

* <a name="term-employer-state"></a> *работодательское состояние отклика/приглашения* –
  статус отклика/приглашения у работодателя. Может отличаться от
  соискательского. Список возможных статусов
  **зависит от вакансии и работодателя**, поэтому список
  [необходимо запрашивать](#states), передавая нужную вакансию.

* <a name="term-action"></a> *действие по отклику/приглашению* – действие, которое
  можно выполнить над откликом/приглашением. В результате действия
  работодательское и соискательское состояния отклика/приглашения могут как
  поменяться, так и остаться прежними.

Не следует путать *действие*, *коллекцию* и *состояние* – они могут быть похожи,
но предназначены для разных целей.


<a name="flow"></a>
## Общее описание процесса работы с откликами/приглашениями

Вся работа с откликами/приглашениями происходит в рамках
**одной выбранной вакансии**. Даже у одного работодателя могут быть вакансии
с различными правилами работы по откликам/приглашениям.

Сначала необходимо получить список
[коллекций и работодательских состояний](#collections). Используйте коллекции
для **получения списков откликов/приглашений**. Предлагайте пользователю
выбирать, какую из коллекций он хочет получить. Для получения всех
откликов/приглашений нужно последовательно получить все коллекции. Список
состояний используется только как справочник.

Для **создания приглашения** необходимо запросить вакансии работодателя,
применимые к выбранному резюме. Получить эту информацию можно в
[списке вакансий работодателя](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-active-vacancy-list), там же
будут указаны необходимые параметры (ключ `arguments`) и состояние созданного
отклика (ключ `resulting_employer_state`). У разных работодателей и разных
вакансий могут быть различные правила и состояния добавляемого отклика. Для
каждой пары *вакансия + резюме* может быть только один отклик/приглашение.

Для создания приглашения, работодатель должен иметь активированный доступ к базе
резюме. Для работы с существующим откликом/приглашением доступ не требуется. Это
позволяет обрабатывать отклики на вакансии, даже не имея доступ к базе резюме.

Если вам необходимо **совершить действие** по отклику/приглашению,
ориентируйтесь на [список действий](#actions-info), который будет доступен в
[списке (коллекции) откликов/приглашений](#negotiations-list) и в
[отдельном отклике/приглашении](#get-negotiation). Если действие приводит
к смене состояния по отклику/приглашению, это будет явно указано в ключе
`resulting_employer_state`. Не все действия приводят к смене состояния.

После приглашения соискателя вы можете начать с ним
[свободную переписку](#get-messages). Вы сможете
[отправлять сообщения](#add-messages), а соискатель – вам отвечать.
При необходимости переписку для конкретной вакансии
[можно отключить](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/get-vacancy) (поле `allow_messages`).

Чтобы соискательский отклик считался просмотренным работодателем необходимо сделать одно из следующих действий:
* запросить список сообщений по урлу, 
пришедшему при запросе [списка (коллекции) откликов/приглашений](#negotiations-list) или 
[отдельного отклика/приглашения](#get-negotiation),
* [запросить сообщения](#get-messages) по отклику
* запросить резюме по урлу, пришедшему при запросе [списка (коллекции) откликов/приглашений](#negotiations-list) 
или [отдельного отклика/приглашения](#get-negotiation)
* с помощью отдельного метода [отметить определенные отклики как прочитанные](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/post-negotiations-topics-read)


<a name="states"></a>
<a name="collections"></a>
## Коллекции и работодательские состояния откликов/приглашений по вакансии

У работодателя доступны коллекции откликов и приглашений. Список этих коллекций
может меняться в зависимости от конкретной вакансии.

Получить доступные у текущего пользователя вакансии можно через
[списки вакансий работодателя](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-active-vacancy-list).

В данный момент нет коллекции, которая объединяла бы все отклики/приглашения по
вакансии. Если вам необходимо получить полный список – запросите последовательно
все коллекции.


### Запрос

`GET /negotiations?vacancy_id={vacancy_id}&with_generated_collections={true|false}`

где `vacancy_id` - id вакансии, `with_generated_collections` - Добавить в выдачу информацию по сгенерированным [коллекциям](#term-collection) откликов/приглашений для данной вакансии, значение по умолчанию — `false`

<a name="collections_response"></a>
### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "collections": [
        {
            "id": "somecollection",
            "name": "Название коллекции",
            "description": "Описание коллекции",
            "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456",
            "counters": {
                "with_updates": 4,
                "total": 5
            },
            "order_types": [
                {
                    "id": "last_change_time_except_employer_inbox",
                    "name": "По дате создания и активности соискателя",
                    "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456&order_by=last_change_time_except_employer_inbox"
                },
                {
                    "id": "relevance",
                    "name": "лучшие",
                    "url": "https://api.hh.ru/negotiations/somecollection?vacancy_id=123456&order_by=relevance"
                }
            ]
        },
        {
            "id": "anothercollection",
            "name": "Название другой коллекции",
            "url": "https://api.hh.ru/negotiations/anothercollection?vacancy_id=123456",
            "counters": {
                "with_updates": 0,
                "total": 1
            },
            "order_types": [
                {
                    "id": "last_change_time_except_employer_inbox",
                    "name": "По дате создания и активности соискателя",
                    "url": "https://api.hh.ru/negotiations/anothercollection?vacancy_id=123456&order_by=last_change_time_except_employer_inbox",
                }
            ]
        }
    ],
    "generated_collections": [
        {
            "id": "some_generated_collection",
            "name": "Название сгенерированной коллекции",
            "description": "Описание сгенерированной коллекции",
            "url": "https://api.hh.ru/negotiations/some_generated_collection?vacancy_id=123456",
            "counters": {
                "with_updates": 4,
                "total": 5
            },
            "order_types": [
                {
                    "id": "last_change_time_except_employer_inbox",
                    "name": "По дате создания и активности соискателя",
                    "url": "https://api.hh.ru/negotiations/some_generated_collection?vacancy_id=123456&order_by=last_change_time_except_employer_inbox"
                },
                {
                    "id": "relevance",
                    "name": "лучшие",
                    "url": "https://api.hh.ru/negotiations/some_generated_collection?vacancy_id=123456&order_by=relevance"
                }
            ]
        }
    ],
    "employer_states": [
        {
            "id": "response",
            "name": "Отклик"
        },
        {
            "id": "invitation",
            "name": "Приглашение"
        },
        {
            "id": "discard",
            "name": "Отказ"
        },
        {
            "id": "discard_after_interview",
            "name": "Отказ после интервью"
        }
    ]
}

```

Имя | Тип | Описание
--- | --- | --------
collections | список | [коллекции](#term-collection) откликов/приглашений для данной вакансии
collections[].id | строка | идентификатор коллекции, уникальный как минимум для данной вакансии
collections[].name | строка | название коллекции
collections[].description | строка | описание коллекции
collections[].url | строка | url, на который необходимо делать GET запрос для получения откликов/приглашений данной коллекции
collections[].counters.with_updates | число | количество откликов/приглашений в коллекции, [требующих внимания](#has_updates)
collections[].counters.total | число | общее количество откликов/приглашений в коллекции
collections[].order_types | список | <a name="order-types"></a> возможные варианты сортировки откликов/приглашений в коллекции
generated_collections | список | сгенерированные [коллекции](#term-collection) откликов/приглашений для данной вакансии. Данные коллекции не привязаны к статусу отклика, как, например, "Подумать", "Интервью" или "Предложение о работе", а созданы для облегчения работы пользователя.
generated_collections[].id | строка | идентификатор сгенерированной коллекции, уникальный как минимум для данной вакансии. Возможные варианты: vacancy_visitors, relevant_responses, by_location, phone_calls.
generated_collections[].name | строка | название сгенерированной коллекции
generated_collections[].description | строка | описание сгенерированной коллекции
generated_collections[].url | строка | url, на который необходимо делать GET запрос для получения откликов/приглашений данной коллекции
generated_collections[].counters.with_updates | число | количество откликов/приглашений в сгенерированной коллекции, [требующих внимания](#has_updates)
generated_collections[].counters.total | число | общее количество откликов/приглашений в сгенерированной коллекции
generated_collections[].order_types | список | <a name="order-types"></a> возможные варианты сортировки откликов/приглашений в сгенерированной коллекции
employer_states | список | [работодательские состояния](#term-employer-state) откликов/приглашений данной вакансии
employer_states[].id | строка | идентификатор состояния, уникальный как минимум для данной вакансии
employer_states[].name | строка | название состояния

### Ошибки

* `400 Bad Request` - если параметр `vacancy_id` не передан или передано не правильное значение
* `404 Not Found` - у пользователя нет доступа к вакансии или вакансия не существует 

<a name="negotiations-list"></a>
## Список откликов/приглашений


### Запрос

Получив `collections[].url` из [списка коллекций](#collections) нужно сделать GET запрос на него, например:

`GET https://api.hh.ru/negotiations/somecollection?vacancy_id=123456`

Некоторые параметры принимают множественные значения: `key=value&key=value`. Если параметр может принимать несколько значений, об этом явно указано в его описании.
Коллекция `phone_calls` принимает только параметры `vacancy_id`, `order_by`, `page` и `per_page` из таблицы ниже.

Параметры:

Имя | Обязательный | Описание
--- | ------------ | --------
vacancy_id | да | Идентификатор вакансии
order_by | нет | Тип сортировки. Возможные значения могут отличаться у разных коллекций, варианты указаны в [списке коллекций в поле `order_types`](#order-types).
page | нет | Номер страницы, по умолчанию: 0
per_page | нет | Количество выдаваемых элементов на страницу, по умолчанию: 20, максимальное значение: 50
age_from | нет | Возраст соискателя в годах, диапазон от
age_to | нет | Возраст соискателя в годах, диапазон до
area | нет | Регион. Можно передать множественные значения. Возможные значения: [/areas](https://github.com/hhru/api/blob/master/docs/areas.md)
citizenship | нет | Страна желаемого гражданства. Можно передать множественные значения. Возможные значения можно посмотреть в [справочнике стран](areas.md#countries)
currency | нет | Код валюты. Возможные значения: `currency` (ключ code) в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries
driver_license_types | нет | Категории водительских прав. Можно передать множественные значения. Возможные значения: `driver_license_types` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
educational_institution | нет | Идентификатор [учебного заведения](https://github.com/hhru/api/blob/master/docs/suggests.md). Можно передать множественные значения
education_level | нет | Образование. Возможные значения: `education_level` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
experience | нет | Опыт работы. Можно передать множественные значения. Возможные значения: `experience` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
gender | нет | Пол. Возможные значения: `gender` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
language | нет | Знание языков. Можно передать множественные значения. Задается в формате language.level, где: `language` — значение из справочника [/languages](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-languages), `level` — значение из справочника `language_level` [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
relocation | нет | Готовность к переезду. Возможные значения: `resume_search_relocation` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
salary_from | нет | Желаемая заработная плата, диапазон от
salary_to | нет | Желаемая заработная плата, диапазон до
search_radius_meters | нет | Расстояние до потенциального кандидата (в метрах)
search_text | нет | Поисковая строка
show_only_new_responses | нет | Показывать только новые отклики (то есть отклики, которые не были просмотрены). Только для коллекции "Все неразобранные" (`/responses`)
show_only_with_vehicle | нет | Фильтровать по наличию автомобиля
show_only_new | нет | Показывает отклики, в которых есть новые сообщения. Для коллекций, **отличных от** "Все неразобранные" (`/responses`)

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "ordered_by": {
        "id": "last_change_time_except_employer_inbox",
        "name": "По дате создания и активности соискателя"
    },
    "found": 12,
    "pages": 1,
    "page": 0,
    "per_page": 20,
    "items": [
        {
            "id": "123456789",
            "created_at": "2015-05-14T00:00:00+0300",
            "updated_at": "2015-05-14T12:00:05+0300",
            "has_updates": true,
            "state": {
                "id": "response",
                "name": "Отклик"
            },
            "employer_state": {
                "id": "response",
                "name": "Отклик"
            },
            "actions": [
                {
                    "id": "invitation",
                    "name": "Пригласить",
                    "enabled": true,
                    "method": "PUT",
                    "url": "https://api.hh.ru/negotiations/somecollection/123456789",
                    "resulting_employer_state": {
                        "id": "invitation",
                        "name": "Приглашение"
                    },
                    "templates": [
                        {
                            "id": "invite_after_response",
                            "name": "Приглашение откликнувшегося соискателя",
                            "quick": false,
                            "url": "https://api.hh.ru/message_templates/invite_after_response?topic_id=123456789"
                        }
                    ],
                    "arguments": [
                        {
                            "id": "message",
                            "required": true,
                            "required_arguments": []
                        },
                        {
                            "id": "send_sms",
                            "required": false,
                            "required_arguments": [
                                {
                                    "id": "message"
                                }
                            ]
                        },
                        {
                            "id": "address_id",
                            "required": false,
                            "required_arguments": [
                                {
                                    "id": "message"
                                }
                            ]
                        }
                    ]
                },
                {
                    "id": "hold",
                    "name": "Подумать",
                    "enabled": true,
                    "method": "PUT",
                    "url": "https://api.hh.ru/negotiations/hold/123456789",
                    "arguments": [],
                    "resulting_employer_state": null,
                    "templates": []
                }
            ],
            "url": "https://api.hh.ru/negotiations/123456789",
            "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
            "viewed_by_opponent": false,
            "resume": {
                "id": "0123456789abcdef",
                "title": "Начинающий специалист",
                "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
                "first_name": "Иван",
                "last_name": "Иванов",
                "middle_name": "Иванович",
                "age": 19,
                "can_view_full_info": true,
                "alternate_url": "https://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
                            "result": "",
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
                                "name": "Интернет-компания  (поисковики, платежные системы, соц.сети, информационно-познавательные и развлекательные ресурсы, продвижение сайтов и прочее)"
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
            },
            "templates": [
                {
                    "url": "https://api.hh.ru/message_templates/discard_after_interview?topic_id=123456789",
                    "id": "discard_after_interview"
                }
            ],
            "counters": {
                "messages": 100,
                "unread_messages": 50
            },
            "source": "NEGOTIATION",
            "test_result": {
                "url": "https://api.hh.ru/negotiations/1359970704/test/solution",
                "alternate_url": "https://hh.ru/employer/vacancy_response/test?topicId=1359970704",
                "score": 100,
                "mark": "EXCELLENT"
            }
        }
    ]
}
```

где:

Имя | Тип | Описание
--- | --- | --------
ordered_by | объект | Использованный тип сортировки
found | число | Количество найденных откликов ( ≥ 0 )
pages | число | Количество страниц с откликами ( ≥ 1 )
per_page | число | Количество элементов на страницу ( > 0 )
page | число | Номер текущей страницы ( ≥ 0 )

<a name="negotiations-list-item"></a>
В элементе `items` содержатся данные о откликах/приглашениях и резюме к ним:

Имя | Тип   | Описание
--- | ----- | --------
id | строка | Идентификатор отклика
created_at | строка | Дата и время создания отклика/приглашения
updated_at | строка | Дата и время последнего обновления отклика/приглашения
state | объект | Текущее [соискательское состояние отклика](#term-state).
employer_state | объект | Текущее [работодательское состояние отклика](#term-employer-state).
actions | список | возможные [действия по отклику/приглашению](#actions-info)
url | строка | url для получения [полной версии отклика/приглашения](#get-negotiation)
messages_url | строка | url для получения [списка сообщений в отклике](#get-messages)
resume | объект, null | [Сокращенное представление резюме](employer_resumes.md#resume-short). Для получения полного резюме необходимо запросить его GET запросом по url из ключа `url`. Может быть `null`, если соискатель удалил резюме или закрыл к нему доступ.
has_updates | логический | <a name="has_updates"></a> Есть ли в отклике/приглашении обновления, требующие внимания. Флаг сбрасывается при различных действиях по отклику/приглашению, например, [просмотре списка сообщений](#get-messages), а также при [правильном просмотре резюме из отклика/приглашения](#view-resume).
viewed_by_opponent | логический | Был ли отклик просмотрен соискателем
counters | объект | Счётчики
counters.messages | число | Общее количество сообщений
counters.unread_messages | число | Количество непрочитанных работодателем сообщений
test_result | обьект, null | Результат [теста](employer_negotiations_test.md) прикрепленного к вакансии
test_result.url | строка | Ссылка на результат теста
test_result.alternate_url | строка | Ссылка на результат теста на сайте
test_result.score | число | Результат прохождения теста (от 0 до 100)
test_result.mark | строка | Оценка дифференцированная (`UNFAIR` - от 0 до 14  баллов, `FAIR` - от 15 до 44 баллов, `GOOD` - от 45 до 79 баллов, `EXCELLENT` от 80 до 100 баллов)
source | строка | Источник отклика. Возможные значения NEGOTIATION, PHONE_CALL, CHAT, VR.

<a name="view-resume"></a>

В списке откликов/приглашений предоставлена только основная информация о резюме.
Для получения полной информации, в частности контактной информации соискателя,
необходимо запросить полное резюме. У соискателя запрос резюме будет отражён в
истории просмотров.

**Важно!** Дополнительный запрос на получение данных о резюме **необходимо**
выполнять именно по url из JSON ответа. Только в таком случае запрос будет
правильно учтён в истории просмотров. Например, при запросе резюме из отклика
на анонимную вакансию, в истории будет отражено анонимное название компании.

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой
* `404 Not Found` - вакансия, по которой запрашиваются отклики, 
не существует или недоступна текущему пользователю


<a name="actions-info"></a>
### Действия по отклику/приглашению (`actions`)

Количество действий может быть разное, в том числе список действий может быть пустым.

По каждому действию указано:

Имя | Тип | Описание
--- | --- | --------
id | строка | Идентификатор действия
name | строка | Название действия
enabled | логический | Возможно ли действие совершить
method | строка | HTTP метод, который необходимо выполнить
url | строка | url, на который необходимо выполнить запрос
resulting_employer_state | объект, null | [работодательское состояние](#term-employer-state) по отклику/приглашению, которое будет после совершения действия. Если действие не меняет состояние – `null`.
templates | список | Шаблоны писем. Содержит идентификатор шаблона и url для [получения текста по шаблону](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-mail-templates).
agruments | список | Обязательные и дополнительные аргументы для запроса

К действию прилагается список аргументов, на данный момент могут встретиться такие:

* `message` - сообщение, которое будет отправлено соискателю на электронную почту. Используйте [шаблоны](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-mail-templates) для получения текстов.
* `address_id` - идентификатор [адреса](https://api.hh.ru/openapi/redoc#tag/Adresa-rabotodatelya), который будет указан в приглашении
* `send_sms` – уведомлять ли соискателя о приглашении с помощью sms. Чтобы отправить – передайте `true`, значение по умолчанию — `false`. Обратите внимание: в sms-сообщении используется стандартный текст, изменить его нельзя.

Приложение должно уметь заполнять данные аргументы. В будущем могут появляться
и другие аргументы, но они не будут обязательными. Обязательность аргументов
может быть разная для разных откликов/приглашений.

По каждому аргументу будет указано:

Имя | Тип | Описание
--- | --- | --------
id | строка | Идентификатор аргумента
required | логический | Обязательность аргумента
required_arguments | список | Аргументы, которые необходимо приложить, если указан данный аргумент. Например, адрес является необязательным, но при его указании необходимо указать также и сообщение.


<a name="get-negotiation"></a>
## Просмотр отклика/приглашения

Для того, чтобы просмотреть полную информацию об отклике необходимо перейти по урлу (поле `items[].url`), 
полученному в [списке откликов/приглашений](#negotiations-list), например:

`GET /negotiations/123456789`

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "id": "123456789",
    "created_at": "2015-05-14T00:00:00+0300",
    "updated_at": "2015-05-14T12:00:05+0300",
    "has_updates": true,
    "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
    "messaging_status": "ok",
    "state": {
        "id": "response",
        "name": "Отклик"
    },
    "employer_state": {
        "id": "response",
        "name": "Отклик"
    },
    "actions": [
        {
            "id": "invitation",
            "name": "Пригласить",
            "enabled": true,
            "method": "PUT",
            "url": "https://api.hh.ru/negotiations/somecollection/123456789",
            "resulting_employer_state": {
                "id": "invitation",
                "name": "Приглашение"
            },
            "templates": [
                {
                    "id": "invite_after_response",
                    "name": "Приглашение откликнувшегося соискателя",
                    "quick": false,
                    "url": "https://api.hh.ru/message_templates/invite_after_response?topic_id=123456789"
                }
            ],
            "arguments": [
                {
                    "id": "message",
                    "required": true,
                    "required_arguments": []
                },
                {
                    "id": "send_sms",
                    "required": false,
                    "required_arguments": [
                        {
                            "id": "message"
                        }
                    ]
                },
                {
                    "id": "address_id",
                    "required": false,
                    "required_arguments": [
                        {
                            "id": "message"
                        }
                    ]
                }
            ]
        },
        {
            "id": "hold",
            "name": "Подумать",
            "enabled": true,
            "method": "PUT",
            "url": "https://api.hh.ru/negotiations/hold/123456789",
            "arguments": [],
            "resulting_employer_state": null,
            "templates": []
        }
    ],
    "viewed_by_opponent": false,
    "resume": {
        "id": "0123456789abcdef",
        "title": "Начинающий специалист",
        "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
        "first_name": "Иван",
        "last_name": "Иванов",
        "middle_name": "Иванович",
        "age": 19,
        "alternate_url": "https://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
                    "result": "",
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
                "area": {
                    "id": "1",
                    "name": "Москва",
                    "url": "https://api.hh.ru/areas/1"
                },
                "company": "Рога и копыта",
                "company_id": null,
                "company_url": "http://example.com/",
                "employer": null,
                "end": "1999-03-01",
                "industries": [
                    {
                        "id": "45.507",
                        "name": "Добыча и обогащение руд черных, цветных, драгоценных, благородных, редких металлов"
                    }
                ],
                "industry": null,
                "start": "1998-01-01"
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
    },
    "vacancy": {
        "address": null,
        "alternate_url": "https://hh.ru/vacancy/123456",
        "archived": false,
        "area": {
            "id": "1",
            "name": "Москва",
            "url": "https://api.hh.ru/areas/1"
        },
        "created_at": "2015-05-14T11:00:00+0300",
        "employer": {
            "alternate_url": "https://hh.ru/employer/1",
            "id": "1",
            "logo_urls": {
                "240": "https://hh.ru/employer-logo/1111.jpeg",
                "90": "https://hh.ru/employer-logo/1111.jpeg",
                "original": "https://hh.ru/employer-logo-original/1111.jpeg"
            },
            "name": "Рога и копыта",
            "url": "https://api.hh.ru/employers/1",
            "vacancies_url": "https://api.hh.ru/vacancies?employer_id=1"
        },
        "id": "123456",
        "name": "Менеджер",
        "premium": false,
        "published_at": "2015-05-14T10:00:00+0300",
        "response_letter_required": false,
        "salary": null,
        "type": {
            "id": "closed",
            "name": "Закрытая"
        },
        "url": "https://api.hh.ru/vacancies/123456?host=hh.ru"
    },
    "counters": {
        "messages": 100,
        "unread_messages": 50
    },
  "source": "NEGOTIATION",
    "test_result": {
        "url": "https://api.hh.ru/negotiations/1359970704/test/solution",
        "alternate_url": "https://hh.ru/employer/vacancy_response/test?topicId=1359970704",
        "score": 100,
        "mark": "EXCELLENT"
    }
}
```

Тело ответа аналогично
[элементу в списке откликов/приглашений](#negotiations-list-item), а также
содержит ключ `vacancy` в котором выдаётся
[краткая информация о вакансии](vacancies.md#nano).

<a name="messaging_status"></a>
Дополнительно по отклику/приглашению возвращается поле `messaging_status`,
которое указывает на состояние переписки. Возможные значения
содержатся в [справочнике messaging_status](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

### Ошибки

* `404 Not Found` - отклик/приглашение не существует или недоступен текущему пользователю

<a name="get-messages"></a>
> ‼️ Обратите внимание, что методы для работы с сообщениями в рамках отклика/приглашения от имени [соискателя](docs/negotiations.md#get_messages) и
> [менеджера работодателя](docs/employer_negotiations.md#get-messages) устарели, и новые возможности [чатов](https://feedback.hh.ru/knowledge-base/article/1290) в них не будут поддерживаться.
> В связи с этим переписка может некорректно отображаться.

## Просмотр списка сообщений в отклике/приглашении

Сообщения в отклике/приглашении могут быть:

* сопроводительным письмом, оставленным соискателем при отклике на вакансию
* текстом, отправленным работодателем при приглашении на вакансию, приглашении
  на интервью или отказе
* сообщениями свободной переписки между соискателем и работодателем

Для того, чтобы посмотреть список сообщений в отклике необходимо сделать запрос по урлу (поле `messages_url`), пришедшему в 
[списке откликов/приглашений](#negotiations-list) или в [просмотре отклика/приглашения](#get-negotiation).
Например: 

`GET /negotiations/123456789/messages`

Параметры:

Имя | Обязательный | Принимаемые значения | Описание
--- | ------------ | -------------------- | --------
with_text_only | нет | true/false | Вернуть только те сообщения, которые содержат текст в поле `text`, по умолчанию: `false`, т.е. будут возвращены все сообщения

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
   "found": 2,
   "pages": 1,
   "page": 0,
   "per_page": 20,
   "items": [
       {
           "id": "123",
           "text": "Приглашаем вас на нашу вакансию ...",
           "created_at": "2015-05-15T19:23:35+0300",
           "author": {
               "participant_type": "employer"
           },
           "viewed_by_opponent": true,
           "viewed_by_me": true,
           "state": {
               "id": "invitation",
               "name": "Приглашение"
           },
           "address": {
                "building": "10",
                "city": "Москва",
                "description": "Направо под знак",
                "lat": 35.0,
                "lng": 30.0,
                "metro": {
                    "lat": 55.789704,
                    "line_id": "2",
                    "line_name": "Замоскворецкая",
                    "lng": 37.558212,
                    "station_id": "2.34",
                    "station_name": "Динамо"
                },
                "metro_stations": [
                    {
                        "lat": 55.789704,
                        "line_id": "2",
                        "line_name": "Замоскворецкая",
                        "lng": 37.558212,
                        "station_id": "2.34",
                        "station_name": "Динамо"
                    }
                ],
                "street": "ул. Динамо"
            },
            "assessments": [
                {
                    "id": "123",
                    "name": "Динамический тест числовых способностей",
                    "actions": [
                        {
                            "id": "proceed",
                            "name": "Перейти к тестированию",
                            "enabled": true,
                            "alternate_url": "https://hh.ru/applicant/assessment/123"
                        }
                    ]
                }
            ]
       },
       {
           "id": "321",
           "text": "Отлично, с удовольствием пройду интервью ...",
           "created_at": "2015-05-15T19:23:35+0300",
           "author": {
               "participant_type": "applicant"
           },
           "viewed_by_me": false,
           "viewed_by_opponent": true,
           "state": {
               "id": "text",
               "name": "Текст"
           },
           "address": null
       }
   ]
}
```

где:

Имя | Тип | Описание
--- | --- | --------
found | число | Количество сообщений в переписке ( ≥ 0 )
pages | число | Количество страниц с сообщениями ( ≥ 1 )
per_page | число | Количество сообщений на страницу ( > 0 )
page | число | Номер текущей страницы ( ≥ 0 )

Сообщения отсортированы в следующем порядке: самое старое - первое, самое новое - последнее.

<a name="negotiations-message-item"></a>
В элементе `items` содержатся данные о сообщениях:

Имя | Тип | Описание
--- | --- | --------
id | строка | Идентификатор сообщения
viewed_by_me | логический | Прочитано ли сообщение смотрящим (для сообщений отправленных работодателем всегда `true`)
viewed_by_opponent | логический | Прочитано ли сообщение соискателем (для сообщений соискателя всегда `true`)
created_at | строка | Дата и время создания сообщения
text | строка, null | Текст сообщения. `null` может быть в случае, когда соискатель не оставил сопроводительное письмо к отклику.
state | объект | Текущее состояние отклика. Возможные значения находятся в справочнике [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) в разделе `negotiations_state`
author | объект | Кто автор сообщения
author.participant_type | строка | Роль автора сообщения. Возможные значения находятся в справочнике [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) в разделе `negotiations_participant_type`
address | объект, null | [Адрес](./address.md), привязанный к отклику/приглашению
assessments | массив | [инструменты оценки](assessment.md), привязанные к сообщению

В случае, когда отклик/приглашение не существует или переписка недоступна
текущему пользователю возвращается ответ `404 Not Found`.


<a name="add-messages"></a>
## Отправка сообщения в отклике/приглашении

Обмен сообщениями возможен после приглашения соискателя. О возможности написать
сообщение можно узнать из
[поля `messages_status` в отклике/приглашении](#messaging_status).

### Запрос

`POST /negotiations/{nid}/messages`

где `nid` – идентификатор отклика/приглашения.

Дополнительно необходимо передать параметр `message` - текст сообщения.

### Ответ

Успешный ответ приходит с кодом `201 Created` и не содержит тело.

### Ошибки

* `400 Bad Request` – ошибка в параметрах запроса.
* `403 Forbidden` – отправка сообщения невозможна.
* `404 Not Found` – переданный отклик/приглашение не существует, либо у
  текущего менеджера нет прав для работы с ним.

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#negotiations).

Например:

* `resume_not_found` – если резюме в отклике/приглашении было скрыто
  либо удалено
* `invalid_vacancy` – если вакансия в отклике/приглашении была архивирована
  либо скрыта
* `no_invitation` – если отклик/приглашение не в статусе «приглашение».
  Например, уже в статусе «отказано» или ещё в статусе «отклик».
* `in_a_row_limit` – если превышено количество последовательных сообщений.
  Соискатель должен ответить на сообщение, чтобы появилась возможность писать
  вновь.
* `overall_limit` – если превышен лимит сообщений


<a name="add-invite"></a>
## Приглашение соискателя на вакансию

Приглашение устанавливается между вакансией работодателя и резюме соискателя по
инициативе работодателя. Чтобы выполнить запрос, нужно узнать начальное
состояние для данной пары вакансии и резюме. Подробнее в
[общем описании процесса работы](#flow).

Для создания приглашения необходимо запросить вакансии работодателя, применимые к выбранному резюме.
Получить эту информацию можно в [списке вакансий работодателя](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-active-vacancy-list)

Для того, чтобы пригласить соискателя нужно выполнить запрос, пришедший в поле `negotiations_actions[].url`, передав аргументы, содержащиеся в поле `arguments`, например:

### Запрос

`POST /negotiations/phone_interview?resume_id=123456&vacancy_id=654321&message=new_msg`

Параметры необходимо отправлять в стандартном формате `application/x-www-form-urlencoded`.


### Ответ

Успешный ответ приходит с кодом `201 Created`, не содержит тело и содержит
заголовок `Location`, указывающий на созданное приглашение:

```
HTTP/1.1 201 Created

Location: /negotiations/321
```


### Ошибки

* `400 Bad Request` – ошибка в параметрах запроса.
* `403 Forbidden` – приглашение невозможно.

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#negotiations).

Например:

* `already_invited` - если отклик между переданными резюме и вакансией уже существует
* `resume_not_found` – если переданное резюме было скрыто либо удалено
* `invalid_vacancy` - если переданная вакансия была архивирована либо скрыта
* `limit_exceeded` - если превышен лимит менеджера на количество приглашений в сутки
* `application_denied` - общая ошибка запрета приглашения в случае, когда
  дополнительная информация недоступна
* `address_not_found` – если переданный адрес не существует, либо принадлежит
  другому работодателю
* `not_enough_purchased_services` - не хватает оплаченных услуг, обычно
  [доступа к базе резюме](https://hh.ru/price#dbaccess)


<a name="actions"></a>
<a name="put-on-hold"></a>
<a name="invite"></a>
<a name="discard"></a>
## Действия по отклику/приглашению 

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-pref-negotiations-order)


<a name="get-preference-order"></a>
## Просмотр предпочитаемой сортировки откликов

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-pref-negotiations-order)

<a name="update-preference-order"></a>
## Изменение предпочитаемой сортировки откликов

### Запрос

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-pref-negotiations-order)

