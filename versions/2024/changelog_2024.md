# Обновления API

<details>
<summary><strong>1.2.0 (2024-12-24)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: source |
| `GET /negotiations/active` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: source |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: source |

</details>

<details>
<summary><strong>1.1.0 (2024-12-17)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: employment_form, fly_in_fly_out_duration, work_format, work_schedule_by_days, working_hours |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `POST /vacancies` | Да ⚠️ | • добавлены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля тела запроса: employment, schedule, working_days, working_time_intervals, working_time_modes<br>• изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля тела запроса: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля тела запроса: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • добавлены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля тела запроса: employment, schedule, working_days, working_time_intervals, working_time_modes<br>• изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |
| `GET /vacancy_conditions` | Нет | • добавлены поля ответа: employment_form, fly_in_fly_out_duration, work_format, work_schedule_by_days, working_hours<br>• изменены поля ответа: employment, schedule, working_days, working_time_intervals, working_time_modes |

</details>

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