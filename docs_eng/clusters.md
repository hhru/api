## Clusters in vacancy search

In [vacancies search](vacancies.md#search) vacancies are conveniently separated
according to different criteria.
For example, when searching by criteria, it may be useful to know
how salaries are distributed in the selected vacancies — for how many vacancies it is
specified, where it is above a certain amount. This information can be obtained
using the vacancies search by creating a separate request for each criterion
you are interested in. However, there is a better way, a special search result option —
divide data into clusters.

You can find an example of this on the hh.ru homepage,
in the left column on the [page with vacancies search results](https://hh.ru/search/vacancy).

To obtain data by clusters, add `clusters=true` argument in the `/vacancies` search. In this case, the search response
will return additional division by clusters, as well as
normal search results. If you want to get only clusters without a list of found vacancies,
you can add `?per_page=0` to the query.

Clusters are divided into groups; groups consist of clusters with
similar meaning. For example, the `Salary` group may contain clusters
"starts from RUB45,000" and "starts from RUB75,000".

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
    }
    // ...
  ]
}
```

The set of cluster groups (elements of the `clusters` array) may vary
from query to query and depends on the parameters of the search query. You can find the list of all possible cluster groups
in the [directory](dictionaries.md), in the elements with the `vacancy_cluster` key.

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
