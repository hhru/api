# Specializations

`GET /specializations` returns a directory of all professions and specialisations.

```json
    [
        {
            "name": "Sports Clubs, Fitness Clubs, Beauty Salons",
            "id": "24",
            "specializations": [
                {
                    "id": "24.493",
                    "name": "Hair Stylist"
                }
            ]
        }
    ]
```

specializations[].laboring - is this specialist area associated with the list of blue-collar jobs

Example: [https://api.hh.ru/specializations?locale=EN](https://api.hh.ru/specializations?locale=EN)
