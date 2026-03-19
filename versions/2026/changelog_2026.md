# Обновления API

<details>
<summary><strong>1.33.0 (2026-02-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /negotiations/phone_interview` | Да ⚠️ | • изменены поля ответа: errors |
| `PUT /negotiations/{collection_name}/{nid}` | Да ⚠️ | • изменены поля ответа: errors |
| `POST /negotiations/{nid}/messages` | Да ⚠️ | • изменены поля ответа: errors |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены обязательные поля ответа: удалены schedule |
| `GET /vacancies/{vacancy_id}` | Да ⚠️ | • изменены обязательные поля ответа: удалены schedule |

</details>

<details>
<summary><strong>1.32.0 (2026-02-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• удалены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: address, video_vacancy<br>• удалены поля ответа: snippet_picture, snippet_picture_url, snippet_video, snippet_video_url |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• удалены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• удалены поля ответа: video_vacancy |

</details>

<details>
<summary><strong>1.31.0 (2026-01-29)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /resumes/{resume_id}` | Нет | • изменены поля ответа: negotiations_history<br>• изменены поля ответа: url |
| `GET /resumes/{resume_id}/negotiations_history` | Нет | • изменены поля ответа: vacancies<br>• изменены поля ответа: url |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: address<br>• добавлены поля ответа: can_edit<br>• изменены обязательные поля ответа: добавлены can_edit |

</details>

<details>
<summary><strong>1.30.1 (2026-01-22)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: civil_law_contracts |
| `GET /resumes` | Нет | • добавлены параметры: business_trip_readiness |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: accept_labor_contract, civil_law_contracts<br>• изменены поля ответа: accept_temporary<br>• изменено описание схемы ответа |
| `POST /vacancies` | Нет | • добавлены поля тела запроса: accept_labor_contract, civil_law_contracts<br>• изменены поля тела запроса: accept_temporary<br>• изменено описание схемы тела запроса |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: accept_labor_contract, civil_law_contracts<br>• изменены поля тела запроса: accept_temporary |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: accept_labor_contract, civil_law_contracts<br>• изменены поля ответа: accept_temporary<br>• изменено описание схемы ответа |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: accept_labor_contract, civil_law_contracts<br>• изменены поля тела запроса: accept_temporary |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: accept_labor_contract, civil_law_contracts<br>• изменены поля ответа: accept_temporary<br>• изменено описание схемы ответа |
| `PUT /vacancies/{vacancy_id}` | Нет | • добавлены поля тела запроса: accept_labor_contract, civil_law_contracts<br>• изменены поля тела запроса: accept_temporary<br>• изменено описание схемы тела запроса |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: accept_labor_contract, civil_law_contracts<br>• изменены поля ответа: accept_temporary<br>• изменено описание схемы ответа |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: accept_labor_contract, civil_law_contracts<br>• изменены поля ответа: accept_temporary<br>• изменено описание схемы ответа |
| `GET /vacancy_conditions` | Нет | • добавлены поля ответа: accept_labor_contract, civil_law_contracts<br>• изменены поля ответа: accept_temporary |

</details>

<details>
<summary><strong>1.30.0 (2026-01-15)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: salary_range_frequency, salary_range_mode |
| `POST /employers/{employer_id}/managers` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `DELETE /employers/{employer_id}/managers/{manager_id}` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `PUT /employers/{employer_id}/managers/{manager_id}` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `GET /employers/{employer_id}/managers/{manager_id}/method_access` | Нет | • обновлено описание метода |
| `GET /locales/resume` | Нет | • обновлено описание метода |
| `POST /negotiations` | Да ⚠️ | • удален эндпоинт |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • обновлено описание метода<br>• изменены поля ответа: messages_url |
| `GET /negotiations/{nid}/messages` | Нет | • обновлено описание метода |
| `POST /negotiations/{nid}/messages` | Нет | • обновлено описание метода |
| `GET /resumes` | Нет | • изменены параметры: text |
| `POST /resumes` | Да ⚠️ | • удален эндпоинт |
| `DELETE /resumes/{resume_id}` | Да ⚠️ | • удален эндпоинт |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • удален эндпоинт |
| `POST /saved_searches/resumes` | Нет | • изменены параметры: text |
| `GET /suggests/companies` | Нет | • обновлено описание метода |
| `GET /suggests/educational_institutions` | Нет | • обновлено описание метода |
| `GET /vacancies` | Нет | • изменены параметры: text |
| `POST /vacancies` | Нет | • изменены поля тела запроса: accept_kids<br>• изменено описание схемы тела запроса |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: accept_kids<br>• изменено описание схемы ответа |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: accept_kids, branded_description, employer<br>• изменено описание схемы ответа<br>• изменены поля ответа: blacklisted |
| `PUT /vacancies/{vacancy_id}` | Нет | • изменены поля тела запроса: accept_kids<br>• изменено описание схемы тела запроса |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены параметры: text |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены параметры: text |

</details>