# Region directory

* [Tree view of all regions](#areas)
* [Region directory, starting from the indicated region](#item)
* [Countries](#countries)

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

Example: `https://api.hh.ru/areas?locale=EN`

### Errors

* `403 Forbidden` – authorization is failed.


<a name="item"></a>
## Region directory, starting from the indicated region

`GET /areas/{area_id}` returns the region tree view list, starting from the
indicated region.

Example: `https://api.hh.ru/areas/1146?locale=EN`

### Errors

* `403 Forbidden` – authorization is failed.
* `404 Not Found` - the area is not found.


<a name="countries"></a>
## Countries

`GET /areas/countries` returns the regions list with countries.

```json
[
  {
    "url": "https://api.hh.ru/areas/113",
    "id": "113",
    "name": "Russia"
  },
  {
    "url": "https://api.hh.ru/areas/5",
    "id": "5",
    "name": "Ukraine"
  }
]
 ```
 
### Errors
 
* `403 Forbidden` – authorization is failed.
