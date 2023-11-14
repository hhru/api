# Salary Database Catalogues

* [Industries and fields of expertise](#salary-industries)
* [Competency levels](#employee-levels)
* [Professions and specialist area](#professional-areas)
* [Regions and cities](#salary-areas)

<a name="salary-industries"></a>
## Industries and fields of expertise

```
GET /salary_statistics/dictionaries/salary_industries
```

The response contains a list of industries and fields of expertise.

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

Industry fields:

Name | Type | Description
--- | --- | ---
id | string | Industry ID
name | string | Industry name
industries | array | A list of fields of expertise
industries[].id | string | Field of expertise ID
industries[].name | string | Field of expertise name
 
<a name="employee-levels"></a>
## Competency levels

```
GET /salary_statistics/dictionaries/employee_levels
```

The response contains a list of competency levels.

```json
[
    {
        "id": "specialist",
        "name": "специалист",
        "description": "Прямые подчиненные отсутствуют, периодически координирует работу других сотрудников в рамках поставленной задачи."
    }
]
```

The fields of a competency level:

Name | Type | Description
--- | --- | ---
id | string | Level ID
name | string | Level name
description | string | Level description
 
 
<a name="professional-areas"></a>
## Professions and specialisations

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-professional-areas)

<a name="salary-areas"></a>
## Regions and cities

```
GET /salary_statistics/dictionaries/salary_areas
```

The response contains a list of regions and cities.

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

The fields of a region:

Name | Type | Description
--- | --- | ---
id | string | Region ID
name | string | Region name
areas | array | An array of subsidiary regions / cities with a structure similar to the region
