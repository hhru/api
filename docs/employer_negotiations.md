# Переписка (отклики/приглашения) для работодателя


_Документация по переписке для соискателя доступна в [отдельной статье](negotiations.md)._

* [Коллекции откликов/приглашений](#collections)
* [Список откликов/приглашений](#negotiations-list)
* [Просмотр отклика/приглашения](#get-negotiation)
* [Просмотр списка сообщений в отклике/приглашении](#get-messages)


<a name="collections" />
## Коллекции откликов/приглашений

У работодателя доступны коллекции откликов и приглашений. Каждая коллекция
содержит отклики/приглашения в определённом состоянии. Список этих коллекций
может меняться в зависимости от конкретной вакансии.

Получить доступные у текущего пользователя вакансии можно через
[списки вакансий работодателя](employer_vacancies.md#active).

Если вам необходимо получить полный список откликов/приглашений по вакансии,
запросите последовательно все коллекции.

Наиболее часто встречающиеся коллекции:
* `inbox` - неразобранные
* `hold` - подумать
* `invited` - приглашенные
* `discarded` - отклоненные


### Запрос на получение списка коллекций

`GET /negotiations?vacancy_id={vacancy_id}`

где `vacancy_id` - id вакансии.


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "states": [
        {
            "id": "inbox",
            "name": "Неразобранные",
            "url": "https://api.hh.ru/negotiations/inbox?vacancy_id=123456"
        },
        {
            "id": "invited",
            "name": "Приглашенные",
            "url": "https://api.hh.ru/negotiations/invited?vacancy_id=123456"
        }
    ]
}

```

Имя | Тип | Описание
--- | --- | --------
id | строка | Идентификатор коллекции, уникальный как минимум для данной вакансии
name | строка | название коллекции
url | строка | url на который необходимо делать GET запрос для получения откликов/приглашений данной коллекции

Если параметр `vacancy_id` не передан вернётся ответ с кодом `400 Bad Request`.


<a name="negotiations-list" />
## Список откликов/приглашений


### Запрос

Получив url из [списка коллекций](#collections) нужно сделать GET запрос на
него, например:

`GET https://api.hh.ru/negotiations/invited?vacancy_id=123456`

Параметры:

Имя | Обязательный | Описание
--- | ------------ | --------
vacancy_id | да | Идентификатор вакансии
page | нет | Номер страницы, по умолчанию: 0
per_page | нет | Количество выдаваемых элементов на страницу, по умолчанию 20

Коллекция `inbox`, если она доступна для данной вакансии, поддерживает
дополнительный параметр `with_updates_only=true` – показывать только
отклики/приглашения, имеющие обновления.

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
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
                "id": "invitation",
                "name": "Приглашение"
            },
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
                "alternate_url": "http://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
                    "name": "Мужской"
                },
                "salary": {
                    "amount": 1000000,
                    "currency": "RUR"
                },
                "photo": {
                    "medium": "http://hh.ru/...",
                    "small": "http://hh.ru/...",
                    "id": "1337"
                }
            }
        }
    ]
}
```

где:

Имя | Тип | Описание
--- | --- | --------
found | число | Количество найденных откликов ( ≥ 0 )
pages | число | Количество страниц с откликами ( ≥ 1 )
per_page | число | Количество элементов на страницу ( > 0 )
page | число | Номер текущей страницы ( ≥ 0 )

<a name="negotiations-list-item" />
В элементе `items` содержатся данные о откликах/приглашениях и резюме к ним:

Имя | Тип | Описание
--- | --- | --------
id | строка | Идентификатор отклика
created_at | строка | Дата и время создания отклика/приглашения
updated_at | строка | Дата и время последнего обновления отклика/приглашения
state | объект | Текущее состояние отклика. Возможные значения находятся в справочнике [/dictionaries] (./dictionaries.md) в разделе ```negotiations_state```.
url | строка | url для получения [полной версии отклика/приглашения](#get-negotiation)
messages_url | строка | url для получения [списка сообщений в отклике](#get-messages)
resume | объект, null | Резюме. Выдаваемые поля аналогичны [поиску резюме](resumes.md#search-results). Для получения полного резюме необходимо запросить его GET запросом по url из ключа `url`. Может быть `null`, если соискатель удалил резюме или закрыл к нему доступ.
has_updates | логический | Есть ли в отклике/приглашении обновления, требующие внимания
viewed_by_opponent | логический | Был ли отклик просмотрен соискателем

**Важно!** Дополнительный запрос на получение данных о резюме **необходимо**
выполнять именно по url из JSON ответа, только в таком случае просмотр резюме
будет правильно учтён в истории просмотров резюме соискателя. Например,
при просмотре резюме из отклика на анонимную вакансию в истории будет отражено
анонимное название компании.

В случае, когда вакансия, по которой запрашиваются отклики, не существует или
не доступна текущему пользователю возвращается ответ `404 Not Found`.

<a name="get-negotiation" />
## Просмотр отклика/приглашения

### Запрос

`GET /negotiations/{nid}`

где `nid` – идентификатор отклика/приглашения.

Обычно получается из ключа `url` в
[списке откликов/приглашений](#negotiations-list).

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "id": "123456789",
    "created_at": "2015-05-14T00:00:00+0300",
    "updated_at": "2015-05-14T12:00:05+0300",
    "has_updates": true,
    "messages_url": "https://api.hh.ru/negotiations/123456789/messages",
    "state": {
        "id": "invitation",
        "name": "Приглашение"
    },
    "viewed_by_opponent": false,
    "resume": {
        "id": "0123456789abcdef",
        "title": "Начинающий специалист",
        "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
        "first_name": "Иван",
        "last_name": "Иванов",
        "middle_name": "Иванович",
        "age": 19,
        "alternate_url": "http://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
        }
    },
    "vacancy": {
        "address": null,
        "alternate_url": "http://hh.ru/vacancy/123456",
        "archived": false,
        "area": {
            "id": "1",
            "name": "Москва",
            "url": "https://api.hh.ru/areas/1"
        },
        "created_at": "2015-05-14T11:00:00+0300",
        "employer": {
            "alternate_url": "http://hh.ru/employer/1",
            "id": "1",
            "logo_urls": {
                "240": "http://hh.ru/employer-logo/1111.jpeg",
                "90": "http://hh.ru/employer-logo/1111.jpeg",
                "original": "http://hh.ru/employer-logo-original/1111.jpeg"
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
    }
}
```

