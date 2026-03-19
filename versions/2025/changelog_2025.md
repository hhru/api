# Обновления API

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