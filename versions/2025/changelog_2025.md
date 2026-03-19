# Обновления API

<details>
<summary><strong>1.27.0 (2025-12-10)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • изменены поля ответа: employment_form |
| `GET /employers/{employer_id}/vacancy_branded_templates` | Нет | • обновлено описание метода |
| `GET /vacancies` | Нет | • добавлены параметры: driver_license_types |
| `POST /vacancies/{vacancy_id}/prolongate` | Да ⚠️ | • изменены поля ответа: errors<br>• изменены поля ответа: value |

</details>

<details>
<summary><strong>1.26.2 (2025-12-03)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /suggests/resume_search_keyword` | Нет | • добавлены поля ответа: suggest_id |
| `GET /suggests/vacancy_search_keyword` | Нет | • добавлены поля ответа: suggest_id |

</details>

<details>
<summary><strong>1.26.1 (2025-11-26)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: vacancy_search_employment_form<br>• изменены обязательные поля ответа: добавлены vacancy_search_employment_form |
| `POST /employers/{employer_id}/managers` | Нет | • изменены поля тела запроса: manager_type<br>• изменены поля тела запроса: id |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: premium |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: premium |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: premium |
| `GET /vacancies` | Нет | • изменены параметры: employment_form |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: premium<br>• изменено описание схемы ответа |
| `GET /vacancy_conditions` | Нет | • добавлены поля ответа: closed_for_applicants, vacancy_properties<br>• изменены поля ответа: billing_type, type |

</details>

<details>
<summary><strong>1.26.0 (2025-11-19)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Да ⚠️ | • изменены ответы 400 |
| `GET /me` | Да ⚠️ | • добавлены поля ответа: auth_type, is_admin, is_applicant, is_application, is_employer, is_employer_integration<br>• изменены поля ответа: counters, first_name, id, last_name, linked_socials, negotiations_url, profile_videos, resumes_url и еще 1<br>• изменены обязательные поля ответа: добавлены auth_type, is_admin, is_applicant, is_application, is_employer, is_employer_integration<br>• изменено описание схемы ответа<br>• изменён заголовок схемы ответа |
| `GET /negotiations/{nid}/messages` | Нет | • добавлены параметры: page, per_page |
| `POST /resume_profile` | Нет | • изменены поля ответа: profile<br>• добавлены поля ответа: experience |
| `GET /resume_profile/{resume_id}` | Нет | • изменены поля ответа: profile<br>• добавлены поля ответа: experience |
| `PUT /resume_profile/{resume_id}` | Нет | • изменены поля ответа: profile<br>• добавлены поля ответа: experience |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • добавлены поля тела запроса: vacancy_properties<br>• изменены поля тела запроса: billing_type<br>• изменены обязательные поля тела запроса: добавлены vacancy_properties<br>• изменены поля тела запроса: id<br>• изменено описание схемы тела запроса |
| `GET /vacancies/{vacancy_id}/upgrades` | Нет | • добавлены поля ответа: error_reason<br>• изменены поля ответа: items<br>• добавлены поля ответа: appearance, vacancy_properties<br>• изменены поля ответа: vacancy_billing_type |
| `GET /vacancy_conditions` | Нет | • изменены поля ответа: fly_in_fly_out_duration, work_format, work_schedule_by_days, working_hours |

</details>

<details>
<summary><strong>1.25.2 (2025-11-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}` | Нет | • изменены поля ответа: branding<br>• изменены поля ответа: makeup |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.25.1 (2025-11-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /vacancies` | Нет | • добавлены поля тела запроса: auto_response |
| `GET /vacancies/drafts` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: auto_response |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: auto_response |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: auto_response |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: auto_response |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: auto_response |
| `PUT /vacancies/{vacancy_id}` | Нет | • добавлены поля тела запроса: auto_response |
| `GET /vacancy_conditions` | Нет | • добавлены поля ответа: auto_response |

</details>

<details>
<summary><strong>1.25.0 (2025-10-29)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: linked_socials |
| `GET /me` | Нет | • добавлены поля ответа: linked_socials<br>• изменены обязательные поля ответа: добавлены linked_socials |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: citizenship |
| `POST /resume_profile` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: citizenship |
| `GET /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: citizenship |
| `PUT /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: citizenship |
| `GET /resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: citizenship |
| `GET /suggests/area_leaves` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: parent |
| `GET /suggests/areas` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: parent |
| `POST /vacancies/drafts` | Да ⚠️ | • удалены поля тела запроса: auction |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • удалены поля ответа: auction |
| `PUT /vacancies/drafts/{draft_id}` | Да ⚠️ | • удалены поля тела запроса: auction |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.24.3 (2025-10-22)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}` | Нет | • добавлены поля ответа: country_code |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /negotiations` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /negotiations/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: vacancy<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /negotiations/{nid}/test/solution` | Нет | • изменены ответы 404 |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /vacancies/blacklisted` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /vacancies/favorited` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: employer<br>• добавлены поля ответа: country_id |

</details>

<details>
<summary><strong>1.24.2 (2025-10-15)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /areas` | Нет | • добавлены поля ответа: lat, lng |
| `GET /areas/{area_id}` | Нет | • добавлены поля ответа: lat, lng |
| `GET /clickme/statistics` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: vacancy_area_name<br>• изменены обязательные поля ответа: добавлены vacancy_area_name |
| `GET /resumes` | Нет | • добавлены ответы 429 |

