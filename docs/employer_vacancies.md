# Вакансии для работодателя

* [Варианты публикации вакансий](#available_types)
* [Публикация вакансий](#creation)
* [Условия заполнения полей при добавлении и редактировании вакансий](#conditions)
* [Редактирование вакансий](#edit)
* [Продление вакансий](#prolongate)
* [Информация о возможности продления вакансии](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-prolongation-vacancy-info)
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

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/operation/get-available-vacancy-types)

<a name="creation"></a>
## Публикация вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/publish-vacancy)

<a name="conditions"></a>
## Условия заполнения полей при добавлении и редактировании вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-vacancy-conditions)

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
branded_template.id | <a name="branded-template-field"></a> брендированное оформление вакансии из [справочника](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/operation/get-vacancy-branded-templates-list)
languages | список языков
driver_license_types | категория водительских прав. Элемент справочника [driver_license_types](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)

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
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/vacancy-prolongation)

## Информация о возможности продления вакансии
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-prolongation-vacancy-info)

<a name="active"></a>
## Список опубликованных вакансий

> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/get-active-vacancy-list)

<a name="archive"></a>
## Архивация вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/add-vacancy-to-archive)

<a name="archived"></a>
## Список архивных вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-archived-vacancies)

<a name="hide"></a>
## Удаление вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/add-vacancy-to-hidden)

<a name="hidden"></a>
## Список удаленных вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-hidden-vacancies)

<a name="restore"></a>
## Восстановление из удаленных

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/restore-vacancy-from-hidden)

<a name="stats"></a>
## Статистика по вакансии

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-vacancy-stats)

<a name="visitors"></a>
## Просмотры вакансии

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/get-vacancy-visitors)
