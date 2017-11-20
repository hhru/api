# Справочники

`GET /dictionaries` возвращает объект со справочниками полей и сущностей,
используемых в API. Обычно справочник состоит из списка объектов,
содержащих `id` и `name`.

Пример: [https://api.hh.ru/dictionaries](https://api.hh.ru/dictionaries)

<a name="resume"></a>
## Справочники для полей, используемых в резюме
* `education_level` - образование в резюме
* `gender` - пол
* `language_level` - уровень владения языком
* `preferred_contact_type` - желаемый способ связи
* `relocation_type` - готовность к переезду
* `travel_time` - время в пути
* `resume_access_type` - уровень доступа к резюме
* `business_trip_readiness` - готовность к командировкам
* `resume_contacts_site_type` - тип сайта в поле «контакты»
* `resume_status` - статус резюме
* `resume_moderation_note` — комментарий модератора
* `driver_license_types` — категории водительских прав

## Справочники для полей вакансии
* `employment` - тип занятости
* `experience` - опыт работы
* `schedule` - график работы
* `vacancy_type` - тип вакансии
* `vacancy_label` - метки вакансии
* `vacancy_relation` - типы связи вакансии с пользователем
* `vacancy_billing_type` - варианты размещения вакансии с точки зрения биллинга
* `vacancy_site` - возможные значения сайтов для размещения вакансии

## Справочники для параметров поиска вакансий
* `vacancy_search_fields` - область поиска в вакансии
* `vacancy_search_order` - тип сортировки вакансии
* `vacancy_cluster` - тип кластеров

## Справочники для сортировки вакансий работодателя
* `employer_active_vacancies_order` - тип сортировки списка опубликованных
  вакансий
* `employer_archived_vacancies_order` - тип сортировки списка архивных вакансий

<a name="negotiations"></a>
## Справочники для откликов/приглашений (переписка)
* `negotiations_order` - типы порядка отображения откликов
* `negotiations_state` - типы состояний откликов
* `messaging_status` — статус возможности отправки сообщения в переписке
* `negotiations_participant_type` – типы участников переписки

<a name="etc"></a>
## Остальные справочники
* `currency` - справочник валют
* `employer_type` - тип работодателя
* `employer_relation` — типы связи компании с пользователем
* `vacancy_not_prolonged_reason` — причины, из-за которых невозможно
  [продлить вакансию](employer_vacancies.md#prolongate-info).
* `applicant_comments_order` — типы сортировки
  [списка комментариев к соискателю](applicant_comments.md#list)
* `applicant_comment_access_type` - тип доступа для комментария к соискателю
