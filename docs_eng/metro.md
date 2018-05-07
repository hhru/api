# Metro directory

## Obtaining all metro stations of all cities

`GET /metro` will return a list of all metro stations and lines of all cities.

```json
[
  {
    "id": "1",
    "url": "https://api.hh.ru/metro/1",
    "name": "Moscow",
    "lines": [
      {
        "hex_color": "339999",
        "id": "11",
        "name": "Kakhovskaya",
        "stations": [
          {
            "id": "11.46",
            "name": "Kashirskaya",
            "lat": 55.654327,
            "lng": 37.647705,
            "order": 0
          }
        ]
      }
    ]
  }
]
```

The first level has the list of cities that have a metro. The second level has
the list of city metro lines indicated in the `lines` parameter. The third level
has metro stations of the line indicated in the `stations` parameter.

* `hex_color` is the color of the line in the HEX RRGGBB format
  (from 000000 to FFFFFF);
* `lat`, `lng` are coordinates of the station location;
* `order` is an order number of the station on its line, starting from 0.

Example: [https://api.hh.ru/metro?locale=EN](https://api.hh.ru/metro?locale=EN)


## List of metro stations and lines in a specific city

`GET /metro/{city_id}` will return the list of metro stations and lines in the
indicated city. A root element is not a list (as in the request to `/metro`),
but an object with data on the indicated city.

Example: [https://api.hh.ru/metro/1?locale=EN](https://api.hh.ru/metro/1?locale=EN)

### Errors

* `404 Not Found` - the city is not found.
