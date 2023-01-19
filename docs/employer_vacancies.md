# Вакансии для работодателя

* [Варианты публикации вакансий](#available_types)
* [Публикация вакансий](#creation)
* [Условия заполнения полей при добавлении и редактировании вакансий](#conditions)
* [Редактирование вакансий](#edit)
* [Продление вакансий](#prolongate)
* [Информация о возможности продления вакансии](#prolongate-info)
* [Список опубликованных вакансий](#active)
* [Архивация вакансий](#archive)
* [Список архивных вакансий](#archived)
* [Удаление вакансий](#hide)
* [Список удаленных вакансий](#hidden)
* [Восстановление из удаленных](#restore)
* [Статистика по вакансии](#stats)
* [Просмотры вакансии](#visitors)

Смотрите также:

* [Дополнительные поля для автора вакансии при получении вакансии](vacancies.md#author)


<a name="available_types"></a>
## Варианты публикации вакансий у текущего менеджера

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/paths/~1employers~1%7Bemployer_id%7D~1managers~1%7Bmanager_id%7D~1vacancies~1available_types/get)

<a name="creation"></a>
## Публикация вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/paths/~1vacancies/post)

<a name="conditions"></a>
## Условия заполнения полей при добавлении и редактировании вакансий

`GET /vacancy_conditions`

Каждое конечное поле описано объектом правил. Если поле состоит из
объекта с несколькими полями, эти поля описаны в `fields`.

Для всех полей и их частей указано, являются ли они необходимыми (`required`).


### Ответ

Успешный ответ содержит код ответа `200 OK` и тело.

```json
{
    "accept_handicapped": {
        "required": false
    },
    "accept_kids": {
            "required": false
    },
    "address": {
        "fields": {
            "show_metro_only": {
                "required": false
            }
        },
        "required": false
    },
    "allow_messages": {
        "required": false
    },
    "area": {
        "required": true
    },
    "billing_type": {
        "required": true
    },
    "code": {
        "max_length": 50,
        "min_length": 0,
        "required": false
    },
    "contacts": {
        "fields": {
            "email": {
                "max_length": 255,
                "min_length": 0,
                "required": false
            },
            "name": {
                "max_length": 255,
                "min_length": 0,
                "required": true
            },
            "phones": {
                "fields": {
                    "city": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\d{0,6}$",
                        "required": true
                    },
                    "comment": {
                        "max_length": 255,
                        "min_length": 0,
                        "required": false
                    },
                    "country": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\+?\\d{0,5}$",
                        "required": true
                    },
                    "number": {
                        "max_length": 32,
                        "min_length": 4,
                        "regexp": "^[\\d -]{4,32}$",
                        "required": true
                    }, 
                    "formatted": {
                        "max_length": 43,
                        "min_length": 6,
                        "regexp": "^\\d{6,43}$",
                        "required": false
                  }
                },
                "max_count": 2,
                "min_count": 0,
                "required": true
            }
        },
        "required": false
    },
    "custom_employer_name": {
        "max_length": 150,
        "min_length": 0,
        "required": false
    },
    "department": {
        "max_length": 32,
        "min_length": 0,
        "required": false
    },
    "description": {
        "max_length": 10000,
        "min_length": 200,
        "required": true
    },
    "employment": {
        "required": false
    },
    "experience": {
        "required": false
    },
    "key_skills": {
        "max_count": 30,
        "min_count": 0,
        "required": false
    },
    "manager": {
        "required": false
    },
    "name": {
        "max_length": 220,
        "min_length": 0,
        "required": true
    },
    "response_letter_required": {
        "required": false
    },
    "response_notifications": {
        "required": false
    },
    "response_url": {
        "max_length": 511,
        "min_length": 0,
        "regexp": "^(http|https)://.+$",
        "required": false
    },
    "salary": {
        "fields": {
            "currency": {
                "required": false
            },
            "from": {
                "required": false
            },
            "to": {
                "required": false
            },
            "gross": {
                "required": false
            }
        },
        "required": false
    },
    "schedule": {
        "required": false
    },
    "test": {
        "fields": {
            "required": {
                "required": false
            }
        },
        "required": false
    },
    "type": {
        "required": true
    },
	"working_days": {
		"min_count": 0,
		"max_count": null,
		"required": false
	},
	"working_time_intervals": {
		"min_count": 0,
		"max_count": null,
		"required": false
	},
	"working_time_modes": {
		"min_count": 0,
		"max_count": null,
		"required": false
	},
	"accept_temporary": {
		"required": false
	}
}
```

### Правила

Имя | Тип | Описание
--- | --- | --------
required | логический | Является ли поле вакансии или поле объекта необходимым?
min_length | целое | Минимальная длина для текстовых полей.
max_length | целое | Максимальная длина для текстовых полей.
min_count | целое | Минимальное количество объектов для полей, где необходимо передавать список.
max_count | целое или `null` | Максимально количество объектов для полей, где необходимо передавать список. `null` – если количество не ограничено.

### Ошибки

`403 Forbidden` – условия заполнения полей вакансии недоступны данному пользователю.

<a name="edit"></a>
## Редактирование вакансий

`PUT /vacancies/{vacancy_id}`

* `ignore_duplicates=true` - игнорировать
  [появление дубликата](#edit-ignore-duplicates), после редактирования вакансии.

Редактирование происходит по аналогии с созданием вакансии, но есть возможность
передачи отдельных полей в объекте для частичного редактирования вакансии.
Cоставные поля (например, `salary`, `contacts`, `professional_roles`) можно
редактировать только целиком, передавая полный объект. Например, для изменения
валюты в зарплате, необходимо передавать также и значения зарплаты, а
для изменения специализации необходимо передать полный список.

### Поля, доступные для редактирования

Имя | Описание
-----|----------
name | название
description | описание
key_skills | ключевые навыки
schedule | график работы
experience | требуемый опыт работы
employment | тип занятости
professional_roles | список профессиональных ролей
salary | зарплата
address | адрес
test | тестовое задание
department | департамент
code | внутренний код вакансии
response_letter_required | необходимость сопроводительного письма при отклике
accept_handicapped | указание, что вакансия доступна для соискателей с инвалидностью
accept_kids | указание, что вакансия доступна для соискателей от 14 лет
response_notifications | настройка уведомления о новых откликах
allow_messages | возможность переписки с кандидатами по данной вакансии
contacts | контактная информация
custom_employer_name | название компании для анонимных вакансий
response_url | URL отклика для прямых вакансий
accept_incomplete_resumes | разрешен ли отклик на вакансию неполным резюме
working_days | рабочие дни
working_time_intervals | временные интервалы работы
working_time_modes | режимы времени работы
accept_temporary | указание, что вакансия доступна для соискателей с временным трудоустройством
branded_template.id | <a name="branded-template-field"></a> брендированное оформление вакансии из [справочника](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1vacancy_branded_templates/get)
languages | список языков

Остальные поля доступны только для чтения, либо их можно задать только при создании вакансии.

### Ответ

При успешном обновлении вакансии вернется `204 No Content`.

### Ошибки

* `404 Not Found` – редактируемая вакансия не найдена.
* `403 Forbidden` – редактирование вакансий недоступно данному пользователю.
* `400 Bad Request` – ошибки в полях при редактировании вакансии.
* <a name="edit-ignore-duplicates"></a> `403 Forbidden` –
  изменение вакансии невозможно, так как после изменения, вакансия становится
  похожа на другую вакансию у данного работодателя. Если вы уверены, что
  появление дубликата необходимо, вы можете добавить к запросу параметр
  `PUT /vacancies/{vacancy_id}?ignore_duplicates=true`.

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#vacancies-create-n-edit).

<a name="edit_more"></a>
### Смена биллинг-типа, менеджера вакансии

Возможно только улучшение типа вакансии.

Изменение биллингового типа вакансии, а также передача вакансии другому
менеджеру компании происходит по аналогии с редактированием
`PUT /vacancies/{vacancy_id}`. Единственная особенность — эти поля
(`billing_type` и `manager`) необходимо отправлять отдельно от остальных полей
вакансии.

```
PUT /vacancies/{vacancy_id}
```

```json
{
    "billing_type": {
        "id": "premium"
    }
}
```

и

```
PUT /vacancies/{vacancy_id}
```

```json
{
    "manager": {
        "id": "1337"
    }
}
```

### Ответ

При успешном обновлении биллинг-типа, менеджера вакансии вернется `204 No Content`.

### Ошибки

* `404 Not Found` – редактируемая вакансия не найдена.
* `403 Forbidden` – редактирование вакансий недоступно данному пользователю.
* `403 Forbidden` – поля `billing_type` и `manager` передаются вместе с другими.

Дополнительно к HTTP коду сервер может вернуть описание [причины ошибки](errors.md#vacancies-create-n-edit).


<a name="other-actions"></a>
### Прочие действия

* [архивация](#archive)
* [удаление](#hide)
* [восстановление из удаленных](#restore)


<a name="prolongate"></a>
## Продление вакансий
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/paths/~1vacancies~1%7Bvacancy_id%7D~1prolongate/post)

## Информация о возможности продления вакансии
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/paths/~1vacancies~1%7Bvacancy_id%7D~1prolongate/get)

<a name="active"></a>
## Список опубликованных вакансий

`GET /employers/{employer_id}/vacancies/active`

По умолчанию возвращаются вакансии текущего пользователя. Если требуется
получить вакансии другого менеджера, необходимо передать дополнительный параметр
`manager_id={manager_id}`. Можно передать только 1 `manager_id`, если передать несколько, будет использоваться последний.

Максимальное значение per_page, которое можно передать в данном запросе: 50.


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "salary": {
                "to": null,
                "from": 30000,
                "currency": "RUR",
                "gross": true
            },
            "name": "Секретарь",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Москва"
            },
            "url": "https://api.hh.ru/vacancies/8331228",
            "published_at": "2013-07-08T16:17:21+0400",
            "relations": [],
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/289027.png",
                    "240": "https://hh.ru/employer-logo/289169.png",
                    "original": "https://hh.ru/file/2352807.png"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455",
                "trusted": true
            },
            "response_letter_required": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/8331228",
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
            "department": {
                "id": "HH-1455-TECH",
                "name": "HeadHunter::Технический департамент"
            },
            "premium": false,
            "type": {
                "id": "open",
                "name": "Открытая"
            },
            "id": "8331228",
            "archived": false,
            "counters": {
                "views": 100500,
                "responses": 5,
                "unread_responses": 3,
                "resumes_in_progress": 5,
                "invitations": 10,
                "invitations_and_responses": 14,
                "calls": 99,
                "new_missed_calls": 11
            },
            "expires_at": "2013-07-08T16:17:21+0400",
            "has_updates": false,
            "billing_type": {
                "id": "standard",
                "name": "Стандарт"
            },
            "can_upgrade_billing_type": true,
            "manager": {
              "first_name": "Петр",
              "last_name": "Иванов",
              "id": "5032",
              "middle_name": null
            }
        }
    ]
}
```

Где помимо [стандартных полей вакансии](vacancies.md#nano) вернутся
дополнительные поля:

Имя | Тип | Описание
-----|-----|---------
counters.views | number | количество просмотров вакансии
counters.responses | number | количество откликов на вакансию
counters.unread_responses | number | количество непросмотренных откликов на вакансию
counters.resumes_in_progress | number | количество резюме в работе на вакансию
counters.invitations | number | количество приглашений на вакансию
counters.invitations_and_responses | number | количество откликнувшихся и приглашенных соискателей на вакансию
counters.calls | number | общее количество звонков по вакансии
counters.new_missed_calls | number | количество новых пропущенных звонков
expires_at | string | дата окончания публикации вакансии
has_updates | boolean | Есть ли в откликах/приглашениях по данной вакансии обновления, требующие внимания
billing_type | object | Биллинговый тип вакансии. Элемент справочника [vacancy_billing_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get).
billing_type.id | string | Идентификатор биллингового типа вакансии
billing_type.name | string | Название биллингового типа вакансии
can_upgrade_billing_type | boolean | Можно ли улучшить биллинговый тип вакансии

Также доступен
[список опубликованных вакансий, подходящих для приглашения соискателя](employer_vacancies_for_invitation.md).


### Поддерживаемые параметры

Помимо стандартных параметров для пагинации `per_page` и `page`, коллекция поддерживает:

* `text` — строка для поиска по названию вакансии
* `area` — id региона (см.
  [список регионов, в которых есть активные вакансии](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1vacancy_areas~1active/get))
* `resume_id` - выборка сужается для работы с конкретным резюме
* `order_by` — сортировка вакансий, возможные варианты доступны в справочнике
  `employer_active_vacancies_order`

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой
* `403 Forbidden` – текущий пользователь не является работодателем.
* `404 Not Found` – у текущего пользователя нет прав на просмотр опубликованных вакансий.
* `404 Not Found` – менеджер с переданным идентификатором не существует.

<a name="archive"></a>
## Архивация вакансий

Для переноса вакансии в архив необходимо отправить запрос PUT:

`PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}`

### Ответ

При успешной архивации вернётся `204 No Content`.

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем.
* `404 Not Found` – указан неверный идентификатор работодателя.
* `404 Not Found` – у текущего пользователя нет прав на архивацию вакансии.
* `404 Not Found` – вакансия с переданным идентификатором не существует.


<a name="archived"></a>
## Список архивных вакансий

`GET /employers/{employer_id}/vacancies/archived`

По умолчанию возвращаются вакансии текущего пользователя. Если требуется
получить вакансии другого менеджера, необходимо передать дополнительный параметр
`manager_id={manager_id}`. Можно передать только 1 `manager_id`, если передать несколько, будет использоваться последний.

Поддерживается пагинация (`per_page` и `page`) и сортировка (`order_by`).

Максимальное значение `per_page`, которое можно передать в данном запросе: 1000.

Возможные значения сортировки доступны в
[справочнике `employer_archived_vacancies_order`](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get).

В отличие от списка опубликованных вакансий, данная коллекция не поддерживает
поиск (параметры `text` и `area`).


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "salary": {
                "to": null,
                "from": 30000,
                "currency": "RUR",
                "gross": true
            },
            "name": "Секретарь",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Москва"
            },
            "url": "https://api.hh.ru/vacancies/8331228",
            "published_at": "2013-07-08T16:17:21+0400",
            "relations": [],
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/289027.png",
                    "240": "https://hh.ru/employer-logo/289169.png",
                    "original": "https://hh.ru/file/2352807.png"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455",
                "trusted": true
            },
            "response_letter_required": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/8331228",
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
            "department": {
                "id": "HH-1455-TECH",
                "name": "HeadHunter::Технический департамент"
            },
            "premium": false,
            "type": {
                "id": "open",
                "name": "Открытая"
            },
            "id": "8331228",
            "archived": true,
            "counters": {
                "responses": 3,
                "invitations_and_responses": 5
            },
            "archived_at": "2013-08-08T16:17:21+0400"
        }
    ]
}
```

Где помимо [стандартных полей вакансии](vacancies.md#nano) вернутся
дополнительные поля:

| Имя                                | Тип      | Описание                                      |
|------------------------------------|----------|-----------------------------------------------|
| counters.responses                 | числовой | количество откликов на вакансию               |
| counters.invitations_and_responses | числовой | количество откликов и приглашений на вакансию |
| archived_at                        | строка   | дата архивации вакансии                       |

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой.
* `403 Forbidden` – текущий пользователь не является работодателем.
* `403 Forbidden` – указан неверный идентификатор работодателя.
* `404 Not Found` – у текущего пользователя нет прав на просмотр архивных вакансиий.


<a name="hide"></a>
## Удаление вакансий

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

Удалить можно только вакансию из архива.

### Ответ

При успешной операции вернётся `204 No Content`.

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем.
* `403 Forbidden` – удалять вакансию не из архива запрещено.
* `404 Not Found` – указан неверный идентификатор работодателя.
* `404 Not Found` – у текущего пользователя нет прав на удаление вакансиии из архива.
* `404 Not Found` – вакансия с переданным идентификатором не существует.


<a name="hidden"></a>
## Список удаленных вакансий

`GET /employers/{employer_id}/vacancies/hidden`

По умолчанию возвращаются вакансии текущего пользователя. Если требуется
получить вакансии другого менеджера, необходимо передать дополнительный параметр
`manager_id={manager_id}`. Можно передать только 1 `manager_id`, если передать несколько, будет использоваться последний.

Поддерживается пагинация (`per_page` и `page`) и сортировка (`order_by`).

Максимальное значение `per_page`, которое можно передать в данном запросе: 1000.

Возможные значения сортировки доступны в справочнике
[справочнике `employer_hidden_vacancies_order`](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get).

В отличие от списка опубликованных вакансий, данная коллекция не поддерживает
поиск (параметры `text` и `area`).


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
        {
            "salary": {
                "to": null,
                "from": 30000,
                "currency": "RUR",
                "gross": true
            },
            "name": "Секретарь",
            "area": {
                "url": "https://api.hh.ru/areas/1",
                "id": "1",
                "name": "Москва"
            },
            "url": "https://api.hh.ru/vacancies/8331228",
            "published_at": "2013-07-08T16:17:21+0400",
            "relations": [],
            "employer": {
                "logo_urls": {
                    "90": "https://hh.ru/employer-logo/289027.png",
                    "240": "https://hh.ru/employer-logo/289169.png",
                    "original": "https://hh.ru/file/2352807.png"
                },
                "name": "HeadHunter",
                "url": "https://api.hh.ru/employers/1455",
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455",
                "trusted": true
            },
            "response_letter_required": true,
            "address": null,
            "alternate_url": "https://hh.ru/vacancy/8331228",
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
            "department": {
                "id": "HH-1455-TECH",
                "name": "HeadHunter::Технический департамент"
            },
            "premium": false,
            "type": {
                "id": "open",
                "name": "Открытая"
            },
            "id": "8331228",
            "archived": true
        }
    ]
}
```

Ответ состоит из [стандартных полей вакансии](vacancies.md#nano).

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой
* `403 Forbidden` – текущий пользователь не является работодателем.
* `403 Forbidden` – указан неверный идентификатор работодателя.
* `404 Not Found` – у текущего пользователя нет прав на просмотр удаленных вакансиий.


<a name="restore"></a>
## Восстановление из удаленных

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

Восстановить можно только удаленную из архива вакансию.
Вакансия вернется в архив.

### Ответ

При успешной операции вернётся `204 No Content`.

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем.
* `403 Forbidden` – восстанавливать не удаленную вакансию запрещено.
* `404 Not Found` – указан неверный идентификатор работодателя.
* `404 Not Found` – у текущего пользователя нет прав на восстановление вакансии из удаленных.
* `404 Not Found` – вакансия с переданным идентификатором не существует.


<a name="stats"></a>
## Статистика по вакансии

`GET /vacancies/{vacancy_id}/stats`

где `vacancy_id` - идентификатор вакансии.

### Ответ

Успешный ответ содержит код ответа `200 OK` и тело:
```json
{
    "items": [
        {
            "date": "2017-01-10",
            "responses": 1,
            "views": 36
        },
        {
            "date": "2017-01-11",
            "responses": 4,
            "views": 35
        },
        {
            "date": "2017-01-12",
            "responses": 1,
            "views": 32
        },
        {
            "date": "2017-01-13",
            "responses": null,
            "views": null
        },
        {
            "date": "2017-01-14",
            "responses": null,
            "views": null
        }
    ]
}
```
В элементе `items` содержатся данные:

Имя | Тип | Описание
--- | --- | ---
date | Строка | Дата в формате `YYYY-MM-DD`
responses | Число или null | Количество откликов, `null` если дата в будущем или данных на эту дату нет
views | Число или null | Количество просмотров, `null` если дата в будущем или данных на эту дату нет

Возвращается окно в 5 последних дней существования вакансии:

* если вакансия создана поздее начала окна, то первой датой будет дата создания вакансии;
* если вакансия находится в архиве или удалена, то последней датой будет дата архивации.

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем.
* `404 Not Found` – вакансия с переданным идентификатором не существует.

<a name="visitors"></a>
## Просмотры вакансии

`GET /vacancies/{vacancy_id}/visitors`

Возвращает список резюме соискателей, просмотревших вакансию за последнюю неделю. Список отсортирован по убыванию по
дате просмотра. Если у пользователя несколько резюме, то вернется резюме с наиболее поздней датой обновления.

Параметры:

Имя | Обязательный | Описание
--- | ------------ | --------
vacancy_id | да | Идентификатор вакансии
page | нет | Номер страницы, по умолчанию: 0
per_page | нет | Количество выдаваемых элементов на страницу, по умолчанию: 20, максимальное значение: 50


### Ответ

Успешный ответ содержит код ответа `200 OK` и тело:
```json
{
  "found": 12,
  "pages": 1,
  "page": 0,
  "per_page": 20,
  "hidden_on_page": 0,
  "items": [
    {
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
    }
  ]
}
```

где:

Имя | Тип | Описание
--- | --- | --------
found | число | Количество найденных резюме ( ≥ 0 )
pages | число | Количество страниц с резюме ( ≥ 1 )
per_page | число | Количество элементов на страницу ( > 0 )
page | число | Номер текущей страницы ( ≥ 0 )
hidden_on_page | число | Количество удалённых или скрытых соискателями резюме на странице ( ≥ 0 )

В элементе `items` содержится список [сокращенных представлений резюме](employer_resumes.md#resume-short).

Если соискатель удалил или скрыл резюме от работодателя, то в списке `items` эти резюме будут пропущены, но будут 
учитываться при пагинации (`per_page`) и в количестве найденный резюме (`found`), а поле 
`hidden_on_page` указывает на количество таких пропущенных резюме на странице.

Например

```json
{
  "found": 12,
  "pages": 2,
  "page": 0,
  "per_page": 10,
  "hidden_on_page": 5,
  "items": [
    // ...
  ]
}
```
Такой ответ говорит о том что всего найдено 12 резюме, запрашивается первая страница с `per_page=10`. 
`hidden_on_page=5` в ответе указывает на то, что в списке `items` всего 5 элементов и 5 резюме пропущено.

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой
* `404 Not Found` - вакансия, по которой запрашиваются посетители,
  не существует или недоступна текущему пользователю

