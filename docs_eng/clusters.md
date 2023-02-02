## Clusters in vacancy search

In [vacancies search](vacancies.md#search) vacancies are conveniently separated
according to different criteria.
For example, when searching by criteria, it may be useful to know
how salaries are distributed in the selected vacancies — for how many vacancies it is
specified, where it is above a certain amount. This information can be obtained
using the vacancies search by creating a separate request for each criterion
you are interested in. However, there is a better way, a special search result option —
divide data into clusters.
Cluster includes vacancy search link with certain filter. 
Thr purpose of usage clusters is getting less search result set.

You can find an example of this on the hh.ru homepage,
in the left column on the [page with vacancies search results](https://hh.ru/search/vacancy).

To obtain data by clusters, add `clusters=true` argument in the `/vacancies` search. In this case, the search response
will return additional division by clusters, as well as
normal search results. If you want to get only clusters without a list of found vacancies,
you can add `?per_page=0` to the query. 

Clusters are divided into groups; groups consist of clusters with
similar meaning. For example, the `Salary` group may contain clusters
"starts from RUB45,000" and "starts from RUB75,000". If the cluster doesn't consist searching criteria, then it has an empty array of clusters when following the url. 

Example cluster results in the search, the `clusters` key is added to
[standard vacancies search results](vacancies.md#search-results).
(includes all possible cluster groups, not all of them will be in real queries):

```json
{
  "clusters": [
    {
      "id": "professional_area",
      "name": "Professional field",
      "items": [
        {
          "name": "Gyms, fitness, beauty salons",
          "url": "https://api.hh.ru/vacancies?clusters=true&specialization=24&per_page=1",
          "count": 2852
        },
        {
          "name": "Installation and service",
          "count": 2469,
          "url": "https://api.hh.ru/vacancies?clusters=true&specialization=25&per_page=1"
        }
      ]
    },
    {
      "id": "specialization",
      "name": "Specialist field",
      "items": [
        {
          "name": "Sales",
          "url": "https://api.hh.ru/vacancies?clusters=true&specialization=15.389",
          "count": 3098
        },
        {
          "name": "Administrative Personnel",
          "url": "https://api.hh.ru/vacancies?clusters=true&specialization=15.388",
          "count": 1035
        }
      ]
    },
    {
      "id": "area",
      "name": "Region",
      "items": [
        {
          "name": "Moscow",
          "url": "https://api.hh.ru/vacancies?clusters=true&area=1",
          "count": 83285
        },
        {
          "name": "Moscow Oblast",
          "url": "https://api.hh.ru/vacancies?clusters=true&area=2019",
          "count": 16413
        }
      ]
    },
    {
      "id": "metro",
      "name": "Metro",
      "items": [
        {
          "name": "Zamoskvoretskaya",
          "url": "https://api.hh.ru/vacancies?clusters=true&metro=2&area=1",
          "count": 11639,
          "type": "metro_line",
          "metro_line": {
            "id": "2",
            "hex_color": "4FB04F",
            "area": {
              "id": "1",
              "name": "Moscow",
              "url": "https://api.hh.ru/areas/1"
            }
          }
        },
        {
          "name": "Alekseevskaya",
          "url": "https://api.hh.ru/vacancies?clusters=true&metro=6.8&area=1",
          "count": 1046,
          "type": "metro_station",
          "metro_station": {
            "id": "6.8",
            "hex_color": "4FB04F",
            "lat": 55.807794,
            "lng": 37.638699,
            "order": 5,
            "area": {
              "id": "1",
              "name": "Moscow",
              "url": "https://api.hh.ru/areas/1"
            }
          }
        }
      ]
    },
    {
      "id": "schedule",
      "name": "Work schedule",
      "items": [
        {
          "name": "Full day",
          "url": "https://api.hh.ru/vacancies?clusters=true&schedule=fullDay",
          "count": 67101
        },
        {
          "name": "Shift schedule",
          "url": "https://api.hh.ru/vacancies?clusters=true&schedule=shift",
          "count": 10736
        }
      ]
    },
    {
      "id": "experience",
      "name": "Work experience",
      "items": [
        {
          "name": "Between 1 and 3 years",
          "url": "https://api.hh.ru/vacancies?clusters=true&experience=between1And3",
          "count": 39873
        },
        {
          "name": "Between 3 and 6 years",
          "url": "https://api.hh.ru/vacancies?clusters=true&experience=between3And6",
          "count": 22922
        }
      ]
    },
    {
      "id": "label",
      "name": "Exclusion",
      "items": [
        {
          "name": "No vacancies from agencies",
          "url": "https://api.hh.ru/vacancies?clusters=true&label=not_from_agency",
          "count": 77116
        },
        {
          "name": "With address only",
          "url": "https://api.hh.ru/vacancies?clusters=true&label=with_address",
          "count": 47774
        },
        {
          "name": "Only vacancies suitable for people with a disability",
          "url": "https://api.hh.ru/vacancies?clusters=true&label=accept_handicapped",
          "count": 1407
        },
        {
          "name": "Only available to candidates aged 14+",
          "url": "https://api.hh.ru/vacancies?clusters=true&label=accept_kids",
          "count": 607
        },
        {
          "name": "Vacancies from accredited IT employers",
          "url": "https://api.hh.ru/vacancies?clusters=true&label=accredited_it",
          "count": 421
        },
        {
          "name": "Only vacancies with less than 10 responses",
          "url": "https://api.hh.ru/vacancies?clusters=true&label=low_performance",
          "count": 254
        }
      ]
    },
    {
      "id": "salary",
      "name": "Salary",
      "items": [
        {
          "name": "Specified",
          "url": "https://api.hh.ru/vacancies?clusters=true&only_with_salary=true",
          "count": 51300
        },
        {
          "name": "from 45000 RUB",
          "url": "https://api.hh.ru/vacancies?salary=45000&clusters=true&only_with_salary=true",
          "count": 40026
        },
        {
          "name": "from 75000 RUB",
          "url": "https://api.hh.ru/vacancies?salary=75000&clusters=true&only_with_salary=true",
          "count": 19903
        }
      ]
    },
    {
      "id": "employment",
      "name": "Employment type",
      "items": [
        {
          "name": "Full time",
          "url": "https://api.hh.ru/vacancies?clusters=true&employment=full",
          "count": 79713
        },
        {
          "name": "Part time",
          "url": "https://api.hh.ru/vacancies?clusters=true&employment=part",
          "count": 2699
        }
      ]
    },
    {
      "id": "industry",
      "name": "Company branch",
      "items": [
        {
          "name": "IT, System Integration, Internet",
          "url": "https://api.hh.ru/vacancies?clusters=true&industry=7",
          "count": 10316
        },
        {
          "name": "Agriculture",
          "url": "https://api.hh.ru/vacancies?clusters=true&industry=29",
          "count": 512
        }
      ]
    },
    {
      "name": "Education",
      "id": "education",
      "items": [
        {
          "name": "Not required or not specified",
          "url": "https://api.hh.ru/vacancies?clusters=true&text=java&education=not_required_or_not_specified",
          "count": 410
        },
        {
          "name": "Special secondary",
          "url": "https://api.hh.ru/vacancies?clusters=true&text=java&education=special_secondary",
          "count": 5219
        },
        {
          "name": "Higher",
          "url": "https://api.hh.ru/vacancies?clusters=true&text=java&education=higher",
          "count": 4310
        }
      ]
    }
  ]
}
```

The set of cluster groups (elements of the `clusters` array) may vary
from query to query and depends on the parameters of the search query. You can find the list of all possible cluster groups
in the [directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries), in the elements with the `vacancy_cluster` key.

In this case, if the search query contained `clusters=false` or the
`cluster` argument was not specified, the `clusters` field will have `null` in the response.

Each cluster group has the following fields:

Name | Type | Value
--- | --- | ---
id | string | Cluster type
name | string | Name of cluster type
items | array | The search query array in this cluster, specifying additional parameters

Each element of the `items` array is an object with the following fields:

Name | Type | Value
--- | --- | ---
name | string | Name of cluster element
url | string | Link to search results for this cluster element
count | number | Number of vacancies in this cluster element
type | string or null | Type of value related to the group

### Types of clusters

Types currently available:

* `metro_line` - metro line
* `metro_station` - metro station


For metro lines(`type=metro_line`), the system additionally gives a key `metro_line` containing 
an object with the following fields:

Name | Type | Value
--- | --- | ---
id | string | line ID
hex_color | string | HEX colour code of the line in RRGGBB format (from 000000 to FFFFFF)
area | object | [Region](areas.md) (city) of the line

For metro station (`type=metro_station`), the system additionally gives a key `metro_station` containing
an object with the following fields:

Name | Type | Value
--- | --- | ---
id | string | station ID
hex_color | string | HEX colour code of the line in RRGGBB format (from 000000 to FFFFFF)
lat, lng | number | station coordinates (latitude and longitude)
order | number | station order on the metro line
area | object | [Region](areas.md) where the station is located
