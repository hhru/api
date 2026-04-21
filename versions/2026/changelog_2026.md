# Обновления API

<details>
<summary><strong>1.40.0 (2026-04-21)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: contact_view_status |
| `GET /salary_statistics/paid/salary_evaluation/{area_id}` | Да ⚠️ | • изменены поля ответа: error_description |
| `POST /token` | Да ⚠️ | • добавлены поля тела запроса: code_verifier<br>• изменены поля ответа: error_description |

</details>

<details>
<summary><strong>1.39.0 (2026-04-16)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: complaint_status<br>• изменены обязательные поля ответа: добавлены complaint_status |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: contacts<br>• изменены поля ответа: email |
| `POST /vacancies` | Нет | • изменены поля тела запроса: contacts<br>• изменены поля тела запроса: email |
| `POST /vacancies/drafts` | Нет | • изменены поля тела запроса: contacts |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены поля ответа: contacts<br>• изменены поля ответа: email<br>• изменены обязательные поля ответа: удалены email |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • изменены поля тела запроса: contacts |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: contacts<br>• изменены поля ответа: email |
| `PUT /vacancies/{vacancy_id}` | Нет | • изменены поля тела запроса: contacts<br>• изменены поля тела запроса: email |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: contacts<br>• изменены поля ответа: email |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: contacts<br>• изменены поля ответа: email |

</details>

