# Обновления API

<details>
<summary><strong>1.0.1 (2024-12-09)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: university_acronym |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: resume<br>• изменены поля ответа: education<br>• добавлены поля ответа: university_acronym |
| `GET /resumes` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• добавлены поля ответа: university_acronym |
| `POST /resumes` | Нет | • изменены поля тела запроса: education<br>• добавлены поля тела запроса: university_acronym |
| `GET /resumes/mine` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• добавлены поля ответа: university_acronym |
| `GET /resumes/{resume_id}` | Нет | • изменены поля ответа: education<br>• добавлены поля ответа: university_acronym |
| `PUT /resumes/{resume_id}` | Нет | • изменены поля тела запроса: education<br>• изменены поля тела запроса: primary<br>• добавлены поля тела запроса: university_acronym |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Нет | • изменены поля ответа: already_applied<br>• изменены поля ответа: education<br>• добавлены поля ответа: university_acronym |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• добавлены поля ответа: university_acronym |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: university_acronym |

</details>