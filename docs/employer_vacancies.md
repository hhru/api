# Вакансии для работодателя

* [Список опубликованных вакансий](#active)
* [Архивация вакансий](#archive)
* [Список архивных вакансий](#archived)
* [Удаление вакансии](#hide)
* [Список удаленных вакансий](#hidden)
* [Восстановление из удаленных](#restore)

Смотрите также:

* [Публикация вакансий](vacancies.md#creation)
* [Редактирование вакансий](vacancies.md#edit)
* [Продление вакансий](vacancies.md#prolongate)


<a name="active"/>
## Список опубликованных вакансий

`GET /employers/{employer_id}/vacancies/active?manager_id={manager_id}`

Для просмотра списка опубликованных вакансий необходимо указать id менеджера,
даже если необходимо сделать запрос для текущего менеджера (значение можно
взять из `/me`).

Помимо [стандартных полей вакансии](vacancies.md#nano) вернутся дополнительные
поля:

```json
{
  "counters": {
    "views": 100500,
    "responses": 5,
    "unread_responses": 3,
    "invitations": 10
  },
  "expires_at": "2013-07-08T16:17:21+0400",
  "has_updates": false
}
```

ключ | тип | описание
-----|-----|---------
counters.views | number | количество просмотров вакансии
counters.responses | number | количество откликов на вакансию
counters.unread_responses | number | количество непросмотренных откликов на вакансию
counters.invitations | number | количество приглашений на вакансию
expires_at | string | дата окончания публикации вакансии
has_updates | boolean | Есть ли в откликах/приглашениях по данной вакансии обновления, требующие внимания

Также доступен
[список опубликованных вакансий, подходящих для приглашения соискателя](employer_vacancies_for_invitation.md).

### Поддерживаемые параметры

Помимо стандартных параметров для пагинации `per_page` и `page`, коллекция поддерживает:

* `text` — строка для поиска по названию вакансии
* `area` — id региона (см.
  [список регионов, в которых есть активные вакансии](employer_vacancy_areas_active.md))
* `order_by` — сортировка вакансий, возможные варианты доступны в справочнике
  `employer_active_vacancies_order`


<a name="archive"/>
## Архивация вакансий

Для переноса вакансии в архив необходимо отправить запрос PUT:

`PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}`

При успешной архивации вернётся `204 No Content`.


<a name="archived"/>
## Список архивных вакансий

`GET /employers/{employer_id}/vacancies/archived?manager_id={manager_id}`

Для просмотра списка архивных вакансий также необходимо указать id менеджера,
даже если необходимо сделать запрос для текущего менеджера (значение можно
взять из `/me`). Поддерживается пагинация (`per_page` и `page`) и сортировка
(`order_by`). Возможные значения сортировки доступны в справочнике
`employer_archived_vacancies_order` (`/dictionaries`). В отличие от списка
опубликованных вакансий, данная коллекция не поддерживает поиск (параметры
`text` и `area`).

Помимо [стандартных полей вакансии](vacancies.md#nano) вернутся дополнительные
поля:

```json
{
  "counters": {
    "responses": 3,
    "invitations_and_responses": 5
  },
  "archived_at": "2013-07-08T16:17:21+0400"
}
```

ключ | тип | описание
---- |---- |---------
counters.responses | числовой | количество откликов на вакансию
counters.invitations_and_responses | числовой | количество откликов и приглашений на вакансию
archived_at | строка | дата архивации вакансии


<a name="hide"/>
## Удаление вакансии

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

Удалить можно только вакансию из архива.
При успешной операции вернётся `204 No Content`.


<a name="hidden"/>
## Список удаленных вакансий

`GET /employers/{employer_id}/vacancies/hidden?manager_id={manager_id}`

Поддерживается пагинация (`per_page` и `page`) и сортировка (`order_by`).
Возможные значения сортировки доступны в справочнике
`employer_hidden_vacancies_order` (`/dictionaries`). В отличие от списка
опубликованных вакансий, данная коллекция не поддерживает поиск (параметры
`text` и `area`).


<a name="restore"/>
## Восстановление из удаленных

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

Восстановить можно только удаленную из архива вакансию.
При успешной операции вернётся `204 No Content`.
Вакансия вернется в архив.
