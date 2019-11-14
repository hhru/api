# Address

Address field is used in different API responses, such as CVs, responses and
vacancy views. It can contain longitude, latitude, information regarding the
nearest metro stations and other location details. It appears as follows:

```json
{
    "city": "Moscow",
    "street": "Godovikova",
    "building": "9",
    "description": "Additional information",
    "lat": 55.807794,
    "lng": 37.638699,
    "metro_stations": [
        {
            "station_name": "station name",
            "line_name": "Line name",
            "station_id": "Station ID",
            "line_id": "Line ID",
            "lat": 55.807794,
            "lng": 37.638699
        }
    ]
}
```

where:

 Name | Type | Description
 --- | --- | ---
 city | string, null | City name
 street | string, null | Street name
 building | string, null | Building number
 description | string, null | Additional address info
 lat | number, null | Latitude
 lng | number, null | Longitude
 raw | string, null | Textual description of address
 metro_stations | array | Metro station list, may be empty, see below

The object contains key `metro` for backward compatibility.
Key `metro_stations` should be used.

## Metro

```json
{
    "id": "8.189",
    "lat": 55.745113,
    "lng": 37.864052,
    "name": "Novokosino"
}
```

where:

 Name | Type | Description
 --- | --- | ---
 id | string | Metro station ID
 lat | number, null | Latitude
 lng | number, null | Longitude
 name | string | Metro station name
