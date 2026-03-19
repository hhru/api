# Обновления API

<details>
<summary><strong>1.13.1 (2025-04-29)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/addresses` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `GET /employers/{employer_id}/addresses/{address_id}` | Нет | • изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /negotiations` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /negotiations/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: vacancy<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /negotiations/{nid}/messages` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `POST /negotiations/{nid}/messages` | Нет | • изменены поля ответа: address<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `POST /vacancies` | Нет | • изменены поля тела запроса: fly_in_fly_out_duration<br>• изменено описание схемы тела запроса |
| `POST /vacancies/drafts` | Нет | • изменены поля тела запроса: fly_in_fly_out_duration |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: address<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • изменены поля тела запроса: fly_in_fly_out_duration |
| `GET /vacancies/favorited` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: address<br>• изменены поля ответа: metro<br>• изменены поля ответа: line_name |
| `PUT /vacancies/{vacancy_id}` | Нет | • изменены поля тела запроса: fly_in_fly_out_duration<br>• изменено описание схемы тела запроса |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: metro_stations<br>• изменены поля ответа: line_name |
| `DELETE /webhook/subscriptions/{subscription_id}` | Нет | • обновлены теги метода<br>• изменены ответы 403 |

</details>

<details>
<summary><strong>1.13.0 (2025-04-22)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/services/payable_api_actions/active` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: balance |
| `GET /message_templates/{template}` | Да ⚠️ | • изменены поля ответа: mail |
| `GET /negotiations` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: viewed_by_opponent |
| `GET /negotiations/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: viewed_by_opponent |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: viewed_by_opponent |
| `POST /resume_profile` | Да ⚠️ | • изменены поля ответа: profile |
| `GET /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля ответа: profile |
| `PUT /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля ответа: profile |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: area, education, gender |

</details>

<details>
<summary><strong>1.12.0 (2025-04-15)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/vacancies/active` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties |
| `GET /employers/{employer_id}/vacancies/archived` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties |
| `GET /employers/{employer_id}/vacancies/hidden` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: contacts_open_until_date, employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days и еще 1 |
| `GET /resumes` | Нет | • изменены параметры: education_level<br>• изменены поля ответа: items<br>• добавлены поля ответа: contacts_open_until_date, employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days и еще 1 |
| `POST /resumes` | Нет | • обновлено описание метода<br>• добавлены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours<br>• эндпоинт помечен deprecated |
| `GET /resumes/mine` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: contacts_open_until_date, employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days и еще 1 |
| `PUT /resumes/{resume_id}` | Нет | • добавлены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /vacancies/drafts` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: vacancy_properties |
| `GET /vacancies/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Нет | • изменены поля ответа: already_applied<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours<br>• изменён заголовок схемы ответа |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours<br>• изменён заголовок схемы ответа |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.11.1 (2025-04-08)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations/response` | Нет | • изменены параметры: driver_license_types, experience |
| `GET /resumes` | Нет | • изменены параметры: driver_license_types, experience |
| `POST /saved_searches/resumes` | Нет | • изменены параметры: driver_license_types, experience |

</details>

<details>
<summary><strong>1.11.0 (2025-03-26)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /negotiations` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• добавлены поля ответа: salary_range<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /negotiations/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• добавлены поля ответа: salary_range<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: vacancy<br>• добавлены поля ответа: salary_range<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `POST /vacancies` | Нет | • добавлены поля тела запроса: salary_range, show_contacts<br>• изменены поля тела запроса: salary |
| `GET /vacancies/blacklisted` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: salary_range<br>• изменены поля тела запроса: salary |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: salary_range<br>• изменены поля ответа: salary |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: salary_range<br>• изменены поля тела запроса: salary |
| `GET /vacancies/favorited` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary |
| `PUT /vacancies/{vacancy_id}` | Нет | • обновлено описание метода<br>• добавлены поля тела запроса: salary_range, show_contacts<br>• изменены поля тела запроса: salary |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Да ⚠️ | • удалены параметры: with_profile_inconsistencies<br>• удалены поля ответа: profile_inconsistencies |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: salary_range, show_contacts<br>• изменены поля ответа: salary<br>• изменены обязательные поля ответа: добавлены salary_range |
| `GET /vacancy_conditions` | Нет | • добавлены поля ответа: salary_range<br>• изменены поля ответа: salary |