</details>

<details>
<summary><strong>1.24.1 (2025-10-08)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations/response` | Нет | • добавлены поля ответа: hidden_count |

</details>

<details>
<summary><strong>1.24.0 (2025-09-24)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/services/available_publications` | Нет | • изменены поля ответа: publication_variants<br>• изменены поля ответа: appearance, available_publications_count, suitable_packages, vacancy_properties<br>• изменены поля ответа: count, invalid<br>• изменён заголовок схемы ответа |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• изменено описание схемы ответа<br>• изменены поля ответа: title |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• изменено описание схемы ответа<br>• изменены поля ответа: title |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: appearance<br>• изменено описание схемы ответа<br>• изменены поля ответа: title |
| `POST /vacancies` | Нет | • изменены поля тела запроса: billing_type, type, vacancy_properties<br>• изменены поля тела запроса: id<br>• изменено описание схемы тела запроса<br>• изменены поля тела запроса: properties<br>• изменён заголовок схемы тела запроса |
| `GET /vacancies/drafts` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• удалены поля ответа: id<br>• изменены поля ответа: appearance, properties<br>• изменено описание схемы ответа<br>• изменён заголовок схемы ответа<br>• изменены поля ответа: title |
| `POST /vacancies/drafts` | Нет | • изменены поля тела запроса: billing_type, type, vacancy_properties |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены поля ответа: billing_type, type, vacancy_properties<br>• изменены поля ответа: id<br>• изменено описание схемы ответа<br>• удалены поля ответа: id<br>• изменены поля ответа: appearance, properties<br>• изменён заголовок схемы ответа<br>• изменены поля ответа: title |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • изменены поля тела запроса: billing_type, type, vacancy_properties |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: type, vacancy_properties<br>• изменены поля ответа: appearance<br>• изменено описание схемы ответа<br>• изменены поля ответа: title |

</details>

