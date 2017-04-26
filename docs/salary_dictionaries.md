# Справочники Банка данных заработных плат

* [Отрасли и сферы деятельности](#salary-industries)
* [Уровни специалистов](#employee-levels)
* [Профобласти и специализации](#professional-areas)
* [Регионы и города](#salary-areas)

<a name="salary-industries"></a>
## Отрасли и сферы деятельности

```
GET /salary_statistics/dictionaries/salary_industries
```

В ответе содержится список отраслей и сфер деятельности.

```json
[
    {
        "id": "49",
        "name": "Услуги для населения",
        "industries": [
            {
                "id": "409",
                "name": "Салоны красоты"
            }
        ]
    }
]
```

Поля отрасли:

Имя | Тип | Описание
--- | --- | ---
id | string | Идентификатор отрасли
name | string | Название отрасли
industries | array | Список сфер деятельности
industries[].id | string | Идентификатор сферы деятельности
industries[].name | string | Название сферы деятельности
 
<a name="employee-levels"></a>
## Уровни специалистов

```
GET /salary_statistics/dictionaries/employee_levels
```

В ответе содержится список уровней специалистов.

```json
[
    {
        "id": "specialist",
        "name": "специалист",
        "description": "Прямые подчиненные отсутствуют, периодически координирует работу других сотрудников в рамках поставленной задачи."
    }
]
```

Поля уровня специалиста:

Имя | Тип | Описание
--- | --- | ---
id | string | Идентификатор уровня
name | string | Название уровня
description | string | Описание уровня
 
 
<a name="professional-areas"></a>
## Профобласти и специализации

```
GET /salary_statistics/dictionaries/professional_areas
```

В ответе содержится список профобластей и специализаций.

```json
[
    {
        "id": "1030000",
        "name": "Административная поддержка",
        "specializations": [
            {
                "id": "1030015",
                "name": "Архив",
                "description": "Организация социальной работы с сотрудниками, распределение фонда материальной и социальной помощи"
            }
        ]
    }
]
```

Поля профобласти:

Имя | Тип | Описание
--- | --- | ---
id | string | Код профобласти
name | string | Название профобласти
specialiaztions | array | Список специализаций профобласти
specialiaztions[].id | string | Код специализации
specialiaztions[].name | string | Название специализации
specialiaztions[].description | string | Описание специализации


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
