# Работа с вакансиями для соискателя

* [Отобранные вакансии](#favorited)
* [Дополнительные поля вакансии для соискателей](#vacancy-fields-applicant)
* [Скрытые вакансии](blacklisted.md)


<a name="favorited"></a>
## Отобранные вакансии

Данные методы требуют авторизации соискателем, иначе вернут `403 Forbidden`.

`GET /vacancies/favorited` - возвращает [подмножество вакансий](vacancies.md#item), добавленных
пользователем в отобранные с [дополнительными полями для соискателя](#vacancy-fields-applicant). Пейджинг работает по стандартным page&per_page,
страницы нумеруются с нуля.

`PUT /vacancies/favorited/{vacancy_id}` добавит указанную вакансию в список.
Данная операция — идемпотентная: при добавлении вакансии, которая уже есть в
отобранных, вернётся также `204 No Content`, как и в случае первичного
добавления.

`DELETE /vacancies/favorited/{vacancy_id}` удалит вакансию из списка отобранных
авторизованного пользователя. Операция также идемпотентна.
При успешном удалении метод возвращает `204 No Content`.

### Ошибки

* `404 Not Found` - если вакансия не найдена
* `403 Forbidden` - у пользователя не хватает прав
* `403 Forbidden` - при запросе не от имени соискателя

Дополнительно к HTTP коду сервер может вернуть описание причины ошибки

HTTP code | type | value | описание
----------|------|-------|-----------
403 | vacancies_favorited | vacancy_archived | вакансия уже архивирована и не может быть добавлена в отобранное
403 | vacancies_favorited | limit_exceeded | превышен лимит количества отобранных вакансий


<a name="vacancy-fields-applicant"></a>
## Дополнительные поля вакансии для соискателей

При авторизации соикателем возвращаются дополнительные поля:

```json
{
    "relations": [
        "favorited",
        "got_response"
    ],
    "negotiations_url": "https://api.hh.ru/negotiations?vacancy_id=8331228",
    "suitable_resumes_url": "https://api.hh.ru/vacancies/8331228/suitable_resumes"
}
```

Имя | Тип | Описание
---- | --- | --------
relations | array | При авторизации соискателем, возвращает связи с вакансией. Значения из [справочника vacancy_relation](dictionaries.md).
negotiations_url | string | Cсылка для получения списка откликов/приглашений
suitable_resumes_url | string | Подходящие резюме на вакансию

Смотрите также [отклики на вакансии](negotiations.md#post_negotiation).
