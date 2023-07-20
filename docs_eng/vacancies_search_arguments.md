# Description of selected vacancy search arguments

To get selected arguments in [vacancy search](vacancies.md#search), add `describe_arguments=true` argument to the `/vacancies` search query.

Example of argument results (includes all existing arguments,
real queries will be shorter):

```json
{
    "arguments": [
        {
            "argument": "area",
            "value": "1",
            "value_description": "Moscow",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "area",
                "name": "Region"
            }
        },
        {
            "argument": "area",
            "value": "2",
            "value_description": "St. Petersburg",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=1&...",
            "cluster_group": {
                "id": "area",
                "name": "Region"
            }
        },
        {
            "argument": "text",
            "value": "Manager",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "search_field",
            "value": "name",
            "value_description": "in vacancy name",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "experience",
            "value": "between3And6",
            "value_description": "Between 3 and 6 years",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "experience",
                "name": "experience"
            }
        },
        {
            "argument": "employment",
            "value": "full",
            "value_description": "Full time",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "employment",
                "name": "Employment type"
            }
        },
        {
            "argument": "schedule",
            "value": "fullDay",
            "value_description": "Full day",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "schedule",
                "name": "Work schedule"
            }
        },
        {
            "argument": "metro",
            "value": "2.133",
            "value_description": "Sokol",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&metro=2&...",
            "cluster_group": {
                "id": "metro",
                "name": "Metro"
            },
            "metro_type": "station",
            "hex_color": "13703a"
        },
        {
            "argument": "industry",
            "value": "51",
            "value_description": "Other",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "industry",
                "name": "Company branch"
            }
        },
        {
            "argument": "industry",
            "value": "51.675",
            "value_description": "Energy saving",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "sub_industry",
                "name": "Company's sphere of activity"
            }
        },
        {
            "argument": "label",
            "value": "not_from_agency",
            "value_description": "No vacancies from agencies",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "label",
                "name": "Exclusion"
            }
        },
        {
            "argument": "currency",
            "value": "USD",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "only_with_salary",
            "value": "true",
            "value_description": "Do not show resumes without salary specified",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "salary",
                "name": "Salary"
            }
        },
        {
            "argument": "salary",
            "value": "1500",
            "value_description": "от 1500 USD",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "salary",
                "name": "Salary"
            }
        },
        {
            "argument": "bottom_lat",
            "value": "55.58",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "left_lng",
            "value": "37.52",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "top_lat",
            "value": "55.74",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "right_lng",
            "value": "37.86",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "date_from",
            "value": "2017-02-01",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "date_to",
            "value": "2017-02-10",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "order_by",
            "value": "salary_desc",
            "value_description": "by salary descending",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "sort_point_lat",
            "value": "55.74",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "sort_point_lng",
            "value": "37.86",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "period",
            "value": "7",
            "value_description": "last week",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "employer_id",
            "value": "1455",
            "value_description": "HeadHunter",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "search_period",
            "value": "7",
            "value_description": "last week",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "no_magic",
            "value": "true",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "host",
            "value": "hh.kz",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "per_page",
            "value": "10",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?page=0&area=1&area=2...",
            "cluster_group": null
        },
        {
            "argument": "page",
            "value": "0",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&area=1&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "professional_role",
            "value": "90",
            "value_description": "Security guard",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&area=1&area=2&...",
            "cluster_group": {
                "id": "professional_role",
                "name": "Professional role"
            }
        }
    ]
}
```

The list only includes those arguments that [affect vacancy search](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/operation/get-vacancies), 
unknown arguments are ignored. A list item with one `argument` value
can be repeated several times if the argument has several values.

For each element in the `arguments` list you will have available:

Name | Type | Description
---- | ----| --------
argument | string | vacancy search argument
value | string | argument value
name | string or null | name of value if it exists, otherwise — `null`
disable_url | string | url of the resulting vacancy search if this argument is no longer selected
cluster_group | object или null | [cluster group](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-search/Clusters-of-vacancy-search) related to this argument if it exists, otherwise — `null`
cluster_group.id | string | id of cluster group
cluster_group.name | string | name of cluster group

Additional fields are available for the `metro` argument:

Name | Type | Description
---- | ----| --------
metro_type | string | metro station or line (`station`/`line`)
hex_color | string | HEX colour code of the line RRGGBB (from 000000 to FFFFFF)