<details>
<summary><strong>1.23.0 (2025-09-17)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/managers/{manager_id}/vacancies/available_types` | Нет | • обновлено описание метода<br>• эндпоинт помечен deprecated |
| `POST /vacancies` | Да ⚠️ | • добавлены поля тела запроса: closed_for_applicants, vacancy_properties<br>• изменены поля тела запроса: billing_type, type<br>• изменены обязательные поля тела запроса: добавлены area, description, name, professional_roles, vacancy_properties<br>• изменено описание схемы тела запроса<br>• изменён заголовок схемы тела запроса<br>• изменены поля тела запроса: id |
| `GET /vacancies/drafts` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: closed_for_applicants<br>• изменены поля ответа: publication_type, vacancy_type |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: closed_for_applicants, vacancy_properties<br>• изменены поля тела запроса: billing_type, type<br>• изменён заголовок схемы тела запроса |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: billing_type, closed_for_applicants, type<br>• изменены поля ответа: id<br>• изменено описание схемы ответа |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: closed_for_applicants, vacancy_properties<br>• изменены поля тела запроса: billing_type, type<br>• изменён заголовок схемы тела запроса |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: closed_for_applicants, type |

</details>

<details>
<summary><strong>1.22.0 (2025-09-10)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /areas` | Нет | • добавлены поля ответа: utc_offset |
| `GET /areas/{area_id}` | Нет | • добавлены поля ответа: utc_offset |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /negotiations` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• изменены поля ответа: show_contacts |
| `GET /negotiations/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• изменены поля ответа: show_contacts |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: resume, tags, vacancy<br>• изменены поля ответа: show_contacts<br>• изменены поля ответа: viewed |
| `GET /resumes` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: viewed |
| `GET /resumes/{resume_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `POST /vacancies` | Да ⚠️ | • изменены поля тела запроса: accept_kids, manager, show_contacts<br>• изменено описание схемы тела запроса |
| `GET /vacancies/blacklisted` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: accept_kids, age_restriction, manager<br>• изменено описание схемы ответа<br>• изменены поля ответа: id |
| `GET /vacancies/favorited` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: accept_kids, age_restriction, manager, show_contacts<br>• изменено описание схемы ответа<br>• изменены поля ответа: id |
| `PUT /vacancies/{vacancy_id}` | Да ⚠️ | • изменены поля тела запроса: accept_kids, show_contacts<br>• изменено описание схемы тела запроса |
| `GET /vacancies/{vacancy_id}/related_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /vacancies/{vacancy_id}/similar_vacancies` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: show_contacts |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.21.0 (2025-09-02)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /applicant_comments/{applicant_id}` | Нет | • изменены параметры: applicant_id |
| `POST /applicant_comments/{applicant_id}` | Нет | • изменены параметры: applicant_id |
| `DELETE /applicant_comments/{applicant_id}/{comment_id}` | Нет | • изменены параметры: applicant_id |
| `PUT /applicant_comments/{applicant_id}/{comment_id}` | Нет | • изменены параметры: applicant_id |
| `GET /dictionaries` | Нет | • изменены поля ответа: resume_hidden_fields |
| `GET /educational_institutions` | Нет | • изменены ответы 400 |
| `GET /employers/{employer_id}/mail_templates` | Нет | • обновлено описание метода |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Нет | • обновлено описание метода |
| `POST /employers/{employer_id}/managers` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `DELETE /employers/{employer_id}/managers/{manager_id}` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `PUT /employers/{employer_id}/managers/{manager_id}` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `GET /employers/{employer_id}/managers/{manager_id}/method_access` | Нет | • обновлено описание метода |
| `GET /employers/{employer_id}/managers/{manager_id}/negotiations_statistics` | Нет | • изменены поля ответа: manager_statistics<br>• изменены поля ответа: replied_percent |
| `GET /employers/{employer_id}/negotiations_statistics` | Нет | • изменены поля ответа: employer_statistics<br>• изменены поля ответа: replied_percent |
| `GET /negotiations` | Нет | • изменены параметры: with_generated_collections<br>• изменены поля ответа: employer_states |
| `GET /negotiations/active` | Нет | • изменены поля ответа: employer_states |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: download_with_contact<br>• изменено описание схемы ответа |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: actions, resume<br>• изменены поля ответа: actions, hidden_fields<br>• изменены поля ответа: download_with_contact<br>• изменено описание схемы ответа |
| `PUT /negotiations/{id}` | Нет | • обновлено описание метода |
| `POST /oauth/token` | Нет | • изменены ответы 400<br>• изменены поля ответа: error_description |
| `POST /resume_profile` | Нет | • изменены поля ответа: resume<br>• изменены поля ответа: hidden_fields |
| `GET /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• изменены поля ответа: hidden_fields |
| `PUT /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• изменены поля ответа: hidden_fields |
| `GET /resumes` | Нет | • обновлено описание метода<br>• изменены параметры: area, citizenship, work_ticket<br>• изменены поля ответа: items<br>• изменены поля ответа: actions, hidden_fields<br>• изменены поля ответа: download_with_contact<br>• изменено описание схемы ответа |
| `POST /resumes` | Нет | • изменены поля тела запроса: hidden_fields |
| `GET /resumes/mine` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: hidden_fields |
| `GET /resumes/{resume_id}` | Нет | • обновлено описание метода<br>• изменены поля ответа: hidden_fields |
| `PUT /resumes/{resume_id}` | Нет | • изменены поля тела запроса: hidden_fields |
| `GET /salary_statistics/paid/salary_evaluation/{area_id}` | Нет | • изменены поля ответа: error_description |
| `GET /skills` | Нет | • изменены ответы 400 |
| `POST /vacancies` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `POST /vacancies/drafts` | Да ⚠️ | • удалены поля тела запроса: side_job |
| `PUT /vacancies/drafts/{draft_id}` | Да ⚠️ | • удалены поля тела запроса: side_job |
| `PUT /vacancies/{vacancy_id}` | Нет | • изменены параметры: ignore_duplicates<br>• изменены поля ответа: errors<br>• изменены поля ответа: value |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Нет | • изменены поля ответа: already_applied<br>• изменены поля ответа: hidden_fields |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: hidden_fields |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: download_with_contact<br>• изменено описание схемы ответа |

