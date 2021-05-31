# Предпочтения менеджера

> ‼ Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rabotodatelskie/paths/~1employers~1{employer_id}~1managers~1{manager_id}~1settings/get)

<a name="manager_settings"></a>
### Запрос

`GET /employers/{employer_id}/managers/{manager_id}/settings`

где:

* `employer_id` – идентификатор работодателя,
* `manager_id` – идентификатор менеджера.

Проще всего получить url из поля `manager_settings_url` в
[информации о текущем пользователе (объект `manager`)](me.md#manager-info).


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
  "default_currency": {
    "abbr": "руб.",
    "code": "RUR",
    "name": "Рубли"
  },
  "default_vacancy_branded_template": {
    "id": "default",
    "name": "Стандартный шаблон"
  },
  "use_sms_notification": true
}
```

Имя | Тип | Описание
--- | --- | ------
default_currency | объект | предпочитаемая валюта при [публикации вакансии](employer_vacancies.md#creation)
default_vacancy_branded_template | объект, null | предпочитаемый [брендированный шаблон вакансий работодателя](employer_vacancy_branded_templates.md). `null` – если у компании не используются брендированные шаблоны вакансий.
use_sms_notification | логический | предпочтение по использованию флага `send_sms` [при приглашении соискателя](employer_negotiations.md#add-invite)

Данные предпочтения **не влияют** на действия в API по умолчанию. Например,
брендированный шаблон оформления (`default_vacancy_branded_template`) не будет
применён автоматически при публикации вакансии, если шаблон не передан.
Предпочтения может использовать ваше приложение, чтобы реализовать логику
предзаполнения полей.

### Ошибки

* `404 Not Found` – менеджер не существует, либо просмотр его настроек не доступен.
* `403 Forbidden` – текущий пользователь не является менеджером.
