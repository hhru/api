Специализации
=============

`GET /specializations` возвращает справочник всех профессиональных областей и специализаций.

```json
[
    {
        "name": "Спортивные клубы, фитнес, салоны красоты",
        "id": "24",
        "specializations": [
            {
                "id": "24.493",
                "name": "Парикмахер",
                "laboring": false
            }
        ]
    }
]
```

specializations[].laboring - относится ли специализация к списку рабочих специальностей

Пример: [https://api.hh.ru/specializations](https://api.hh.ru/specializations)