</details>

<details>
<summary><strong>1.10.0 (2025-03-19)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /vacancies` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: reason |

</details>

<details>
<summary><strong>1.9.1 (2025-03-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /applicant_comments/{applicant_id}` | Нет | • добавлены поля ответа: description |
| `POST /applicant_comments/{applicant_id}` | Нет | • добавлены поля ответа: description |
| `DELETE /applicant_comments/{applicant_id}/{comment_id}` | Нет | • добавлены поля ответа: description |
| `PUT /applicant_comments/{applicant_id}/{comment_id}` | Нет | • добавлены поля ответа: description |
| `DELETE /artifacts/{id}` | Нет | • добавлены поля ответа: description |
| `PUT /artifacts/{id}` | Нет | • добавлены поля ответа: description |
| `GET /educational_institutions/{id}/faculties` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/addresses` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/addresses/{address_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/departments` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/mail_templates` | Нет | • добавлены поля ответа: description |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/manager_types` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers` | Нет | • добавлены поля ответа: description |
| `POST /employers/{employer_id}/managers` | Нет | • добавлены поля ответа: description |
| `DELETE /employers/{employer_id}/managers/{manager_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers/{manager_id}` | Нет | • добавлены поля ответа: description |
| `PUT /employers/{employer_id}/managers/{manager_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers/{manager_id}/limits/resume` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers/{manager_id}/method_access` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers/{manager_id}/negotiations_statistics` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers/{manager_id}/settings` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/managers/{manager_id}/vacancies/available_types` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/negotiations_statistics` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/services/payable_api_actions/active` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/tests` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • добавлены поля ответа: description |
| `PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • добавлены поля ответа: description |
| `DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancy_areas/active` | Нет | • добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancy_branded_templates` | Нет | • добавлены поля ответа: description |
| `GET /message_templates/{template}` | Нет | • добавлены поля ответа: description |
| `GET /metro/{city_id}` | Нет | • добавлены поля ответа: description |
| `GET /negotiations` | Нет | • добавлены поля ответа: description |
| `DELETE /negotiations/active/{nid}` | Нет | • добавлены поля ответа: description |
| `POST /negotiations/read` | Нет | • добавлены поля ответа: description |
| `GET /negotiations/response` | Нет | • добавлены поля ответа: description |
| `PUT /negotiations/{collection_name}/{nid}` | Нет | • добавлены поля ответа: description |
| `GET /negotiations/{id}` | Нет | • добавлены поля ответа: description |
| `PUT /negotiations/{id}` | Нет | • добавлены поля ответа: description |
| `POST /negotiations/{nid}/messages` | Нет | • добавлены поля ответа: description |
| `PUT /negotiations/{nid}/messages/{mid}` | Нет | • добавлены поля ответа: description |
| `GET /negotiations/{nid}/test/solution` | Нет | • добавлены поля ответа: description |
| `POST /resumes` | Нет | • добавлены поля ответа: description |
| `DELETE /resumes/{resume_id}` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: description |
| `PUT /resumes/{resume_id}` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/access_types` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/conditions` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/negotiations_history` | Нет | • добавлены поля ответа: description |
| `POST /resumes/{resume_id}/publish` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/status` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/views` | Нет | • добавлены поля ответа: description |
| `DELETE /resumes/{resume_id}/{list_type}` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/{list_type}` | Нет | • добавлены поля ответа: description |
| `POST /resumes/{resume_id}/{list_type}` | Нет | • добавлены поля ответа: description |
| `DELETE /resumes/{resume_id}/{list_type}/employer` | Нет | • добавлены поля ответа: description |
| `GET /resumes/{resume_id}/{list_type}/search` | Нет | • добавлены поля ответа: description |
| `GET /salary_statistics/paid/salary_evaluation/{area_id}` | Нет | • добавлены поля ответа: description |
| `DELETE /saved_searches/resumes/{id}` | Нет | • добавлены поля ответа: description |
| `GET /saved_searches/resumes/{id}` | Нет | • добавлены поля ответа: description |
| `PUT /saved_searches/resumes/{id}` | Нет | • добавлены поля ответа: description |
| `DELETE /saved_searches/vacancies/{id}` | Нет | • добавлены поля ответа: description |
| `GET /saved_searches/vacancies/{id}` | Нет | • добавлены поля ответа: description |
| `PUT /saved_searches/vacancies/{id}` | Нет | • добавлены поля ответа: description |
| `GET /vacancies` | Нет | • добавлены поля ответа: description |
| `DELETE /vacancies/auto_publication` | Нет | • добавлены поля ответа: description |
| `DELETE /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: description |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/drafts/{draft_id}/duplicates` | Нет | • добавлены поля ответа: description |
| `POST /vacancies/drafts/{draft_id}/publish` | Нет | • добавлены поля ответа: description |
| `DELETE /vacancies/favorited/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `PUT /vacancies/favorited/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{id}/preferred_negotiations_order` | Нет | • добавлены поля ответа: description |
| `PUT /vacancies/{id}/preferred_negotiations_order` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `PUT /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/prolongate` | Нет | • добавлены поля ответа: description |
| `POST /vacancies/{vacancy_id}/prolongate` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/stats` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/upgrades` | Нет | • добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: description |
| `DELETE /webhook/subscriptions/{subscription_id}` | Нет | • добавлены поля ответа: description |
| `PUT /webhook/subscriptions/{subscription_id}` | Нет | • добавлены поля ответа: description |

</details>

<details>
<summary><strong>1.9.0 (2025-03-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /resumes/{resume_id}/similar_vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: video_vacancy |
| `GET /vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: video_vacancy |

</details>

<details>
<summary><strong>1.8.0 (2025-02-26)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: closed_for_applicants, vacancy_properties<br>• изменены обязательные поля ответа: добавлены closed_for_applicants, vacancy_properties |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: closed_for_applicants, vacancy_properties<br>• изменены обязательные поля ответа: добавлены closed_for_applicants, vacancy_properties |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: resume<br>• изменены поля ответа: actions, photo |
| `GET /resumes` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: actions, photo |
| `GET /vacancies/{vacancy_id}/visitors` | Да ⚠️ | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.7.0 (2025-02-19)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• добавлены поля ответа: appearance<br>• изменены поля ответа: properties |
| `POST /me` | Да ⚠️ | • изменены ответы 400 |
| `GET /resumes` | Нет | • добавлены параметры: district, education_levels, last_used, last_used_timestamp, saved_search_id, search_by_vacancy_id, text.company_size, text.industry <br>изменены параметры: education_level |
| `POST /resumes` | Да ⚠️ | • изменено тело запроса<br>• изменены ответы 400 |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • изменены ответы 400 |
| `GET /vacancies` | Да ⚠️ | • изменены ответы 400 |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: vacancy_properties |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: vacancy_properties |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: vacancy_properties |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: vacancy_properties<br>• добавлены поля ответа: appearance<br>• изменены поля ответа: properties |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • изменены ответы 400 |

</details>

<details>
<summary><strong>1.6.0 (2025-02-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /vacancies` | Да ⚠️ | • изменены поля ответа: errors<br>• добавлены поля ответа: description<br>• изменены поля ответа: value |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • добавлены параметры: ignore_replacement_warning<br>• изменены поля ответа: errors<br>• добавлены поля ответа: description<br>• изменены поля ответа: value |

</details>

<details>
<summary><strong>1.5.0 (2025-02-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `DELETE /employers/blacklisted/{employer_id}` | Нет | • добавлены поля ответа: description |
| `PUT /employers/blacklisted/{employer_id}` | Нет | • добавлены поля ответа: description |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |
| `POST /employers/{employer_id}/managers` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `DELETE /employers/{employer_id}/managers/{manager_id}` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `PUT /employers/{employer_id}/managers/{manager_id}` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: negotiations_actions<br>• добавлены поля ответа: hidden<br>• изменены обязательные поля ответа: добавлены hidden |
| `GET /negotiations` | Нет | • изменены поля ответа: collections<br>• добавлены поля ответа: hidden |
| `GET /negotiations/active` | Нет | • изменены поля ответа: collections<br>• добавлены поля ответа: hidden |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: hidden<br>• изменены обязательные поля ответа: добавлены hidden |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: actions<br>• добавлены поля ответа: hidden<br>• изменены обязательные поля ответа: добавлены hidden |
| `PUT /negotiations/{nid}/messages/{mid}` | Да ⚠️ | • изменены поля ответа: description, errors<br>• добавлены поля ответа: description<br>• изменены поля ответа: value |
| `POST /resume_phone_confirm` | Да ⚠️ | • изменены ответы 400, 403 |
| `POST /resume_phone_generate_code` | Да ⚠️ | • изменены ответы 400, 403 |
| `POST /resumes` | Нет | • добавлены ответы 409 |
| `GET /resumes/{resume_id}` | Да ⚠️ | • изменены ответы 429<br>• изменены поля ответа: errors<br>• изменены поля ответа: value |
| `POST /resumes/{resume_id}/publish` | Нет | • изменены ответы 429<br>• изменены поля ответа: errors<br>• изменены поля ответа: value |
| `POST /vacancies` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |
| `DELETE /vacancies/blacklisted/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `PUT /vacancies/blacklisted/{vacancy_id}` | Нет | • добавлены поля ответа: description |
| `POST /vacancies/drafts` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |
| `PUT /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |
| `POST /webhook/subscriptions` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |
| `PUT /webhook/subscriptions/{subscription_id}` | Нет | • добавлены поля ответа: bad_argument, bad_arguments, description |

</details>

<details>
<summary><strong>1.4.0 (2025-01-29)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/managers/{manager_id}` | Нет | • добавлены ответы 403 |
| `GET /negotiations` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: source |
| `GET /negotiations/active` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: source |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: source |
| `GET /vacancies/{vacancy_id}/visitors` | Да ⚠️ | • изменены параметры: page, per_page<br>• добавлены ответы 403 |

</details>

<details>
<summary><strong>1.3.0 (2025-01-15)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /applicant_comments/{applicant_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /applicant_comments/{applicant_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /applicant_comments/{applicant_id}/{comment_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /applicant_comments/{applicant_id}/{comment_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /artifacts` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /artifacts/photo` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /artifacts/photo/conditions` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /artifacts/portfolio` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /artifacts/portfolio/conditions` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /artifacts/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /artifacts/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/blacklisted` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /employers/blacklisted/{employer_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /employers/blacklisted/{employer_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}` | Нет | • добавлены ответы 400 |
| `GET /employers/{employer_id}/addresses` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/addresses/{address_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/departments` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/mail_templates` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/manager_types` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/managers` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/managers/{manager_id}/limits/resume` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/managers/{manager_id}/method_access` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/managers/{manager_id}/negotiations_statistics` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/managers/{manager_id}/settings` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/managers/{manager_id}/vacancies/available_types` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/negotiations_statistics` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/services/payable_api_actions/active` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/tests` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/vacancies/active` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/vacancies/archived` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/vacancies/hidden` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/vacancy_areas/active` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /employers/{employer_id}/vacancy_branded_templates` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /manager_accounts/mine` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /me` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /me` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /message_templates/{template}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /negotiations` | Да ⚠️ | • изменены поля ответа: oauth_error<br>• добавлены поля ответа: description |
| `POST /negotiations` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /negotiations/active` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /negotiations/active/{nid}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /negotiations/phone_interview` | Нет | • добавлены поля ответа: description |
| `POST /negotiations/read` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items<br>• добавлены поля ответа: education_level<br>• изменены поля ответа: oauth_error |
| `PUT /negotiations/{collection_name}/{nid}` | Нет | • добавлены поля ответа: description |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: resume<br>• изменены поля ответа: oauth_error<br>• изменены поля ответа: education<br>• добавлены поля ответа: education_level |
| `POST /negotiations/{nid}/messages` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /negotiations/{nid}/messages/{mid}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /negotiations/{nid}/test/solution` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /oauth/token` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /oauth/token` | Да ⚠️ | • изменены поля ответа: oauth_error<br>• изменены поля ответа: error, error_description |
| `GET /resume_conditions` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /resume_phone_confirm` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /resume_phone_generate_code` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resume_should_send_sms` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• добавлены поля ответа: description<br>• изменены поля ответа: oauth_error<br>• добавлены поля ответа: education_level |
| `POST /resumes` | Да ⚠️ | • изменены поля тела запроса: education<br>• изменены поля ответа: oauth_error<br>• добавлены поля тела запроса: education_level |
| `GET /resumes/creation_availability` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/mine` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: oauth_error<br>• изменены поля ответа: education<br>• добавлены поля ответа: education_level |
| `DELETE /resumes/{resume_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/{resume_id}` | Да ⚠️ | • изменены поля ответа: education<br>• добавлены поля ответа: description<br>• добавлены поля ответа: education_level<br>• изменены поля ответа: oauth_error |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: education<br>• изменены поля ответа: oauth_error<br>• изменены поля тела запроса: level, primary<br>• добавлены поля тела запроса: education_level |
| `GET /resumes/{resume_id}/access_types` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/{resume_id}/conditions` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/{resume_id}/negotiations_history` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /resumes/{resume_id}/publish` | Да ⚠️ | • изменены поля ответа: oauth_error<br>• добавлены поля ответа: description |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: video_vacancy |
| `GET /resumes/{resume_id}/status` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/{resume_id}/views` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /resumes/{resume_id}/{list_type}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/{resume_id}/{list_type}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /resumes/{resume_id}/{list_type}` | Да ⚠️ | • добавлены поля ответа: description<br>• изменены поля ответа: oauth_error |
| `DELETE /resumes/{resume_id}/{list_type}/employer` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /resumes/{resume_id}/{list_type}/search` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /salary_statistics/paid/salary_evaluation/{area_id}` | Да ⚠️ | • изменены поля ответа: oauth_error<br>• изменены поля ответа: error, error_description |
| `GET /saved_searches/resumes` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /saved_searches/resumes` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /saved_searches/resumes/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /saved_searches/resumes/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /saved_searches/resumes/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /saved_searches/vacancies` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /saved_searches/vacancies` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /saved_searches/vacancies/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /saved_searches/vacancies/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /saved_searches/vacancies/{id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: video_vacancy |
| `POST /vacancies` | Да ⚠️ | • изменены ответы 400<br>• изменены поля ответа: oauth_error |
| `DELETE /vacancies/auto_publication` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/blacklisted` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /vacancies/blacklisted/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /vacancies/blacklisted/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/drafts` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /vacancies/drafts` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: oauth_error |
| `DELETE /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены ответы 404<br>• изменены поля ответа: errors<br>• изменены поля ответа: oauth_error |
| `GET /vacancies/drafts/{draft_id}/duplicates` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /vacancies/drafts/{draft_id}/publish` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/favorited` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `DELETE /vacancies/favorited/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /vacancies/favorited/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: video_vacancy<br>• добавлены поля ответа: snippet_picture_url, snippet_video_url |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: oauth_error<br>• изменены поля ответа: reason |
| `GET /vacancies/{vacancy_id}/prolongate` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /vacancies/{vacancy_id}/prolongate` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Да ⚠️ | • изменены поля ответа: already_applied<br>• изменены поля ответа: oauth_error<br>• изменены поля ответа: education<br>• добавлены поля ответа: education_level |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: video_vacancy |
| `GET /vacancies/{vacancy_id}/stats` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: oauth_error<br>• изменены поля ответа: education<br>• добавлены поля ответа: education_level |
| `GET /vacancies/{vacancy_id}/upgrades` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: education_level |
| `GET /vacancy_conditions` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `GET /webhook/subscriptions` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `POST /webhook/subscriptions` | Да ⚠️ | • изменены поля ответа: oauth_error<br>• изменены поля ответа: errors |
| `DELETE /webhook/subscriptions/{subscription_id}` | Да ⚠️ | • изменены поля ответа: oauth_error |
| `PUT /webhook/subscriptions/{subscription_id}` | Да ⚠️ | • изменены поля ответа: oauth_error<br>• изменены поля ответа: errors |

</details>