</details>

<details>
<summary><strong>1.20.0 (2025-08-26)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `PUT /resume_profile/{resume_id}` | Да ⚠️ | • изменены обязательные поля тела запроса: удалены current_screen_id |

</details>

<details>
<summary><strong>1.19.2 (2025-08-19)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /vacancies` | Нет | • обновлено описание метода |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: auction |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: auction |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: auction |

</details>

<details>
<summary><strong>1.19.1 (2025-08-12)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}` | Нет | • изменены поля ответа: accredited_it_employer, trusted |
| `GET /employers/{employer_id}/mail_templates` | Нет | • добавлены поля ответа: editable<br>• изменены обязательные поля ответа: добавлены editable |
| `PUT /employers/{employer_id}/mail_templates/{template_id}` | Нет | • изменены поля ответа: errors |
| `GET /employers/{employer_id}/services/payable_api_actions/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: activated_at, expires_at |
| `POST /negotiations` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `POST /negotiations/phone_interview` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `PUT /negotiations/{collection_name}/{nid}` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `POST /negotiations/{nid}/messages` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: value |
| `POST /oauth/token` | Нет | • изменены поля ответа: error |
| `PUT /resumes/{resume_id}` | Нет | • изменены поля ответа: errors<br>• изменены поля ответа: pointer |
| `GET /salary_statistics/paid/salary_evaluation/{area_id}` | Нет | • обновлено описание метода<br>• изменены поля ответа: error |
| `POST /vacancies` | Нет | • добавлены поля тела запроса: age_restriction<br>• изменены поля тела запроса: accept_kids, allow_messages<br>• изменены поля ответа: errors<br>• изменено описание схемы тела запроса<br>• изменены поля ответа: pointer |
| `GET /vacancies/drafts` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: scheduled_at<br>• изменено описание схемы ответа |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: age_restriction<br>• изменены поля тела запроса: accept_kids, scheduled_at<br>• изменены поля ответа: errors<br>• изменено описание схемы тела запроса |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: age_restriction<br>• изменены поля ответа: accept_kids, allow_messages, meta_info<br>• изменено описание схемы ответа<br>• изменены поля ответа: scheduled_at |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: age_restriction<br>• изменены поля тела запроса: accept_kids, scheduled_at<br>• изменены поля ответа: errors<br>• изменено описание схемы тела запроса |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: age_restriction<br>• изменены поля ответа: accept_kids, allow_messages<br>• изменено описание схемы ответа |
| `PUT /vacancies/{vacancy_id}` | Нет | • добавлены поля тела запроса: age_restriction<br>• изменены поля тела запроса: accept_kids, allow_messages<br>• изменены поля ответа: errors<br>• изменено описание схемы тела запроса<br>• изменены поля ответа: pointer |
| `GET /vacancy_conditions` | Нет | • добавлены поля ответа: age_restriction<br>• изменены поля ответа: accept_kids |
| `POST /webhook/subscriptions` | Нет | • изменены поля ответа: errors |
| `PUT /webhook/subscriptions/{subscription_id}` | Нет | • изменены поля ответа: errors |

</details>

<details>
<summary><strong>1.19.0 (2025-08-05)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: resume_employment_form, resume_work_format<br>• изменены обязательные поля ответа: добавлены resume_employment_form, resume_work_format |
| `GET /employers/{employer_id}/managers/{manager_id}/method_access` | Нет | • обновлено описание метода |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • добавлены параметры: all_accessible, department_id, manager_ids <br>изменены параметры: manager_id |
| `GET /negotiations` | Да ⚠️ | • изменены поля ответа: items<br>• добавлены поля ответа: tags<br>• изменены поля ответа: source |
| `GET /negotiations/active` | Да ⚠️ | • изменены поля ответа: items<br>• добавлены поля ответа: tags<br>• изменены поля ответа: source |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Да ⚠️ | • добавлены поля ответа: tags<br>• изменены поля ответа: source |
| `GET /resumes` | Нет | • изменены параметры: text |
| `POST /resumes` | Нет | • изменены поля тела запроса: contact<br>• добавлены поля тела запроса: contact_value, kind, links<br>• изменены поля тела запроса: type, value |
| `GET /resumes/mine` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: contact<br>• добавлены поля ответа: contact_value, kind, links<br>• изменены поля ответа: type, value<br>• изменены обязательные поля ответа: добавлены contact_value, kind; удалены value |
| `GET /resumes/{resume_id}` | Да ⚠️ | • изменены поля ответа: contact<br>• добавлены поля ответа: contact_value, kind, links<br>• изменены поля ответа: type, value<br>• изменены обязательные поля ответа: добавлены contact_value, kind; удалены value |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: contact<br>• добавлены поля тела запроса: contact_value, kind, links<br>• изменены поля тела запроса: type, value<br>• изменены обязательные поля тела запроса: удалены preferred |
| `POST /saved_searches/resumes` | Нет | • изменены параметры: text |
| `POST /vacancies/drafts` | Нет | • добавлены поля тела запроса: side_job |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • добавлены поля тела запроса: side_job |
| `GET /vacancies/{vacancy_id}/prolongate` | Нет | • обновлено описание метода |
| `POST /vacancies/{vacancy_id}/prolongate` | Нет | • обновлено описание метода |

</details>

<details>
<summary><strong>1.18.1 (2025-07-29)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: employment_form, work_format |
| `POST /resume_profile` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: employment_form, work_format |
| `GET /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: employment_form, work_format |
| `PUT /resume_profile/{resume_id}` | Нет | • изменены поля тела запроса: resume<br>• изменены поля ответа: resume<br>• добавлены поля тела запроса: employment_form, work_format<br>• добавлены поля ответа: employment_form, work_format |
| `GET /resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, work_format |
| `POST /resumes` | Нет | • добавлены поля тела запроса: employment_form, work_format |
| `GET /resumes/mine` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, work_format |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: employment_form, work_format |
| `PUT /resumes/{resume_id}` | Нет | • добавлены поля тела запроса: employment_form, work_format |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Нет | • изменены поля ответа: already_applied<br>• добавлены поля ответа: employment_form, work_format<br>• изменён заголовок схемы ответа |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: employment_form, work_format<br>• изменён заголовок схемы ответа |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.18.0 (2025-07-22)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /dictionaries` | Нет | • добавлены поля ответа: age_restriction |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items<br>• изменены обязательные поля ответа: удалены organization |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: resume<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `POST /resume_profile` | Да ⚠️ | • изменены поля ответа: profile, resume<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `GET /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля ответа: profile, resume<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `PUT /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: profile<br>• изменены поля ответа: profile, resume<br>• изменены поля тела запроса: education<br>• изменены поля ответа: education<br>• изменены поля тела запроса: additional<br>• изменены обязательные поля ответа: удалены organization<br>• изменены обязательные поля тела запроса: удалены organization |
| `GET /resumes` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `POST /resumes` | Да ⚠️ | • изменены поля тела запроса: education<br>• изменены обязательные поля тела запроса: удалены organization |
| `GET /resumes/mine` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `GET /resumes/{resume_id}` | Да ⚠️ | • изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: education<br>• изменены поля тела запроса: additional<br>• изменены обязательные поля тела запроса: удалены organization |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Да ⚠️ | • изменены поля ответа: already_applied<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: education<br>• изменены обязательные поля ответа: удалены organization |
| `GET /vacancies/{vacancy_id}/visitors` | Да ⚠️ | • изменены поля ответа: items<br>• изменены обязательные поля ответа: удалены organization |

