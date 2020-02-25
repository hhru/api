# Company branches

> Attention! The values in the directories may change at any time. Do not address them directly.

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

All top-level objects are considered to be industries, while objects from `industries` arrays are specialties.

The directory may have other values.

Example: [https://api.hh.ru/industries?locale=EN](https://api.hh.ru/industries?locale=EN)
