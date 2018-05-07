# Language directory


## Obtaining available languages

`GET /languages` returns the list of all languages.

```json
[
    {
        "id": "ita",
        "name": "Italian"
    },
    {
        "id": "nld",
        "name": "Dutch"
    },
    {
        "id": "ell",
        "name": "Greek"
    }
]
```

Example: `https://api.hh.ru/languages?locale=EN`

### Errors

* `403 Forbidden` – authorization is failed.
