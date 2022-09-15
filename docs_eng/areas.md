# Region directory

> Attention! The values in the directories may change at any time. Do not address them directly.

* [Tree view of all regions](#areas)
* [Region directory, starting from the indicated region](#item)
* [Countries](#countries)
* [Additional request parameters](#additional_parameters)

See also:

* [Region suggestions](suggests.md#areas)


<a name="areas"></a>
## Tree view of all regions

`GET /areas` returns a tree view list of all regions with the indication of
region name and ID and the link to a parent region `parent_id`.

```json
[
    {
        "name": "Kazakhstan",
        "id": "40",
        "parent_id": null,
        "areas": [
            {
                "name": "Abai",
                "id": "6251",
                "parent_id": "40",
                "areas": []
            }
        ]
    }
]
```

Example: [https://api.hh.ru/areas?locale=EN](https://api.hh.ru/areas?locale=EN)


<a name="item"></a>
## Region directory, starting from the indicated region

`GET /areas/{area_id}` returns the region tree view list, starting from the
indicated region.

Example: [https://api.hh.ru/areas/1146?locale=EN](https://api.hh.ru/areas/1146?locale=EN)


<a name="countries" />
## Countires

`GET /areas/countries` returns the regions list with countries.

```json
[
  {
    "url": "https://api.hh.ru/areas/113",
    "id": "113",
    "name": "Russia"
  },
  {
    "url": "https://api.hh.ru/areas/6",
    "id": "6",
    "name": "Australia"
  }
]
 ```
<a name="additional_parameters"></a>
## Additional request parameters

Only for Russian localization, you can get an additional field — area name in prepositional case. To do this, pass the query parameter:

`GET /areas/{area_id}?additional_case=prepositional`

Example: [https://api.hh.ru/areas/1?additional_case=prepositional](https://api.hh.ru/areas/1?additional_case=prepositional)

```json
{
  "id": "1",
  "parent_id": "113",
  "name": "Москва",
  "areas": [],
  "name_prepositional": "в Москве"
}
```

### Errors when querying
Passing an unsupported case returns the error

`GET /areas/{area_id}?additional_case=wrong_case`

Example: [https://api.hh.ru/areas/1?additional_case=wrong_case](https://api.hh.ru/areas/1?additional_case=wrong_case)

```json
{
  "errors": [
    {
      "type": "bad_argument",
      "value": "wrong_case"
    }
  ]
}
```
