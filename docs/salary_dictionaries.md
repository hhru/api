# Справочники Банка данных заработных плат

* [Отрасли и сферы деятельности](#salary-industries)
* [Уровни специалистов](#employee-levels)
* [Профобласти и специализации](#professional-areas)
* [Регионы и города](#salary-areas)

<a name="salary-industries"></a>
## Отрасли и сферы деятельности

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-industries)
 
<a name="employee-levels"></a>
## Уровни специалистов

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-employee-levels)

<a name="professional-areas"></a>
## Профобласти и специализации

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-professional-areas)

<a name="salary-areas"></a>
## Регионы и города

```
GET /salary_statistics/dictionaries/salary_areas
```

В ответе содержится список регионов, областей и городов.

```json
[
    {
        "id": "1",
        "name": "Россия",
        "areas": [
            {
                "id": "2",
                "name": "Алтайский край",
                "areas": [
                    {
                        "id": "3",
                        "name": "Алейск",
                        "areas": []
                    }
                ]
            }    
        ]
    }
]
```

Поля региона:

Имя | Тип | Описание
--- | --- | ---
id | string | Идентификатор региона
name | string | Название региона
areas | array | Массив дочерних областей/городов со структурой, аналогичной региону
