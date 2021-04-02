# Reports of the Salary Database

* [Salary assessment without forecasts](#salary-evaluation)
    * [Request parameters](#salary-evaluation-params)
    * [Examples of requests](#salary-evaluation-examples)
    * [Successful response](#salary-evaluation-response)
        * [Parameters of indirect salary assessment](#salary-evaluation-response-indirect-calculation)
    * [Errors](#salary-evaluation-errors)

<a name="salary-evaluation"></a>
## Salary assessment without forecasts

Method for obtaining salary assessment without forecasts.
[User authorisation](authorization_for_user.md) is required
and a user must have access to paid reports of the Salary Database(https://salary.hh.ru).

```
GET /salary_statistics/paid/salary_evaluation/{area_id}
```

where
* `area_id` — region code (federal districts, constituent entities, cities) on which the sample will be based to generate the report. See [directory of regions](salary_dictionaries.md#salary-areas).


<a name="salary-evaluation-params"></a>
### Request parameters

Name | Required | Description
--- | --- | ---
exclude_area | not | Region codes (federal districts, constituent entities, cities) which will be excluded from the sample in any case to generate the report. The parameter is used to obtain assessments in the regional market with the exception of certain cities/regions.  See [directory of regions](salary_dictionaries.md#salary-areas)
employee_level | not | Levels of specialists which will be included in the sample to generate the report. See [directory of levels of specialists](salary_dictionaries.md#employee-levels)
industry | not | Industry codes on which the sample will be based to generate the report.  See [directory of industries](salary_dictionaries.md#salary-industries)
speciality | not | Codes of professional areas and specialisations which will be included in the sample to generate the report. See [directory of professional areas and specialisations](salary_dictionaries.md#professional-areas)
extend_sources | not | Data from CVs and vacancies shall be used if there is no data in the Salary Database that corresponds to the specified parameters. This parameter is set to 'true' or 'false'. Default — 'false'.
position_name | not | Position name. If there are no `speciality` or `employee_level`, the service will determine the possible specializations and level of employee for the specified position and industry and it will make the report by them.

<a name="salary-evaluation-examples"></a>
### Examples of requests

Salaries in Russia, except for Moscow and St. Petersburg, for the "Specialist" level,
in companies operating in the "Information Technology" or "Agriculture" industries: 

```
GET /salary_statistics/paid/salary_evaluation/113?
    exclude_area=1&
    exclude_area=2&
    employee_level=specialist&
    industry=7&
    industry=29
```

Salaries in Moscow for the levels "Leading Specialist" and "Expert"
in the specialisations "Software Development Management" and "Project Management":

```
GET /salary_statistics/paid/salary_evaluation/1?
    employee_level=senior_specialist&
    employee_level=expert&
    speciality=1170001&
    speciality=1170002
```

<a name="salary-evaluation-response"></a>
### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "market_salary": {
        "upper": 50000,
        "minimum": 20000,
        "median": 35000,
        "average": 50054,
        "maximum": 52643,
        "bottom": 28500
    },
    "resulting_parameters": {
        "areas": [
            {
                "id": "10010",
                "name": "Южный федеральный округ"
            }
        ],
        "excluded_areas": [
            {
                "id": "1530",
                "name": "Ростовская область"
            }
        ],
        "employee_levels": [
            {
                "id": "specialist",
                "name": "Специалист"
            }
        ],
        "industries": [
            {
                "id": "7",
                "name": "Информационные технологии, системная интеграция, интернет"
            }
        ],
        "specialities": [
            {
                "id": "1200000",
                "name": "Эксплуатация информационных систем"
            }
        ],
        "sources": [
            "SALARIES",
            "RESUMES",
            "VACANCIES"
        ],
        "indirect_calculation": null,
        "positions_count": 1648,
        "employers_count": 21
    }
}
```

Name | Type | Description
----|-----|---------
resulting_parameters | object | Set of parameters on the basis of which the calculation was performed
resulting_parameters.areas | array | Region codes (federal districts, constituent entities, cities)
resulting_parameters.excluded_areas | array или null | Excluded region codes (federal districts, constituent entities, cities)
resulting_parameters.employee_levels | array или null | Levels of specialists included in the sample in the target region
resulting_parameters.industries | array или null | Industries
resulting_parameters.specialities | array или null | Professional areas
resulting_parameters.sources | array | Data sources used
resulting_parameters.indirect_calculation | object или null | [Parameters of indirect assessment of salary values](#salary-evaluation-response-indirect-calculation)
employers_count | number | Number of employers whose data are included in the sample
positions_count | number | Number of employee records in questionnaires, on which the sample is based
market_salary | object | Market range of salary values
market_salary.maximum | number | Maximum values (90th percentile)
market_salary.upper | number | Upper limit of market range (75th percentile)
market_salary.median | number | Market average (median)
market_salary.average | number | Average calculated value
market_salary.bottom | number | Lower limit of market range (25th percentile)
market_salary.minimum | number | Minimum values (10th percentile)


<a name="salary-evaluation-response-indirect-calculation"></a>
#### Parameters of indirect salary assessment

The `resulting_parameters.indirect_calculation` field is present in the response only when data is requested
for one region and contains parameters of indirect salary assessment.

In the above example, instead of `"indirect_calculation": null`, there may be the following:

```json
{
    "indirect_employee_levels": [
        {
            "id": "senior_specialist",
            "name": "Ведущий специалист"
        }
    ],
    "indirect_areas":[
        {
            "id": "1",
            "name": "Москва"
        }
    ],
    "indirect_regional_ratio": 0.4375
}
```

Name | Type | Description
----|-----|---------
indirect_calculation.indirect_areas | array or null | Regions used for indirect calculation
indirect_calculation.indirect_employee_levels | array or null | Levels of specialists included in the sample in the region used for indirect calculation
indirect_calculation.indirect_regional_ratio | number | Regional factor used to obtain indirect salary assessment

The response given above means that:
* the request for the "Southern Federal District" (`resulting_parameters.areas`) region
* gave no data on salaries for the requested "Specialist" (`resulting_parameters.employee_levels`) level
* however the indirect calculation
    * for the "Leading Specialist" (`resulting_parameters.indirect_calculation.indirect_employee_levels`) level
    * in the "Moscow" (`resulting_parameters.indirect_calculation.indirect_areas`) region was performed.
    * coefficient was 0.4375 (`resulting_parameters.indirect_calculation.indirect_regional_ratio`)

<a name="salary-evaluation-errors"></a>
### Errors

* `400 Bad Request` — error in parameters.
* `403 Forbidden` — user has no access or is not authorised.
* `404 Not Found` — no data available for the specified parameters.
