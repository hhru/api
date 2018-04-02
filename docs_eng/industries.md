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

### Errors

* `403 Forbidden` – authorization is failed.