Тело ответа аналогично
[элементу в списке откликов/приглашений](#negotiations-list-item), а также
содержит ключ `vacancy` в котором выдаётся
[краткая информация о вакансии](vacancies.md#nano).

В случае, когда отклик/приглашение не существует или не доступен текущему
пользователю возвращается ответ `404 Not Found`.


<a name="get-messages" />
## Просмотр списка сообщений в отклике/приглашении

Сообщения в отклике/приглашении могут быть:

* сопроводительным письмом оставленным соискателем при отклике на вакансию
* текстом отправленным работодателем при приглашении на вакансию
* сообщениями свободной переписки между соискателем и работодателем

### Запрос

`GET /negotiations/{nid}/messages`

где `nid` – идентификатор отклика/приглашения.

Обычно url получается из ключа `messages_url` в
[списке откликов/приглашений](#negotiations-list) или в
[просмотре отклика/приглашения](#get-negotiation).

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
                "raw": null,
                "street": "ул. Динамо"
            },
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

<a name="negotiations-message-item" />
В элементе `items` содержатся данные о сообщениях:

Имя | Тип | Описание
--- | --- | --------
id | строка | Идентификатор сообщения
viewed_by_me | логический | Прочитано ли сообщение смотрящим (для сообщений отправленных работодателем всегда `true`)
viewed_by_opponent | логический | Прочитано ли сообщение соискателем (для сообщений соискателя всегда `true`)
created_at | строка | Дата и время создания сообщения
text | строка, null | Текст сообщения. `null` может быть в случае, когда соискатель не оставил сопроводительное письмо к отклику.
state | объект | Текущее состояние отклика. Возможные значения находятся в справочнике [/dictionaries] (./dictionaries.md) в разделе `negotiations_state`
author | объект | Кто автор сообщения
author.participant_type | строка | Роль автора сообщения. Возможные значения находятся в справочнике [/dictionaries] (./dictionaries.md) в разделе `negotiations_participant_type`
address | объект, null | [Адрес] (./address.md), привязанный к отклику/приглашению

В случае, когда отклик/приглашение не существует или переписка недоступна
текущему пользователю возвращается ответ `404 Not Found`.
