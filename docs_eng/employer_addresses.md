# Employer's address directory

> Attention! The values in the directories may change at any time. Do not address them directly.

Every employer can have several addresses. To learn the address list of a
particular employer, one should send the `GET` request to
`/employers/{employer_id}/addresses`.

request applies [standard pagination parameters](/docs_eng/general.md#pagination) page и per_page (per_page can't be more 5000)

In case of success, the `HTTP 200 OK` code will be returned, and the response
body will contain the company address list.

In case the current user is not allowed to view employer's addresses, the `HTTP
403 Forbidden` code will be returned.

An example of a successful response:

```json
{
    "items": [
        {
            "building": "117",
            "city": "St Petersburg",
            "street": "Nevsky pr.",
            "description": null,
            "raw": null,
            "lat": null,
            "lng": null,
            "id": "244030",
            "metro_stations": [ ]
        }, 
        {
            "building": "10",
            "city": "Moscow",
            "street": "Kozhevnikova ul.",
            "description": null,
            "raw": null,
            "lat": 35.752123,
            "lng": 30.610388,
            "id": "244029",
            "metro_stations": [
                {
                    "line_name": "Sokolnicheskaya",
                    "station_id": "1.4",
                    "line_id": "1",
                    "lat": 55.752123,
                    "station_name": "Biblioteka imeni Lenina",
                    "lng": 37.610388
                }
            ]
        }
    ],
    "found": 2,
    "page": 0,
    "pages": 1,
    "per_page": 20
}
```

The response includes [standard pagination fields](general.md#pagination)

In a successful response, the `items` field contains the company address list.
This list is similar to the [address in the vacancy](address.md).
The `id` field – address string identifier – is added to each address.