</details>

<details>
<summary><strong>1.17.1 (2025-07-15)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /vacancies` | Нет | • добавлены параметры: education, employment_form, excluded_text, work_format, work_schedule_by_days, working_hours <br>изменены параметры: employment, part_time, schedule |

</details>

<details>
<summary><strong>1.17.0 (2025-07-08)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations/response` | Нет | • изменены поля ответа: items |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: resume<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `POST /resume_profile` | Да ⚠️ | • изменены поля ответа: resume<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля ответа: resume<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `PUT /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: resume<br>• изменены поля ответа: resume<br>• удалены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /resumes` | Да ⚠️ | • изменены поля ответа: items<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `POST /resumes` | Да ⚠️ | • удалены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /resumes/mine` | Да ⚠️ | • изменены поля ответа: items<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /resumes/{resume_id}` | Да ⚠️ | • удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `PUT /resumes/{resume_id}` | Да ⚠️ | • удалены поля тела запроса: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours |
| `GET /vacancies/drafts/{draft_id}` | Да ⚠️ | • изменены поля ответа: contacts<br>• изменены поля ответа: phones<br>• изменены поля ответа: formatted |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Да ⚠️ | • изменены поля ответа: already_applied<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours<br>• изменён заголовок схемы ответа |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Да ⚠️ | • изменены поля ответа: items<br>• удалены поля ответа: employment_form, fly_in_fly_out_duration, internship, night_shifts, ready_for_temporary_job, work_format, work_schedule_by_days, working_hours<br>• изменён заголовок схемы ответа |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.16.0 (2025-06-24)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: negotiations_actions<br>• добавлены поля ответа: sub_actions |
| `GET /negotiations` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: source |
| `GET /negotiations/active` | Да ⚠️ | • изменены поля ответа: items<br>• изменены поля ответа: source |
| `GET /negotiations/response` | Да ⚠️ | • изменены поля ответа: items<br>• добавлены поля ответа: sub_actions |
| `GET /negotiations/{id}` | Да ⚠️ | • изменены поля ответа: actions, resume, source<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id<br>• добавлены поля ответа: sub_actions |
| `POST /resume_profile` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `GET /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `PUT /resume_profile/{resume_id}` | Нет | • изменены поля ответа: resume<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `GET /resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `GET /resumes/mine` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `GET /resumes/{resume_id}` | Нет | • добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `POST /vacancies` | Да ⚠️ | • изменены обязательные поля тела запроса: добавлены area, description, name |
| `POST /vacancies/drafts` | Нет | • изменено описание схемы тела запроса<br>• изменён заголовок схемы тела запроса |
| `GET /vacancies/drafts/{draft_id}` | Нет | • добавлены поля ответа: closed_for_applicants |
| `PUT /vacancies/drafts/{draft_id}` | Нет | • изменено описание схемы тела запроса<br>• изменён заголовок схемы тела запроса |
| `GET /vacancies/{vacancy_id}` | Нет | • добавлены поля ответа: closed_for_applicants |
| `GET /vacancies/{vacancy_id}/prolongate` | Нет | • обновлено описание метода |
| `POST /vacancies/{vacancy_id}/prolongate` | Нет | • обновлено описание метода |
| `GET /vacancies/{vacancy_id}/resumes_by_status` | Нет | • изменены поля ответа: already_applied<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `GET /vacancies/{vacancy_id}/suitable_resumes` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: real_id<br>• изменены обязательные поля ответа: добавлены real_id |
| `GET /vacancies/{vacancy_id}/visitors` | Нет | • изменены поля ответа: items |

