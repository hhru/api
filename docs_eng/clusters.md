## Clusters in vacancy search

In vacancy search, you can conveniently obtain advanced information about
vacancy categorization by various search criteria. For instance, upon search by
criteria, you can view requested vacancies split by salary (e.g. the number of
vacancies with salary indicated, or the number of vacancies with a salary
exceeding a set amount). Such data can be retrieved using vacancy search by
separate request for each given criterion. However, it is far easier to use a
special search result option, such as splitting data into clusters.

See an example of using such data on the main hh.ru site see in the left column
on the [vacancy search result page](https://hh.ru/search/vacancy).

If you only need this metadata (and you don't need the list of found vacancies)
enter `?per_page=0` in the request.

In order to get clustered data, in search request for `/vacancies` add parameter
`clusters=true`. Beside the search results, the search display will include
vacancies grouped by cluster.

```json
{
  "items": [],
  "found": 306158,
  "pages": 2000,
  "per_page": 1,
  "page": 0,
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
  ]
}
```

Set of cluster object types (`id` in the elements of the massive `clusters`) may
vary from one request to another and depends on parameters of the requests. See
the full list of clusters in the [reference guide](dictionaries.md) in the entry
with a key `vacancy_cluster`.

Thereby, if the search request contains `clusters=false` and parameter
`clusters` was not specified at all, the `clusters` field in the response
will be `null`.

Each cluster has the following fields:

 Name | Type | Value
 --- | --- | ---
 id | string | Cluster type
 name | string | Cluster type name
 items | array | Search request array in this cluster indicating optional parameters

Each array entry `items` is an object with the following fields:

 Name | Type | Value
 --- | --- | ---
 name | string | Cluster entry name
 url | string | Reference to search results on this cluster entry
 count | number | Number of vacancies in this cluster entry
