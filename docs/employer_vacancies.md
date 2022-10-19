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

Смотрите также:

* [Дополнительные поля для автора вакансии при получении вакансии](vacancies.md#author)


<a name="available_types"></a>
## Варианты публикации вакансий у текущего менеджера

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/paths/~1employers~1%7Bemployer_id%7D~1managers~1%7Bmanager_id%7D~1vacancies~1available_types/get)

### Ошибки

* `404 Not Found` - текущий пользователь - не работодатель, текущий пользователь пытается запросить данные для другого менеджера или у менеджера нет доступа к публикации вакансий
* `404 Not Found` - менеджер или компания не существуют или не доступны для текущего пользователя


<a name="creation"></a>
## Публикация вакансий

`POST /vacancies`

дополнительно можно указать query-параметры:

* `ignore_duplicates=true` - форсировать
  [добавление дубликата](#creation-ignore-duplicates).

* `with_professional_roles=true` - для публикации вакансии с профессиональными ролями вместо специализаций

<a name="creation-with_professional_roles"></a>
При указании параметра `with_professional_roles=true` поле `specializations` перестает быть обязательным и игнорируется, а массив `professional_roles` становится обязательным, при этом количество его элементов равно 1.
Без этого параметра массив `professional_roles` необязателен и игнорируется
### Общая информация

В качестве тела запроса необходимо передавать
[JSON](general.md#request-body) с данными размещаемой вакансии,
формат данных аналогичен [просмотру вакансии](vacancies.md#item), но также содержит
некоторые дополнительные поля.

> В соответствии с
[законом РФ № 1032-1 от 19.04.1991 в ред. от 02.07.2013 г.](https://hh.ru/article/13967)
запрещено размещать информацию, ограничивающую права или устанавливающую
преимущества для соискателей по полу, возрасту, семейному положению и другим
обстоятельствам, не связанным с деловыми качествами работников.

* при успешной публикации будут списаны соответствующие услуги.
* все вакансии проходят ручную модерацию.
* в течение нескольких минут после публикации вакансия станет доступна в поиске.


### Полезные ссылки

* [правила размещения вакансий](https://hh.ru/article/341)
* [как составить хорошее описание вакансии](https://hh.ru/article/16239)


<a name="creation-example"></a>
### Пример тела запроса

```json
{
    "description": "<p>— Eh bien, mon prince. Gênes et Lucques ne sont plus que des apanages, des поместья, de la famille Buonaparte. Non, je vous préviens que si vous ne me dites pas que nous avons la guerre, si vous vous permettez encore de pallier toutes les infamies, toutes les atrocités de cet Antichrist (ma parole, j'y crois) — je ne vous connais plus, vous n'êtes plus mon ami, vous n'êtes plus мой верный раб, comme vous dites. Ну, здравствуйте, здравствуйте.</p><p><em>Je vois que je vous fais peur</em>, садитесь и рассказывайте.</p>",
    "key_skills": [
        {
            "name": "Холодные продажи"
        },
        {
            "name": "Проведение промо акций"
        }
    ],
    "schedule": {
        "id": "flyInFlyOut"
    },
    "experience": {
        "id": "moreThan6"
    },
    "employment": {
        "id": "full"
    },
    "name": "Менеджер по продажам",
    "area": {
        "id": "1"
    },
    "type": {
        "id": "open"
    },
    "specializations": [
        {
            "id": "17.324"
        },
        {
            "id": "3.148"
        }
    ],
    "professional_roles": [
        {
          "id": "59"
        }
    ],
    "response_letter_required": true,
    "salary": {
        "from": 100,
        "to": 500,
        "currency": "USD",
        "gross": true
    },
    "contacts": {
        "name": "Иванов Иван",
        "email": "i.ivanov@example.com",
        "phones": [
            {
                "country": "7",
                "city": "495",
                "number": "1234567",
                "comment": "с 10 до 20",
                "formatted": "79198883344"
            }
        ]
    },
    "accept_handicapped": true,
    "accept_kids": false,
    "code": "код-1234",
    "response_notifications": true,
    "allow_messages": true,
    "billing_type": {
        "id": "standard"
    },
    "address": {
        "id": "123",
        "show_metro_only": true
    },
    "manager": {
        "id": "321"
    },
    "test": {
        "id": "42",
        "required": true
    },
    "branded_template": {
        "id": "marketing"
    },
    "driver_license_types": [
        {
            "id": "A"
        },
        {
            "id": "B"
        }
    ],
    "accept_incomplete_resumes": false,
    "working_days": [
        {
            "id": "only_saturday_and_sunday"
        }
    ],
    "working_time_intervals": [
        {
            "id": "from_four_to_six_hours_in_a_day"
        }
    ],
    "working_time_modes": [
        {
            "id": "start_after_sixteen"
        }
    ],
    "accept_temporary": true
}
```


<a name="creation_fields"></a>
### Поля запроса

* `[]` (например, в полях специализации и контактах) обозначает, что значение данного ключа является массивом объектов.
* `a.b` обозначает объект `a` с ключом `b` описанного типа.

Путь | JSON тип | Описание
---- | -------- | --------
name | string | название
description | string | описание в html, не менее 200 символов
key_skills | array | список ключевых навыков, не более 30
key_skills[].name | string | название ключевого навыка
specializations | array | список специализаций
specializations[].id | string | специализация [из справочника](specializations.md)
professional_roles | array | массив профессиональных ролей с количеством элементов равным 1 (если передать больше возникнет [ошибка](errors.md#причины-возникновения-ошибок) `is_too_long`) [при использовании параметра](#creation-with_professional_roles) `with_professional_roles=true`
professional_roles[].id | string | индификатор профессиональной роли [из справочника](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1professional_roles/get)
area.id | string | город публикации [из справочника](areas.md)
type.id | string | тип из [справочника vacancy_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
billing_type.id | string | биллинговый тип [из справочника vacancy_billing_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
code | string или null | внутренний код вакансии
department.id | string | департамент [из справочника](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1departments/get), от имени которого размещается вакансия (если данная возможность доступна для компании)
salary | object или null | зарплата
salary.from | numeric или null | нижняя граница зарплаты
salary.to | numeric или null | верхняя граница зарплаты
salary.gross | boolean | признак что границы зарплаты указаны до вычета налогов
salary.currency | string | код валюты из [справочника currency](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
address | object или null | адрес
address.id | string | адрес из [списка доступных адресов работодателя](https://api.hh.ru/openapi/redoc#tag/Adresa-rabotodatelya)
address.show_metro_only | boolean | показывать только метро для указанного адреса
experience.id | string или null | требуемый опыт работы из [справочника experience](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
schedule.id | string или null | график работы из [справочника schedule](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
employment.id | string | тип занятости из [справочника employment](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
contacts | object или null | контактная информация
contacts.name | string | контактное лицо
contacts.email | string | email
contacts.phones | array | список телефонов для связи
contacts.phones[].country | string | код страны
contacts.phones[].city | string | код города
contacts.phones[].number | string | телефон
contacts.phones[].comment | string или null | комментарий (удобное время для звонка по этому номеру)
test | object или null | [тест](https://api.hh.ru/openapi/redoc#tag/Spravochniki-rabotodatelya/paths/~1employers~1%7Bemployer_id%7D~1tests/get) для вакансии
test.id | string | тест, который будет добавлен в вакансию
test.required | boolean | требовать прохождение теста для отклика на вакансию
response_url | string | URL отклика для прямых вакансий (`type.id=direct`)
custom_employer_name | string | название компании для анонимных вакансий (`type.id=anonymous`), например "крупный российский банк"
manager.id | string или null | контактное лицо (менеджер) по размещаемой вакансии, по умолчанию текущий пользователь
response_notifications | boolean или null | уведомлять о новых откликах
<a name="allow_messages"></a> allow_messages | boolean или null | возможность [переписки с кандидатами](employer_negotiations.md) по данной вакансии
response_letter_required | boolean или null | требовать сопроводительное письмо
accept_handicapped | boolean или null | указание, что вакансия доступна для соискателей с инвалидностью
accept_kids | boolean или null | указание, что вакансия доступна для соискателей от 14 лет [подробнее](employer_vacancies_accept_kids.md#accept-kids)
branded_template.id | string или null | <a name="branded-template-field"></a> брендированное оформление вакансии из [справочника](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1vacancy_branded_templates/get)
driver_license_types | array или null | список требуемых категорий водительских прав
driver_license_types[].id | string | категория водительских прав. элемент справочника [driver_license_types](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
accept_incomplete_resumes | boolean или null | разрешен ли отклик на вакансию неполным резюме
working_days | array или null | список рабочих дней
working_days[].id | string | рабочие дни из [справочника working_days](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
working_time_intervals | array или null | список с временными интервалами работы
working_time_intervals[].id | string | временной интервал работы из [справочника working_time_intervals](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
working_time_modes | array или null | список режимов времени работы
working_time_modes[].id | string | режимы времени работы из [справочника working_time_modes](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get)
accept_temporary | boolean или null | указание, что вакансия доступна с временным трудоустройством

<a name="creation-results"></a>
### Ответ

При успешном выполнении запроса вернется `201 Created`. В заголовке `Location` будет
  содержаться ссылка на добавленную вакансию:

```
HTTP/1.1 201 Created

Location: /vacancies/78789890
```

В теле ответа возвращается идентификатор добавленной вакансии:

```json
{
    "id": "78789890"
}
```

### Ошибки

* `403 Forbidden` – добавление вакансий недоступно данному пользователю.
* <a name="creation-ignore-duplicates"></a> `403 Forbidden` –
  добавление вакансии недоступно, так как вакансия с похожими
  данными уже опубликована у данного работодателя. Если вы уверены, что
  добавление дубликата необходимо, вы можете добавить к запросу параметр
  `POST /vacancies?ignore_duplicates=true`.
* `400 Bad Request` – ошибки в полях при добавлении вакансии. Дополнительно придет
  [расширенная информация](#vacancy-validation) по ошибкам.

Дополнительно к HTTP коду сервер может вернуть описание [причины ошибки](errors.md#vacancies-create-n-edit).

<a name="vacancy-validation"></a>
### Ошибки в использовании полей при создании и редактировании вакансии

При создании и редактировании вакансии значения в полях проходят проверки (валидация) - формат использования полей и
значений (см. [Параметры](#creation_fields)), существование данных, бизнес правила.

При ошибках в ответ придет `400 Bad Request` с телом:
```json
{ 
  "errors": [
  { 
    "value": "name",
    "reason": "required", 
    "pointer": "/name", 
    "description": "Значение обязательное", 
    "type": "bad_json_data"
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

С возможными причинами ошибок можно ознакомиться на [странице](errors.md#vacancies-create-n-edit).

<a name="error-pointer"></a>
`pointer` для указания использует формат JsonPointer [RFC 6901](https://tools.ietf.org/html/rfc6901).
Например, `/contacts/phones/1/number` значит, что ошибка в поле из сообщения (`number` - должен быть строкой):
```json
{
  
...
  
  "contacts": {
    "phones": [
      {
        "country": "7",
        "city": "912",
        "number": "3456789",
        "comment": ""
      },
      {
        "country": "7",
        "city": "912",
        "number": 3456789,
        "comment": "number задан числом - ошибка"
      }
    ]
  }
  
...
        
}
```




<a name="conditions"></a>
## Условия заполнения полей при добавлении и редактировании вакансий

`GET /vacancy_conditions`

дополнительно можно указать query-параметр:

* `with_professional_roles=true` - для получение условий для вакансии с профессиональными ролями вместо специализаций

При указании параметра `with_professional_roles=true` поле `specializations` не возвращается в ответе, а поле [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1professional_roles/get) появляется вместе с другими полями

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
    "specializations": {
        "max_count": null,
        "min_count": 1,
        "required": true
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
* `with_professional_roles=true` - для редактирования вакансии с профессиональными ролями вместо специализаций. Поведение
  аналогично поведению параметра `with_professional_roles` [при публикации вакансии](#creation-with_professional_roles)

Редактирование происходит по аналогии с созданием вакансии, но есть возможность
передачи отдельных полей в объекте для частичного редактирования вакансии.
Cоставные поля (например, `salary`, `contacts`, `specializations`, `professional_roles`) можно
редактировать только целиком, передавая полный объект. Например, для изменения
валюты в зарплате, необходимо передавать также и значения зарплаты, а
для изменения специализации необходимо передать полный список.

### Поля доступные для редактирования

Имя | Описание
-----|----------
name | название
description | описание
key_skills | ключевые навыки
schedule | график работы
experience | требуемый опыт работы
employment | тип занятости
specializations | список специализаций
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

**Продление вакансии по стоимости приравнивается к новой публикации**

Существуют ограничения по продлению вакансии, они могут меняться, на данный
момент работают следующие правила:

* стандартные вакансии можно продлевать, если с предыдущего продления прошло не менее 1 минуты.
* вакансии "стандарт-плюс" возможно продлевать не ранее 7 дней до окончания публикации.


### Запрос

`POST /vacancies/{vacancy_id}/prolongate`

где `vacancy_id` - идентификатор вакансии.

### Ответ

При успешном продлениии вакансии вернется `204 No Content`.

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем или
  продление невозможно.
* `404 Not Found` – текущему пользователю недоступно продление вакансии.
* `404 Not Found` – вакансия с переданным идентификатором не существует.

Дополнительно к HTTP коду сервер может вернуть
описание [причины ошибки](errors.md#vacancies-prolongate).


<a name="prolongate-info"></a>
## Информация о возможности продления вакансии


### Запрос

`GET /vacancies/{vacancy_id}/prolongate`

где `vacancy_id` - идентификатор вакансии.


### Ответ

Успешный ответ приходит с кодом `200 OK`.

Пример ответа, когда продление невозможно:

```json
{
    "id": "123456789",
    "expires_at": "2015-11-19T17:10:48+0300",
    "actions": [
        {
            "id": "prolongate",
            "enabled": false,
            "disable_reason": {
                "id": "standard_plus_publication_is_updated_automatically",
                "name": "Вакансия \"Стандарт Плюс\" не может быть обновлена, это происходит автоматически раз в три дня."
            }
        }
    ]
}
```

Пример ответа, когда продление возможно:

```json
{
    "id": "123456789",
    "expires_at": "2015-11-19T17:10:48+0300",
    "actions": [
        {
            "id": "prolongate",
            "enabled": true,
            "url": "https://api.hh.ru/vacancies/123456789/prolongate",
            "method": "POST"
        }
    ]
}
```

Имя | Тип | Описание
---- | --- | --------
actions | object | Cписок действий, которые можно предпринять для продления вакансии. В данный момент поддерживается только обычное продление.
actions.id | string | Идентификатор действия
actions.enabled | boolean | Флаг возможно ли действие
actions.disable_reason | object | Причина, по которой совершить действие невозможно. Элемент справочника [vacancy_not_prolonged_reason](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get) 
actions.url | string | url, с которыми нужно сделать запрос, чтобы совершить действие
actions.method | string | HTTP-метод, с которыми нужно сделать запрос, чтобы совершить действие

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем.
* `404 Not Found` – текущему пользователю недоступно получение информации о вакансии.
* `404 Not Found` – вакансия с переданным идентификатором не существует.


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
                "invitations_and_responses": 14
            },
            "expires_at": "2013-07-08T16:17:21+0400",
            "has_updates": false,
            "billing_type": {
                "id": "standard",
                "name": "Стандарт"
            },
            "can_upgrade_billing_type": true
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