</details>

<details>
<summary><strong>1.15.1 (2025-06-10)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations` | Нет | • изменены поля ответа: collections<br>• добавлены поля ответа: sub_collections |
| `GET /negotiations/active` | Нет | • изменены поля ответа: collections<br>• добавлены поля ответа: sub_collections |

</details>

<details>
<summary><strong>1.15.0 (2025-06-03)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /resume_phone_generate_code` | Нет | • добавлены поля ответа: code_length |
| `POST /resume_profile` | Да ⚠️ | • изменены поля ответа: profile<br>• добавлены поля ответа: address_coordinates<br>• изменены поля ответа: area |
| `GET /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля ответа: profile<br>• добавлены поля ответа: address_coordinates<br>• изменены поля ответа: area |
| `PUT /resume_profile/{resume_id}` | Да ⚠️ | • изменены поля тела запроса: profile<br>• изменены поля ответа: profile<br>• добавлены поля тела запроса: address_coordinates<br>• добавлены поля ответа: address_coordinates<br>• изменены поля ответа: area |
| `GET /resumes/{resume_id}` | Нет | • обновлено описание метода |

</details>

<details>
<summary><strong>1.14.1 (2025-05-27)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations/response` | Нет | • обновлено описание метода |
| `PUT /negotiations/{collection_name}/{nid}` | Нет | • изменены параметры: collection_name |