<details>
<summary><strong>1.38.1 (2026-04-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/managers/{manager_id}` | Нет | • добавлены поля ответа: creation_time |

</details>

<details>
<summary><strong>1.38.0 (2026-04-07)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /common/chats` | Нет | • изменены поля ответа: items |
| `GET /common/chats/{chat_id}/messages` | Да ⚠️ | • изменены поля ответа: messages |

</details>

<details>
<summary><strong>1.37.1 (2026-04-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /vacancies` | Нет | • изменены поля тела запроса: description<br>• изменено описание схемы тела запроса |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: description<br>• изменено описание схемы ответа |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: description<br>• изменено описание схемы ответа |
| `PUT /vacancies/{vacancy_id}` | Нет | • изменены поля тела запроса: description<br>• изменено описание схемы тела запроса |

</details>

<details>
<summary><strong>1.37.0 (2026-03-27)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /common/chats/without_vacancy` | Нет | • добавлен новый эндпоинт |
| `GET /employers/{employer_id}/services/available_publications` | Нет | • изменены поля ответа: publication_variants<br>• изменены поля ответа: appearance, vacancy_properties |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• добавлены поля ответа: description |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• добавлены поля ответа: description |
| `GET /me` | Нет | • изменены поля ответа: user_statuses<br>• изменены поля ответа: job_search_status<br>• изменены поля ответа: last_change_time |
| `GET /vacancies/drafts` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: insufficient_publications, vacancy_properties<br>• изменены поля ответа: appearance<br>• добавлены поля ответа: description |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены поля ответа: meta_info, vacancy_properties<br>• изменены поля ответа: insufficient_publications<br>• изменены поля ответа: appearance<br>• добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• добавлены поля ответа: description |
| `GET /vacancies/{vacancy_id}/upgrades` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: required<br>• изменены обязательные поля ответа: добавлены required |

</details>

<details>
<summary><strong>1.36.0 (2026-03-19)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /applicant_comments/{applicant_id}` | Да ⚠️ | • прочие изменения |
| `POST /applicant_comments/{applicant_id}` | Да ⚠️ | • прочие изменения |
| `DELETE /applicant_comments/{applicant_id}/{comment_id}` | Да ⚠️ | • прочие изменения |
| `PUT /applicant_comments/{applicant_id}/{comment_id}` | Да ⚠️ | • прочие изменения |
| `GET /areas` | Да ⚠️ | • прочие изменения |
| `GET /areas/countries` | Да ⚠️ | • прочие изменения |
| `GET /areas/{area_id}` | Да ⚠️ | • прочие изменения |
| `GET /clickme/statistics` | Да ⚠️ | • прочие изменения |
| `GET /common/chats` | Да ⚠️ | • прочие изменения |
| `GET /common/chats/counters/unread` | Да ⚠️ | • прочие изменения |
| `GET /common/chats/files/conditions` | Да ⚠️ | • прочие изменения |
| `POST /common/chats/files/upload_links` | Да ⚠️ | • прочие изменения |
| `PUT /common/chats/{chat_id}/leave` | Да ⚠️ | • прочие изменения |
| `PUT /common/chats/{chat_id}/message/{message_id}/read` | Да ⚠️ | • прочие изменения |
| `GET /common/chats/{chat_id}/messages` | Да ⚠️ | • прочие изменения |
| `POST /common/chats/{chat_id}/messages` | Да ⚠️ | • прочие изменения |
| `DELETE /common/chats/{chat_id}/messages/{message_id}` | Да ⚠️ | • прочие изменения |
| `PUT /common/chats/{chat_id}/messages/{message_id}` | Да ⚠️ | • прочие изменения |
| `GET /common/chats/{chat_id}/participants` | Да ⚠️ | • прочие изменения |
| `PUT /common/chats/{chat_id}/participants` | Да ⚠️ | • прочие изменения |
| `PUT /common/chats/{chat_id}/write_possibility` | Да ⚠️ | • прочие изменения |
| `GET /dictionaries` | Да ⚠️ | • прочие изменения |
| `GET /districts` | Да ⚠️ | • прочие изменения |
| `GET /educational_institutions` | Да ⚠️ | • прочие изменения |
| `GET /educational_institutions/{id}/faculties` | Да ⚠️ | • прочие изменения |
| `GET /employers` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/addresses` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/addresses/{address_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/departments` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/mail_templates` | Да ⚠️ | • прочие изменения |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/manager_types` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers` | Да ⚠️ | • прочие изменения |
| `POST /employers/{employer_id}/managers` | Да ⚠️ | • прочие изменения |
| `DELETE /employers/{employer_id}/managers/{manager_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers/{manager_id}` | Да ⚠️ | • прочие изменения |
| `PUT /employers/{employer_id}/managers/{manager_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers/{manager_id}/limits/resume` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers/{manager_id}/method_access` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers/{manager_id}/negotiations_statistics` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers/{manager_id}/settings` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/managers/{manager_id}/vacancies/available_types` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/negotiations_statistics` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/services/available_publications` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/services/payable_api_actions/active` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/tests` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/vacancies/active` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/vacancies/archived` | Да ⚠️ | • прочие изменения |
| `PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/vacancies/hidden` | Да ⚠️ | • прочие изменения |
| `DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}` | Да ⚠️ | • прочие изменения |
| `PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/vacancy_areas/active` | Да ⚠️ | • прочие изменения |
| `GET /employers/{employer_id}/vacancy_branded_templates` | Да ⚠️ | • прочие изменения |
| `GET /industries` | Да ⚠️ | • прочие изменения |
| `GET /languages` | Да ⚠️ | • прочие изменения |
| `GET /locales` | Да ⚠️ | • прочие изменения |
| `GET /locales/resume` | Да ⚠️ | • прочие изменения |
| `GET /manager_accounts/mine` | Да ⚠️ | • прочие изменения |
| `GET /me` | Да ⚠️ | • прочие изменения |
| `GET /message_templates/{template}` | Да ⚠️ | • прочие изменения |
| `GET /metro` | Да ⚠️ | • прочие изменения |
| `GET /metro/{city_id}` | Да ⚠️ | • прочие изменения |
| `GET /negotiations` | Да ⚠️ | • прочие изменения |
| `POST /negotiations/phone_interview` | Да ⚠️ | • прочие изменения |
| `POST /negotiations/read` | Да ⚠️ | • прочие изменения |
| `GET /negotiations/response` | Да ⚠️ | • прочие изменения |
| `PUT /negotiations/{collection_name}/{nid}` | Да ⚠️ | • прочие изменения |
| `GET /negotiations/{id}` | Да ⚠️ | • прочие изменения |
| `PUT /negotiations/{id}` | Да ⚠️ | • прочие изменения |
| `GET /negotiations/{nid}/messages` | Да ⚠️ | • прочие изменения |
| `POST /negotiations/{nid}/messages` | Да ⚠️ | • прочие изменения |
| `GET /negotiations/{nid}/test/solution` | Да ⚠️ | • прочие изменения |
| `GET /professional_roles` | Да ⚠️ | • прочие изменения |
| `GET /resumes` | Да ⚠️ | • прочие изменения |
| `GET /resumes/{resume_id}` | Да ⚠️ | • прочие изменения |
| `GET /resumes/{resume_id}/negotiations_history` | Да ⚠️ | • прочие изменения |
| `GET /salary_statistics/dictionaries/employee_levels` | Да ⚠️ | • прочие изменения |
| `GET /salary_statistics/dictionaries/professional_areas` | Да ⚠️ | • прочие изменения |
| `GET /salary_statistics/dictionaries/salary_areas` | Да ⚠️ | • прочие изменения |
| `GET /salary_statistics/dictionaries/salary_industries` | Да ⚠️ | • прочие изменения |
| `GET /salary_statistics/paid/salary_evaluation/{area_id}` | Да ⚠️ | • изменены поля ответа: resulting_parameters<br>• изменены поля ответа: specialities |
| `GET /saved_searches/resumes` | Да ⚠️ | • прочие изменения |
| `POST /saved_searches/resumes` | Да ⚠️ | • прочие изменения |
| `DELETE /saved_searches/resumes/{id}` | Да ⚠️ | • прочие изменения |
| `GET /saved_searches/resumes/{id}` | Да ⚠️ | • прочие изменения |
| `PUT /saved_searches/resumes/{id}` | Да ⚠️ | • прочие изменения |
| `PUT /saved_searches/resumes/{saved_search_id}/managers/{manager_id}` | Да ⚠️ | • прочие изменения |
| `GET /skills` | Да ⚠️ | • прочие изменения |
| `GET /suggests/area_leaves` | Да ⚠️ | • прочие изменения |
| `GET /suggests/areas` | Да ⚠️ | • прочие изменения |
| `GET /suggests/companies` | Да ⚠️ | • прочие изменения |
| `GET /suggests/educational_institutions` | Да ⚠️ | • прочие изменения |
| `GET /suggests/fields_of_study` | Да ⚠️ | • прочие изменения |
| `GET /suggests/positions` | Да ⚠️ | • прочие изменения |
| `GET /suggests/professional_roles` | Да ⚠️ | • прочие изменения |
| `GET /suggests/resume_search_keyword` | Да ⚠️ | • прочие изменения |
| `GET /suggests/skill_set` | Да ⚠️ | • прочие изменения |
| `GET /suggests/vacancy_positions` | Да ⚠️ | • прочие изменения |
| `GET /suggests/vacancy_search_keyword` | Да ⚠️ | • прочие изменения |
| `DELETE /token` | Да ⚠️ | • прочие изменения |
| `POST /token` | Да ⚠️ | • прочие изменения |
| `GET /vacancies` | Да ⚠️ | • прочие изменения |
| `POST /vacancies` | Да ⚠️ | • прочие изменения |
| `DELETE /vacancies/auto_publication` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/drafts` | Да ⚠️ | • прочие изменения |
| `POST /vacancies/drafts` | Да ⚠️ | • прочие изменения |
| `DELETE /vacancies/drafts/{draft_id}` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • прочие изменения |
| `PUT /vacancies/drafts/{draft_id}` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/drafts/{draft_id}/duplicates` | Да ⚠️ | • прочие изменения |
| `POST /vacancies/drafts/{draft_id}/publish` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{id}/preferred_negotiations_order` | Да ⚠️ | • прочие изменения |
| `PUT /vacancies/{id}/preferred_negotiations_order` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}` | Да ⚠️ | • прочие изменения |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}/prolongate` | Да ⚠️ | • прочие изменения |
| `POST /vacancies/{vacancy_id}/prolongate` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}/stats` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}/upgrades` | Да ⚠️ | • прочие изменения |
| `GET /vacancies/{vacancy_id}/visitors` | Да ⚠️ | • прочие изменения |
| `GET /vacancy_conditions` | Да ⚠️ | • прочие изменения |
| `GET /webhook/subscriptions` | Да ⚠️ | • прочие изменения |
| `POST /webhook/subscriptions` | Да ⚠️ | • прочие изменения |
| `DELETE /webhook/subscriptions/{subscription_id}` | Да ⚠️ | • прочие изменения |
| `PUT /webhook/subscriptions/{subscription_id}` | Да ⚠️ | • прочие изменения |

</details>

<details>
<summary><strong>1.35.0 (2026-03-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `PUT /common/chats/{chat_id}/message/{message_id}/read` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `POST /common/chats/{chat_id}/messages` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `PUT /common/chats/{chat_id}/messages/{message_id}` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `PUT /common/chats/{chat_id}/write_possibility` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: reason |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • добавлены поля ответа: chat_id |

</details>

<details>
<summary><strong>1.34.1 (2026-03-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /common/chats/counters/unread` | Нет | • изменены поля ответа: unread_chats_count<br>• изменён заголовок схемы ответа |

</details>

<details>
<summary><strong>1.34.0 (2026-02-26)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /negotiations/read` | Нет | • изменено тело запроса |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • обновлено описание метода<br>• изменены поля ответа: resume<br>• добавлены поля ответа: experience_group_by_company |
| `GET /negotiations/{nid}/messages` | Нет | • обновлено описание метода |
| `POST /negotiations/{nid}/messages` | Нет | • обновлено описание метода |
| `GET /resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: experience_group_by_company |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: experience_group_by_company |
| `GET /vacancies` | Нет | • добавлены параметры: salary_frequency, salary_mode <br>изменены параметры: employment, only_with_salary, part_time, schedule |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • добавлены параметры: driver_license_types, education, employment_form, salary_frequency, salary_mode, work_format, work_schedule_by_days, working_hours <br>изменены параметры: employment, only_with_salary, part_time, schedule |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • добавлены параметры: driver_license_types, education, employment_form, salary_frequency, salary_mode, work_format, work_schedule_by_days, working_hours <br>изменены параметры: employment, only_with_salary, part_time, schedule |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |
| `GET /webhook/subscriptions` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: actions |
| `POST /webhook/subscriptions` | Да ⚠️ | • изменены поля тела запроса: actions |
| `PUT /webhook/subscriptions/{subscription_id}` | Да ⚠️ | • изменены поля тела запроса: actions |

</details>

<details>
<summary><strong>1.33.1 (2026-02-19)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /clickme/statistics` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: date_end, date_start |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: source |
| `GET /suggests/companies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: logo_urls<br>• добавлены поля ответа: 240<br>• изменены поля ответа: 90 |

</details>

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