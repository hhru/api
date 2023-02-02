# Работа с вакансиями для соискателя

* [Отобранные вакансии](#favorited)
* [Дополнительные поля вакансии для соискателей](#vacancy-fields-applicant)
* [Скрытые вакансии](https://api.hh.ru/openapi/redoc#tag/Skrytye-vakansii)


<a name="favorited"></a>
## Отобранные вакансии

Данные методы требуют авторизации соискателем, иначе вернут `403 Forbidden`.

## Получение списка отобранных вакансий
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otobrannye-vakansii/operation/get-favorite-vacancies)

## Добавление вакансии в список отобранных 
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otobrannye-vakansii/operation/add-vacancy-to-favorite)

## Удаление вакансии из списка отобранных
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otobrannye-vakansii/operation/delete-vacancy-from-favorite)

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
relations | array | При авторизации соискателем, возвращает связи с вакансией. Значения из [справочника vacancy_relation](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
negotiations_url | string | Cсылка для получения списка откликов/приглашений
suitable_resumes_url | string | Подходящие резюме на вакансию

Смотрите также [отклики на вакансии](negotiations.md#post_negotiation).
