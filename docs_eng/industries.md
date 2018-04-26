# Company branches

`GET /industries` returns two-level directory of all branches.

```json
[
  {
    "id": "49",
    "name": "Public Services",
    "industries": [
        {
            "id": "49.408",
            "name": "Funeral Services"
        }
    ]
  }
]
```

The directory may have other values.

Example: [https://api.hh.ru/industries?locale=EN](https://api.hh.ru/industries?locale=EN)