</details>

<details>
<summary><strong>1.14.0 (2025-05-21)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `POST /resume_profile` | Да ⚠️ | • изменено тело запроса |
| `PUT /resume_profile/{resume_id}` | Да ⚠️ | • изменено тело запроса |
| `PUT /resumes/{resume_id}` | Нет | • обновлено описание метода<br>• эндпоинт помечен deprecated |
| `POST /webhook/subscriptions` | Нет | • обновлено описание метода |

</details>

<details>
<summary><strong>1.13.3 (2025-05-13)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /employers/{employer_id}/vacancies/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties<br>• изменено описание схемы ответа |
| `GET /employers/{employer_id}/vacancies/archived` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties<br>• изменено описание схемы ответа |
| `GET /employers/{employer_id}/vacancies/hidden` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties<br>• изменено описание схемы ответа |
| `POST /resume_profile` | Нет | • изменены поля ответа: profile<br>• добавлены поля ответа: communication_methods, other_communication_methods |
| `GET /resume_profile/dictionaries` | Нет | • добавлены поля ответа: resume_profile_communication_methods<br>• изменены обязательные поля ответа: добавлены resume_profile_communication_methods |
| `GET /resume_profile/{resume_id}` | Нет | • изменены поля ответа: profile<br>• добавлены поля ответа: communication_methods, other_communication_methods |
| `PUT /resume_profile/{resume_id}` | Нет | • изменены поля ответа: profile<br>• добавлены поля ответа: communication_methods, other_communication_methods |
| `GET /vacancies/drafts` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties<br>• изменено описание схемы ответа |
| `GET /vacancies/drafts/{draft_id}` | Нет | • изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties<br>• изменено описание схемы ответа |
| `GET /vacancies/{vacancy_id}` | Нет | • изменены поля ответа: vacancy_properties<br>• изменены поля ответа: properties<br>• изменено описание схемы ответа |

</details>

<details>
<summary><strong>1.13.2 (2025-05-06)</strong></summary>

| Эндпоинт | Breaking | Пояснение |
| --- | --- | --- |
| `GET /negotiations` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• добавлены поля ответа: show_contacts<br>• изменены обязательные поля ответа: добавлены show_contacts |
| `GET /negotiations/active` | Нет | • изменены поля ответа: items<br>• изменены поля ответа: vacancy<br>• добавлены поля ответа: show_contacts<br>• изменены обязательные поля ответа: добавлены show_contacts |
| `GET /negotiations/{id}` | Нет | • изменены поля ответа: vacancy<br>• добавлены поля ответа: show_contacts<br>• изменены обязательные поля ответа: добавлены show_contacts |
| `GET /vacancies/blacklisted` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: show_contacts |
| `GET /vacancies/favorited` | Нет | • изменены поля ответа: items<br>• добавлены поля ответа: show_contacts |

</details>

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