# Резюме

### `GET /resumes/mine` — список резюме авторизованного пользователя
Требует авторизации, в противном случае ответом будет `403 Forbidden`.
```json
{
  "found": 1,
  "per_page": 1,
  "pages": 1,
  "page": 0,
  "items": [
    {
      "title": "...",
      "id": ""
    }
  ]
}
```

### `GET /resumes/{resume_id}` — указанное резюме
```json
{
  "title": "..."
}
```
