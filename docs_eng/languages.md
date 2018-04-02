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

### Errors

* `403 Forbidden` – authorization is failed.
