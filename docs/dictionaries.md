# Справочники

`GET /dictionaries` возвращает объект со справочниками полей и сущностей, используемых в нашем сервисе.
Чаще всего, каждый справочник состоит из списка объектов, содержащих `id` и `name`.

Пример: [https://api.hh.ru/dictionaries](https://api.hh.ru/dictionaries)

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

## Справочники для параметров поиска резюме
* `resume_search_order` - тип сортировки резюме
* `resume_search_label` - дополнительный фильтр результата поиска резюме

## Справочники для полей вакансии
* `employment` - тип занятости
* `experience` - опыт работы
* `schedule` - график работы
* `vacancy_type` - тип вакансии
* `vacancy_label` - метки вакансии
* `vacancy_relations` - типы связи вакансии с пользователем

## Справочники для параметров поиска вакансий
* `vacancy_search_fields` - область поиска в вакансии
* `vacancy_search_order` - тип сортировки вакансии

## Справочники для параметров откликов
* `negotiations_order` - Типы порядка отображения откликов
* `negotiations_state` - Типы состояний откликов


## Остальные справочники
* `site_lang` - язык сайта
* `currency` - cправочник валют
* `employer_type` - тип работодателя
