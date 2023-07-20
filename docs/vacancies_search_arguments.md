# Описание использованных параметров поиска вакансий

Для получения выставленных параметров в
[поиске вакансий](vacancies.md#search) необходимо в поисковом запросе на
`/vacancies` добавить параметр `describe_arguments=true`.

Пример выдачи параметров (приведён пример всех возможных параметров, в
реальных запросах данных будет меньше):

```json
{
    "arguments": [
        {
            "argument": "area",
            "value": "1",
            "value_description": "Москва",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "area",
                "name": "Регион"
            }
        },
        {
            "argument": "area",
            "value": "2",
            "value_description": "Санкт-Петербург",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=1&...",
            "cluster_group": {
                "id": "area",
                "name": "Регион"
            }
        },
        {
            "argument": "text",
            "value": "менеджер по продажам",
            "value_description": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "search_field",
            "value": "name",
            "value_description": "в названии вакансии",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "experience",
            "value": "between3And6",
            "value_description": "От 3 до 6 лет",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "experience",
                "name": "Опыт работы"
            }
        },
        {
            "argument": "employment",
            "value": "full",
            "value_description": "Полная занятость",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "employment",
                "name": "Тип занятости"
            }
        },
        {
            "argument": "schedule",
            "value": "fullDay",
            "value_description": "Полный день",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "schedule",
                "name": "График работы"
            }
        },
        {
            "argument": "metro",
            "value": "2.133",
            "value_description": "Сокол",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&metro=2&...",
            "cluster_group": {
                "id": "metro",
                "name": "Метро"
            },
            "metro_type": "station",
            "hex_color": "13703a"
        },
        {
            "argument": "industry",
            "value": "51",
            "value_description": "ЖКХ",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "industry",
                "name": "Отрасль компании"
            }
        },
        {
            "argument": "industry",
            "value": "51.675",
            "value_description": "Энергосбережение",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "sub_industry",
                "name": "Сфера компании"
            }
        },
        {
            "argument": "label",
            "value": "not_from_agency",
            "value_description": "Без вакансий агентств",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "label",
                "name": "Исключение"
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
            "value_description": "Указана зарплата",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "salary",
                "name": "Зарплата"
            }
        },
        {
            "argument": "salary",
            "value": "1500",
            "value_description": "от 1500 USD",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "salary",
                "name": "Зарплата"
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
            "value_description": "По убыванию зарплат",
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
            "value_description": "За неделю",
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
            "value_description": "За неделю",
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
            "value_description": "Охранник",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&area=1&area=2&...",
            "cluster_group": {
                "id": "professional_role",
                "name": "Профессиональная роль"
            }
        }
    ]
}
```

В списке выдаются только те параметры, которые
[влияют на поиск вакансий](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij/operation/get-vacancies),
неизвестные параметры игнорируются. Элемент списка с одним значением `argument`
может повторяться несколько раз, если параметр имеет несколько значений.

Для каждого элемента в списке `arguments` будет доступно:

Имя | Тип | Описание
---- | ----| --------
argument | string | параметр поиска вакансии
value | string | значение параметра
name | string или null | название значения, если оно есть, либо `null`
disable_url | string | url поиска вакансий, который получится, если перестать учитывать в поиске данный параметр
cluster_group | object или null | [группа кластеров](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij/Klastery-v-poiske-vakansij), которая связана с данным параметром, если она есть, либо `null`
cluster_group.id | string | идентификатор группы кластеров
cluster_group.name | string | название группы кластеров

Для аргумента `metro` доступны дополнительные поля:

Имя | Тип | Описание
---- | ----| --------
metro_type | string | станция или линия метро (`station`/`line`)
hex_color | string | цвет линии в HEX-формате RRGGBB (от 000000 до FFFFFF)
