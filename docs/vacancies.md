# Вакансии

### `GET /vacancies` — поиск по вакансиям
Параметры:
* `text` — текстовый запрос ваканисии. Поиск происходиит по полям вакансии, указанные в `search_field`;
* `search_field` — область поиска (множественный).
  ID справочника [vacancy_search_field](dictionaries.md#vacancy_search_field).
  По умолчанию ищется во всех полях;
* `experience` — опыт работы (множественный).
  ID справочника [experience](dictionaries.md#experience). По умолчанию — 'noExperience';
* `employment` — тип занятости (множественный).
  ID справочника [employment](dictionaries.md#employment);
* `schedule` — тип графика работы (множественный).
  ID справочника [schedule](dictionaries.md#schedule);
* `area` — идентификатор региона (множественный). ID справочника [areas](areas.md);
* `metro` — идентификатор ветки или станции метро (множественный).
  ID ветки или станции метро из справочника [metro](metro.md);
* `specialization` — идентификатор профобласти или специализации(множественный).
  ID справочника [specializations](specializations.md);
* `employer_id` — идентификатор [компании](employers.md) (множественный);
* `currency` — идентификатор [валюты](dictionaries.md#currency);
* `compensation` — желаемая зарплата. Если указан `compensation`,
  а `currency` не указан, то `currency` равен 'RUR';
* `label` — фильтр по тегам вакансий (множественный). ID справочника [vacancy_label](dictionaries.md#vacancy_label);
* `clusters` — отборажать кластеры (true) или нет (false);
* `only_with_salary` — показывать вакансии только с указанием зарплаты (true или false);
* `period` — количество дней, в пределах которых нужно найти ваканции с датой публикации начиная
  с сегодняшнего дня (максимум 30);
* `left_lng` — левое значение долготы. Принимаемое значение — градусы и доли градусов.
  Имеет смысл передавать все четыре параметра гео-координат, иначе вернется ошибка.
  Область задается двумя значениями — левой верхней и правой нижней координатами;
* `top_lat` — верхнее значение широты;
* `right_lng` — правое значение долготы;
* `bottom_lat` — нижнее значение широты;
* `page` — номер страницы отображения для постраничной навигации, начиная с 0;
* `per_page` — количество элементов на странице, но не более 500.
  При этом общее количество возвращаемых вакансий не может быть дальше 2000-й;
* `order_by` — сортировка списка вакансий. ID справочника [vacancy_search_order](dictionaries.md#vacancy_search_order);

Все поля не обязательные, но часть полей имеет смысл задавать только вместе, например,
`left_lng, top_lat, right_lng, bottom_lat`.
Если параметры переданы с ошибкой, то ответ вернется с `400 Bad request`.
При положительном ответе объект с найденными вакансиями.

```json
{
    "found": 100500,
    "pages": 5025,
    "per_page": 20,
    "page": 0,
    "items":[
        {
           "id": "123",
           "name": "Заголовок вакансии",
           "area": {
              "id": "1",
              "name": "Москва"
           },
           "url": "https://api.hh.ru/vacancies/123",
           "created_at": "2013-04-02T12:28:16.199+04:00",
           "employer":{
              "id": "321",
              "name": "Название работодателя",
              "logo_urls":{
                 "90": "http://hh.ru/employer-logo/309201.png",
                 "240": "http://hh.ru/employer-logo/382058.png",
                 "original": "http://hh.ru/file/727526.gif"
              },
              "hrbrand": null,
              "url": "https://api.hh.ru/employers/321",
              "site_url": "http://hh.ru/employer/321"
           },
           "response_letter_required": false,
           "compensation": null,
           "address": null,
           "site_url": "http://hh.ru/vacancy/123",
           "type": "open"
        }
    ]
}
```


### `GET /vacancies/{vacancy_id}` — вакансия

```json
{
  "name": "Ведущий инженер в отдел главного энергетика",
  "id": "235",
  "created_at": "2003-05-14T14:53:23.000+04:00",
  "response_letter_required": false,
  "archived": true,
  "area": {
    "id": "1",
    "name": "Москва"
  },
  "url": "http://hh.ru/vacancy/235",
  "employment": {
    "id": "full",
    "name": "Полная занятость"
  },
  "schedule": {
    "id": "fullDay",
    "name": "полный день"
  },
  "experience": {
    "id": "between1And3",
    "name": "1–3 года"
  },
  "compensation": {
    "to": 400,
    "from": null,
    "currency": "USD"
  },
  "accept_handicapped": false,
  "address": {
    "building": "9с15",
    "city": "Москва",
    "street": "улица Годовикова",
    "description": "",
    "metro": {
        "line_name": "Калужско-Рижская",
        "station_id": "6.8",
        "line_id": "6",
        "lat": 55.807794,
        "station_name": "Алексеевская",
        "lng": 37.638699
    },
    "raw": "",
    "lat": 55.807434,
    "lng": 37.630346
  },
  "company": {
    "name": "Москабельмет",
    "id": "2494",
    "hrbrand": null,
    "url": "https://api.hh.ru/employers/2494",
    "site_url": "http://hh.ru/employer/2494",
    "logo_urls": {
      "90": "http://hh.ru/employer-logo/859961.jpeg",
      "240": "http://hh.ru/employer-logo/859962.jpeg",
      "original": "http://hh.ru/file/10909689.JPG"
    }
  },
  "specializations": [
    {
      "id": "361",
      "name": "Энергетик производства",
      "profarea_id": "18",
      "profarea_name": "Производство",
    }
  ],
  "description": "Требования:\r<br />\nМужчина 26-45 лет.\r<br />..."
}
```
