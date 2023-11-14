# Salary Database Catalogues

* [Industries and fields of expertise](#salary-industries)
* [Competency levels](#employee-levels)
* [Professions and specialist area](#professional-areas)
* [Regions and cities](#salary-areas)

<a name="salary-industries"></a>
## Industries and fields of expertise

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-industries)
 
<a name="employee-levels"></a>
## Competency levels

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Salary-Database-directories/operation/get-salary-employee-levels)

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
