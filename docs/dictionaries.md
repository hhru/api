# Справочники

### `GET /dictionaries` - справочники

```json
{
  "key": [
    {
      "id": "code1",
      "name": "Значение 1"
    },
    {
      "id": "code2",
      "name": "Значение 2"
    }
  ]
}
```

Где:
* `key` - один из ключей описанных ниже
* `id` - уникальный идентификатор
* `name` - значение

#### <a name="currency"/> Ключ `currency` - cправочник валют

Для справочника валют также указываются:
* `default` – валюта со значением `true` используется по-умолчанию в других запросах к API
* `name` – сокращение валюты
* `full_name` – полное название валюты
* `rate` – курс

```json
{
  "currency": [
    {
      "default": true,
      "rate": 1.0,
      "code": "RUR",
      "name": "руб.",
      "full_name": "Рубли"
    },
    {
      "default": false,
      "rate": 0.031372,
      "code": "USD",
      "name": "USD",
      "full_name": "Доллары"
    }
  ]
}
```

#### <a name="education_level"/> Ключ `education_level` - образование

#### <a name="employment"/> Ключ `employment` - тип занятости

#### <a name="experience"/> Ключ `experience` - опыт работы

#### <a name="gender"/> Ключ `gender` - пол

#### <a name="language_level"/> Ключ `language_level` - уровень владения языком

#### <a name="prefered_contact_type"/> Ключ `prefered_contact_type` - желаемый способ связи

#### <a name="relocation_type"/> Ключ `relocation_type` - готовность к переезду

#### <a name="schedule"/> Ключ `schedule` - график работы

#### <a name="site_lang"/> Ключ `site_lang` - язык сайта

#### <a name="site_type"/> Ключ `site_type` - тип сайта

#### <a name="travel_time"/> Ключ `travel_time` - время в пути

#### <a name="resume_access_type"/> Ключ `resume_access_type` - уровень доступа к резюме

#### <a name="vacancy_label"/> Ключ `vacancy_label` - пометка к вакансии

#### <a name="vacancy_search_field"/> Ключ `vacancy_search_field` - область поиска в вакансии

#### <a name="vacancy_search_order"/> Ключ `vacancy_search_order` - тип сортировки вакансии
