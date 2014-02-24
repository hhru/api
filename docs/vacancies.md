Вакансии
========

* [Просмотр вакансии](#Просмотр-вакансии)
* [Отобранные вакансии](#Отобранные-вакансии)
* [Поиск по вакансиям](#Поиск-по-вакансиям)
* [Короткое представление вакансии](#nano)

Просмотр вакансии
-----------------

`GET /vacancies/{vacancy_id}` вернёт подробную информацию по указанной вакансии

Пример: [https://api.hh.ru/vacancies/8252535](https://api.hh.ru/vacancies/8252535)

```json
{
  "description": "...",
  "schedule": {
    "id": "fullDay",
    "name": "Полный день"
  },
  "accept_handicapped": false,
  "experience": {
    "id": "between1And3",
    "name": "1–3 года"
  },
  "address": null,
  "alternate_url": "http://hh.ru/vacancy/8331228",
  "employment": {
    "id": "full",
    "name": "Полная занятость"
  },
  "id": "8331228",
  "salary": {
    "to": null,
    "from": 30000,
    "currency": "RUR"
  },
  "archived": false,
  "name": "Секретарь",
  "area": {
    "url": "https://api.hh.ru/areas/1",
    "id": "1",
    "name": "Москва"
  },
  "created_at": "2013-07-08T16:17:21+0400",
  "relations": [ ],
  "negotiations_url": "https://api.hh.ru/negotiations?vacancy_id=8331228",
  "employer": {
    "logo_urls": {
      "90": "http://hh.ru/employer-logo/289027.png",
      "240": "http://hh.ru/employer-logo/289169.png",
      "original": "http://hh.ru/file/2352807.png"
    },
    "name": "HeadHunter",
    "url": "https://api.hh.ru/employers/1455",
    "alternate_url": "http://hh.ru/employer/1455",
    "id": "1455",
    "trusted": true
  },
  "response_letter_required": true,
  "response_url": null,
  "type": {
    "id": "open",
    "name": "Открытая"
  },
  "test": {
    "required": false
  },
  "specializations": [
    {
      "profarea_id": "4",
      "profarea_name": "Административный персонал",
      "id": "4.255",
      "name": "Ресепшен"
    },
    {
      "profarea_id": "4",
      "profarea_name": "Административный персонал",
      "id": "4.429",
      "name": "Делопроизводство"
    },
    {
      "profarea_id": "4",
      "profarea_name": "Административный персонал",
      "id": "4.264",
      "name": "Секретарь"
    },
    {
      "profarea_id": "4",
      "profarea_name": "Административный персонал",
      "id": "4.181",
      "name": "Начальный уровень, Мало опыта"
    }
  ],
  "contacts": {
    "name": "Имя",
    "email": "user@example.com",
    "phones": [
      {
        "comment": null,
        "city": "985",
        "number": "000-00-00",
        "country": "7"
      }
    ]
  }
}
```

При запросе с авторизацией ключ `relations` возвращает значения из справочника `vacancy_relations` в [/dictionaries](dictionaries.md).

В ключе `negotiations_url` возвращается ссылка для получения списка откликов/приглашений по данной вакансии текущего пользователя-соискателя (для других типов пользователей возвращается `null`).

На вакансии с типом `direct` нельзя откликнуться на сайте hh.ru, у этих вакансий в ключе `response_url` выдаётся URL внешнего сайта (чаще всего это сайт работодателя с формой отклика) [Подробнее в документации по откликам](negotiations.md#post_negotiation)

В ключе `contacts` содержится контактная информация. В вакансиях, где контакты не указаны, возвращается `null`. Все внутренние ключи являются строками либо null. Список телефонов может быть пустым.

В ключе `test` возвращается информация о прикрепленном тестовом задании к вакансии. В случае отсутствия теста — `null`, в противном случае объект с ключом `required`, который указывает на необходимость заполнения теста для отклика. 

В данный момент отклик на вакансии с обязательным тестом через API невозможен.

Отобранные вакансии
-------------------
`GET /vacancies/favorited` возвращает подмножество вакансий, добавленных пользователем в отобранные. Требует авторизации, иначе вернёт `403 Forbidden`. Пейджинг работает по стандартным `page&per_page`, страницы нумеруются с нуля.

`PUT /vacancies/favorited/{vacancy_id}` добавит указанную вакансию в список. Данная операция — идемпотентная: при добавлении вакансии, которая уже есть в отобранных, вернётся также `204 No Content`, как и в случае первичного добавления. Если вакансия не найдена, то сервер вернёт `404 Not Found`, если по каким-либо причинам не хватает прав положить вакансию в избранное — `403 Forbidden`.

`DELETE /vacancies/favorited/{vacancy_id}` удалит вакансию из списка отобранных авторизованного пользователя. Операция также идемпотентна. При успешном удалении метод возвращает `204 No Content`.

Поиск по вакансиям
------------------

`GET /vacancies` вернёт результаты поиска вакансий.

Принимаемые параметры:

Некоторые параметры принимают множественные значения: `key=value&key=value`.

* `text` — текстовое поле.  
переданное значение ищется в полях вакансии, указанных в параметре `search_field`. Доступен язык запросов, как и на основном сайте: [http://hh.ru/article/1175](http://hh.ru/article/1175).

* `search_field` — область поиска.  
Справочник с возможными значениями: `vacancy_search_fields` в [/dictionaries](dictionaries.md).  
По умолчанию, используется все поля.  
Возможно указание нескольких значений.  

* `experience` — опыт работы.  
Справочник с возможными значениями: `experience` в [/dictionaries](dictionaries.md).  

* `employment` — тип занятости.  
Справочник с возможными значениями: `employment` в [/dictionaries](dictionaries.md).  
Возможно указание нескольких значений.  

* `schedule` — график работы.  
Справочник с возможными значениями: `schedule` в [/dictionaries](dictionaries.md).  
Возможно указание нескольких значений.  

* `area` — регион.
Справочник с возможными значениями: [/areas](areas.md).    
Возможно указание нескольких значений.  

* `metro` — ветка или станция метро.  
Справочник с возможными значениями: [/metro](metro.md).    
Возможно указание нескольких значений.  

* `specialization` — профобласть или специализация.  
Справочник с возможными значениями: [/specializations](specializations.md).    
Возможно указание нескольких значений.  
  
* `employer_id` — идентификатор [компании](employers.md).  
Возможно указание нескольких значений.  

* `currency` — код валюты.  
Справочник с возможными значениями: `currency` (ключ code) в [/dictionaries](dictionaries.md).  

* `salary` — размер заработной платы.  
Если указано это поле, но не указано `currency`, то используется значение RUR у `currency`.

* `label` — фильтр по меткам вакансий.   
Справочник с возможными значениями: `vacancy_label` в [/dictionaries](dictionaries.md).  
Возможно указание нескольких значений.  

* `only_with_salary` — показывать вакансии только с указанием зарплаты.  
Возможные значения: true или false.  
По умолчанию, используется false.  

* `period` — количество дней, в пределах которых нужно найти вакансии.  
Максимальное значение: 30.

* `top_lat`, `bottom_lat`, `left_lng`, `right_lng` — значение гео-координат.  
При поиске используется значение указанного в вакансии адреса.  
Принимаемое значение — градусы в виде десятичной дроби.  
Необходимо передавать одновременно все четыре параметра гео-координат, иначе вернется ошибка.  

* `order_by` — сортировка списка вакансий.  
Справочник с возможными значениями: `vacancy_search_order` в [/dictionaries](dictionaries.md).   

При указании параметров пэйджинга (page, per_page) работает ограничение: общее кол-во возвращаемых вакансий не может быть больше 2000.

Если параметры переданы с ошибкой, то в ответ вернется `400 Bad request` с описанием ошибки в теле.
Неизвестные параметры и параметры с ошибкой в названии игнорируются.

```json
{
  "per_page": 1,
  "items": [
    {
      "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR"
      },
      "name": "Секретарь",
      "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Москва"
      },
      "url": "https://api.hh.ru/vacancies/8331228",
      "created_at": "2013-07-08T16:17:21+0400",
      "relations": [ ],
      "employer": {
        "logo_urls": {
          "90": "http://hh.ru/employer-logo/289027.png",
          "240": "http://hh.ru/employer-logo/289169.png",
          "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "http://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "http://hh.ru/vacancy/8331228",
      "type": {
        "id": "open",
        "name": "Открытая"
      },
      "id": "8331228"
    }
  ],
  "page": 0,
  "pages": 13,
  "found": 13
}
```

Пример: [https://api.hh.ru/vacancies](https://api.hh.ru/vacancies)

<a name="nano"></a>
Короткое представление вакансии
-------------------------------
```json
{
    "id": "7760476",
    "premium": true,
    "address": null,
    "alternate_url": "http://hh.ru/vacancy/7760476",
    "salary": {
        "to": null,
        "from": 100000,
        "currency": "RUR"
    },
    "name": "Специалист по автоматизации тестирования (Java, Selenium)",
    "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Москва"
    },
    "url": "https://api.hh.ru/vacancies/7760476",
    "created_at": "2013-10-11T13:27:16+0400",
    "relations": [ ],
    "employer": {
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "http://hh.ru/employer/1455",
        "logo_urls": {
            "90": "http://hh.ru/employer-logo/289027.png",
            "240": "http://hh.ru/employer-logo/289169.png",
            "original": "http://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "id": "1455"
    },
    "response_letter_required": false,
    "type": {
        "id": "open",
        "name": "Открытая"
    }
}
```

Здесь: 

 Имя | Тип | Описание
 --- | --- | ---
 id | строка | Идентификатор вакансии
 premium | логический | Является ли премиум вакансией
 address | объект, null | [Адрес вакансии](address.md#Адрес)
 alternate_url | строка, null | Ссылка на представление вакансии на сайте
 salary | объект, null | Оклад
 name | строка | Название вакансии
 area | объект | Регион размещения вакансии
 url | строка, null | Ссылка на полное представление вакансии в api
 created_at | строка | Дата и время создания вакансии
 employer | объект | Короткое представление работодателя
 response\_letter\_required | логический | Обязательно ли заполнять сообщение при отклике
 type | объект | Тип вакансии, один из элементов `vacancy_type` в [Справочнике](dictionaries.md)
 
`url` и `alternate_url` могут принимать значение `null` в случае если подробная информация о вакансии недоступна
(например, вакансия была удалена)