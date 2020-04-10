# Подходящие для приглашения вакансии

Запрос используется для выбора подходящей вакансии при
[приглашении соискателя](employer_negotiations.md#add-invite).


### Запрос

`GET /employers/{employer_id}/vacancies/active?resume_id={resume_id}`

где

* `employer_id` - идентификатор работодателя, который можно узнать в
  [запросе информации о текущем пользователе](me.md#info),
* `resume_id` – идентификатор резюме.

Дополнительно поддерживаются [параметры пагинации](general.md#pagination)
`page`, `per_page`.


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "per_page": 20,
    "items": [
        {
            "negotiations_state": null,
            "negotiations_employer_state": null,
            "can_invite": true,
            "negotiations_actions": [
                {
                    "id": "invitation",
                    "name": "Пригласить",
                    "enabled": true,
                    "method": "POST",
                    "url": "https://api.hh.ru/negotiations/invited",
                    "resulting_employer_state": {
                        "id": "invitation",
                        "name": "Приглашение"
                    },
                    "templates": [
                        {
                            "id": "invite",
                            "name": "Приглашение на вакансию",
                            "quick": false,
                            "url": "https://api.hh.ru/message_templates/invite?resume_id=0123456789abcdef&vacancy_id=123456"
                        }
                    ],
                    "arguments": [
                        {
                            "id": "resume_id",
                            "required": true,
                            "required_arguments": []
                        },
                        {
                            "id": "vacancy_id",
                            "required": true,
                            "required_arguments": []
                        },
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
                }
            ],

            "id": "123456",
            "premium": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/123456",
            "salary": {
                "to": null,
                "from": 100000,
                "currency": "RUR"
            },
            "name": "Специалист по автоматизации тестирования (Java, Selenium)",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Москва"
            },
            "url": "https://api.hh.ru/vacancies/123456",
            "published_at": "2013-10-11T13:27:16+0400",
            "relations": [ ],
            "employer": {
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/1455.png",
                    "240": "https://hh.ru/employer-logo/1455.png",
                    "original": "https://hh.ru/file/1455.png"
                },
                "name": "HeadHunter",
                "id": "1455"
            },
            "response_letter_required": false,
            "type": {
                "id": "open",
                "name": "Открытая"
            }
        }
    ],
    "page": 0,
    "pages": 1,
    "found": 1
}
```

Возвращается список, аналогичный
[опубликованным вакансиям текущего менеджера](employer_vacancies.md#active)
со [стандартными полями](vacancies.md#nano), а также дополнительные поля:

* `negotiations_state` – состояние отклика/приглашения для этой вакансии
  с указанным резюме, либо `null` если отклика/приглашения не было
* `employer_negotiations_state` – работодательское состояние
  отклика/приглашения для этой вакансии с указанным резюме, либо `null` если
  отклика/приглашения не было
* `can_invite` – флаг, говорящий о возможности или невозможности пригласить
  указанное резюме на эту вакансию
* <a name="actions"></a> `negotiations_actions` – действия, для
  [создания отклика](employer_negotiations.md#add-invite).
  Если создать отклик невозможно (например, нет нужных услуг), то вернется пустой массив. 
  Формат выдачи действий аналогичен [действиям по отклику/приглашению](employer_negotiations.md#actions-info).
  Дополнительно будут указаны аргументы `vacancy_id` и `resume_id`.
  Также в отличие от действий по отклику/приглашению используется `POST`
  HTTP метод.

При принятии решении, дать ли пользователю возможность пригласить на вакансию по
выбранному резюме, нельзя полагаться на то, что
`negotiations_state` или `employer_negotiations_state` имеет значение `null`,
нужно использовать флаг `can_invite`.

Наличие у вакансии флага `can_invite` = `true` не означает, что приглашение
пройдет успешно. Например, в момент между получением списка подходящих вакансий
и приглашением, соискатель может удалить свое резюме.

В случае, если у вакансии с указанным резюме уже есть отклик/приглашение, его
состояние будет указано в виде:

```json
{
    "negotiations_state": {
        "id": "response",
        "name": "Отклик"
    },
    "negotiations_employer_state": {
        "id": "response",
        "name": "Отклик"
    }
}
```

Возможные значения состояния отклика/приглашения для соискателя доступны в
[справочнике negotiations_state](dictionaries.md), а для работодателя – в
[списке работодательских состояний по вакансии](employer_negotiations.md#states)
(могут различаться в разных вакансиях).


### Ошибки

При запросе без авторизации или с авторизацией соискателя вернется
`403 Forbidden`.

Если указанный работодатель не существует или отсутствует доступ к его вакансиям
вернётся ошибка `404 Not Found`.
