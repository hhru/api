# Region directory

See also:

* [Region suggestions](suggests.md#areas)


<a name="areas"></a>
## Tree view of all regions

`GET /areas` returns a tree view list of all regions with the indication of
region name and ID and the link to a parent region `parent_id`.

```json
[
    {
        "name": "Ukraine",
        "id": "5",
        "parent_id": null,
        "areas": [
            {
                "name": "Kiev",
                "id": "115",
                "parent_id": "5",
                "areas": []
            }
        ]
    }
]
```

Example: [https://api.hh.ru/areas?locale=EN](https://api.hh.ru/areaslocale=EN)


<a name="item"></a>
## Region directory, starting from the indicated region

`GET /areas/{area_id}` returns the region tree view list, starting from the
indicated region.

Example: [https://api.hh.ru/areas/1146?locale=EN](https://api.hh.ru/areas/1146?locale=EN)
