# Пользователь

### `GET /me` — текущий авторизованный пользователь

```json
{
    "first_name": "Имя",
    "last_name": "Фамилия",
    "is_admin": false,
    "is_anonymous": false,
    "is_applicant": true,
    "is_employer": false,
    "mid_name": "Отчество",
    "email": "contact@example.com",
    "employer": null
}
```

В случае отсутствия или передачи неправильной авторизации сервер ответит `403 Forbidden`.


Если текущий пользователь - работодатель, в `employer` придёт информация про компанию:

```json
{
    "first_name": "Имя",
    "last_name": "Фамилия",
    "is_admin": false,
    "is_anonymous": false,
    "is_applicant": false,
    "is_employer": true,
    "mid_name": "Отчество",
    "email": "contact@example.com",
    "employer": {
        "id": 1455,
        "name": "HeadHunter"
    }
}
```
