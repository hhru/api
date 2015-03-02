# Вакансии

* [Просмотр вакансии](#item)
* [Дополнительные поля для автора вакансии](#author)
* [Отобранные вакансии](#favorited)
* [Поиск по вакансиям](#search)
* [Короткое представление вакансии](#nano)
* [Скрытые вакансии](blacklisted.md)
* [Публикация вакансий](#creation) _beta_
* [Редактирование вакансии](#edit)
* [Продление вакансии](#prolongate)

<a name="item"/>
## Просмотр вакансии

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
  "published_at": "2013-07-08T16:17:21+0400",
  "relations": [ ],
  "negotiations_url": "https://api.hh.ru/negotiations?vacancy_id=8331228",
  "suitable_resumes_url": "https://api.hh.ru/vacancies/8331228/suitable_resumes",
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
  },
  "billing_type": {
    "id": "standard",
    "name": "Стандарт"
  },
  "site": {
    "id": "hh",
    "name": "hh.ru"
  },
  "department": {
    "id": "HH-1455-TECH",
    "name": "HeadHunter::Технический департамент"
  },
  "hidden": null
}
```

При запросе с авторизацией ключ `relations` возвращает значения из справочника `vacancy_relations` в [/dictionaries](dictionaries.md).

В ключе `negotiations_url` возвращается ссылка для получения списка откликов/приглашений по данной вакансии текущего пользователя-соискателя (для других типов пользователей возвращается `null`).

На вакансии с типом `direct` нельзя откликнуться на сайте hh.ru, у этих вакансий в ключе `response_url` выдаётся URL внешнего сайта (чаще всего это сайт работодателя с формой отклика) [Подробнее в документации по откликам](negotiations.md#post_negotiation)

В ключе `contacts` содержится контактная информация. В вакансиях, где контакты не указаны, возвращается `null`. Все внутренние ключи являются строками либо null. Список телефонов может быть пустым.

В ключе `test` возвращается информация о прикрепленном тестовом задании к вакансии. В случае отсутствия теста — `null`, в противном случае объект с ключом `required`, который указывает на необходимость заполнения теста для отклика. 

------

**В данный момент отклик на вакансии с обязательным тестом через API невозможен.**

------

Возможные значения `billing_type` и `site` доступны в справочниках в [/dictionaries](dictionaries.md) (`vacancy_billing_type` и `vacancy_site` соответственно).

<a name="author"/>
## Дополнительные поля вакансии

В случае с запросом вакансии с авторизацией автора, в объекте будут выданы дополнительные поля:
```json
{
  "expires_at": "2015-01-09T17:03:35+0300",
  "response_notifications": false,
  "manager": {
    "id": "1337"
  },
  "allow_messages": true,
  "hidden": false
}
```

| ключ | json тип | описание
------ | -------- | --------
| expires_at | string | дата+время окончания публикации вакансии |
| response_notifications | boolean | уведомлять ли менеджера о новых откликах |
| allow_messages | boolean | включена ли возможность соискателю писать сообщения после приглашения |
| hidden | boolean | удалена ли вакансия (скрыта из архива)

В объекте `manager` — информация о менеджере, который разместил данную вакансию.

Также для автора вакансии в объекте `test` доступен ключ `id`, а в объекте `address` доступны:
```json
{
  "address": {
    "id": "1448", 
    "show_metro_only": false
  }
}
```
  
Подробнее об этих полях вы можете прочитать в разделе о [публикации вакансии](#creation_fields).


<a name="favorited"/>
## Отобранные вакансии

`GET /vacancies/favorited` возвращает подмножество вакансий, добавленных пользователем в отобранные. Требует авторизации, иначе вернёт `403 Forbidden`. Пейджинг работает по стандартным `page&per_page`, страницы нумеруются с нуля.

`PUT /vacancies/favorited/{vacancy_id}` добавит указанную вакансию в список. Данная операция — идемпотентная: при добавлении вакансии, которая уже есть в отобранных, вернётся также `204 No Content`, как и в случае первичного добавления. Если вакансия не найдена, то сервер вернёт `404 Not Found`, если по каким-либо причинам не хватает прав положить вакансию в избранное — `403 Forbidden`.

`DELETE /vacancies/favorited/{vacancy_id}` удалит вакансию из списка отобранных авторизованного пользователя. Операция также идемпотентна. При успешном удалении метод возвращает `204 No Content`.

<a name="search"/>
## Поиск по вакансиям

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
Если выбрана сортировка по удалённости от гео-точки `distance`, необходимо также задать её координаты `sort_point_lat`,`sort_point_lng`.

* `sort_point_lat`, `sort_point_lng` - значение гео-координат точки, по расстоянию от которой будут отсортированы вакансии. Необходимо указывать только, если `order_by` установлено в `distance`.
 
* `clusters` — возвращать ли список кластеров для данного поиска, по умолчанию: `false`. Подробнее [/docs/clusters.md](clusters.md).
 

При указании параметров пэйджинга (page, per_page) работает ограничение: общее кол-во возвращаемых вакансий не может быть больше 2000.

Если параметры переданы с ошибкой, то в ответ вернется `400 Bad request` с описанием ошибки в теле.
Неизвестные параметры и параметры с ошибкой в названии игнорируются.

В зависимости от текущей авторизации выдача может отличаться, так как для соискателей применяется фильтрация по [списку скрытых вакансий и компаний](blacklisted.md).

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
      "published_at": "2013-07-08T16:17:21+0400",
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
  "found": 13,
  "clusters": null
}
```

Пример: [https://api.hh.ru/vacancies](https://api.hh.ru/vacancies)

<a name="nano"/>
## Короткое представление вакансии

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
    "published_at": "2013-10-11T13:27:16+0400",
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
 published_at | строка | Дата и время публикации вакансии
 employer | объект | Короткое представление работодателя
 response\_letter\_required | логический | Обязательно ли заполнять сообщение при отклике
 type | объект | Тип вакансии, один из элементов `vacancy_type` в [Справочнике](dictionaries.md)
 
`url` и `alternate_url` могут принимать значение `null` в случае если подробная информация о вакансии недоступна
(например, вакансия была удалена)

<a name="creation"/>
## Публикация вакансий

`POST /vacancies`

### Внимание, beta!

------

**В данный момент api метода может незначительно изменяться.**
**Вы уже можете начинать разрабатывать ваши приложения на основе данного 
метода, однако дождитесь окончательного релиза перед использованием в production окружении.**

**На время бета версии вам необходимо добавлять к запросу специальный 
параметр `POST /vacancies?beta`.** **В противном случае вы получите 
ошибку `405 Method Not Allowed`.**

------

#### Журнал изменений

26.11.14 — изменен ключ и параметр `employer_manager` на `manager`.

------

### Общая информация

В качестве тела запроса необходимо передавать 
[json](general.md#request-body) с данными размещаемой вакансии, 
формат данных аналогичен [просмотру вакансии](#item), но также содержит 
некоторые дополнительные поля.

> В соответствии с 
[законом РФ № 1032-1 от 19.04.1991 в ред. от 02.07.2013 г.](http://hh.ru/article/13967) 
запрещено размещать информацию, ограничивающую права или устанавливающую 
преимущества для соискателей по полу, возрасту, семейному положению и другим 
обстоятельствам, не связанным с деловыми качествами работников.

* при успешной публикации будут списана соответствующая услуга.
* все вакансии проходят ручную модерацию.
* в течение нескольких минут после публикации вакансия станет доступна в поиске.

### Полезные ссылки

* [правила размещения вакансий](http://hh.ru/article/341).
* [как составить хорошее описание вакансии](http://hh.ru/article/16239).


### Результат запроса

* `204 No Content` - успешное добавление. В заголовке `Location` будет 
  содержаться ссылка на добавленную вакансию.
* `403 Forbidden` - добавление вакансий недоступно данному пользователю.
* `409 Conflict` - добавление вакансии недоступно, так как вакансия с похожими
  данными уже опубликована у данного работодателя. Если вы уверены, что 
  добавление необходимо вы можете добавить к запросу параметр 
  `POST /vacancies?ignore_duplicates=true`.
* `400 Bad Request` - ошибки при добавлении вакансии. Ошибка могут быть связаны 
  как с неверными полями, так и с недостатком купленных услуг у данного 
  работодателя, либо превышения лимитов на публикацию данного пользователя.


### Пример тела запроса

```json
{
  "description": "<p>— Eh bien, mon prince. Gênes et Lucques ne sont plus que des apanages, 
  des поместья, de la famille Buonaparte. Non, je vous préviens que si vous ne me dites pas 
  que nous avons la guerre, si vous vous permettez encore de pallier toutes les infamies, 
  toutes les atrocités de cet Antichrist (ma parole, j'y crois) — je ne vous connais plus, 
  vous n'êtes plus mon ami, vous n'êtes plus мой верный раб, comme vous dites. Ну, 
  здравствуйте, здравствуйте. Je vois que je vous fais peur, садитесь и рассказывайте.</p>",
  "schedule": {
    "id": "flyInFlyOut"
  },
  "experience": {
    "id": "moreThan6"
  },
  "employment": {
    "id": "full"
  },
  "name": "Менеджер по продажам",
  "area": {
    "id": "1"
  },
  "type": {
    "id": "open"
  },
  "employer": {
    "id": "1455"
  },
  "specializations": [
    {
      "id": "17.324"
    },
    {
      "id": "3.148",
    }
  ],
  "response_letter_required": true,
  "salary": {
    "from": 100,
    "to": 500,
    "currency": "USD"
  },
  "contacts": {
    "name": "Иванов Иван",
    "email": "i.ivanov@example.com",
    "phones": [
      {
        "country": "7",
        "city": "495",
        "number": "1234567",
        "comment": "с 10 до 20"
      }
    ]
  },
  "accept_handicapped": true,
  "code": "код-1234",
  "notify": true,
  "allow_messages": true,
  "billing_type": {
    "id": "standard"
  },
  "site": {
    "id": "hh"
  },
  "address": {
    "id": "123",
    "show_metro_only": true
  },
  "manager": {
    "id": "321"
  },
  "test": {
    "id": "42",
    "required": true
  }
}
```

<a name="creation_fields"/>
### Поля запроса

* `[]` (например, в полях специализации и контактах) обозначает, что значение данного ключа является массивом объектов.  
* `a.b` обозначает объект `a` с ключом `b` описанного типа.

Путь | json тип | Описание
---- | -------- | --------
name | string | название
description | string | описание в html, не менее 200 символов
specializations | array | список специализаций
specializations[].id | string | специализация [из справочника](specializations.md)
area.id | string | регион публикации [из справочника](areas.md)
type.id | string | тип из [справочника vacancy_type](dictionaries.md)
billing_type.id | string | биллинговый тип [из справочника vacancy_billing_type](dictionaries.md)
site.id | string | сайт для публикации [из справочника vacancy_site](dictionaries.md)
code | string | внутренний код вакансии
department.id | string | департамент [из справочника](employer_departments.md), от имени которого размещается вакансия (если данная возможность доступна для компании)
salary | object или null | зарплата 
salary.from | numeric или null | нижняя граница зарплаты
salary.to | numeric или null | верхняя граница зарплаты
salary.currency | string | код валюты из [справочника currency](dictionaries.md)
address | object или null | адрес 
address.id | string | адрес из [списка доступных адресов работодателя](employer_addresses.md)
address.show_metro_only | boolean | показывать только метро для указанного адреса
experience.id | string | требуемый опыт работы из [справочника experience](dictionaries.md)
schedule.id | string | график работы из [справочника schedule](dictionaries.md)
employment.id | string | тип занятости из [справочника employment](dictionaries.md)
contacts | object | контактная информация (для вакансий рабочих специальностей)
contacts.name | string | контактное лицо
contacts.email | string | email
contacts.phones | array | список телефонов для связи
contacts.phones[].country | string | код страны
contacts.phones[].city | string | код города
contacts.phones[].number | string | телефон
contacts.phones[].comment | string или null | комментарий (удобное время для звонка по этому номеру)
test | object | тест для вакансии
test.id | string | тест, который будет добавлен в вакансию
test.required | boolean | требовать прохождение теста для отклика на вакансию
response_url | string | URL отклика для прямых вакансий (`type.id=direct`)
custom_employer_name | string | название компании для анонимных вакансий (`type.id=anonymous`), например "крупный российский банк"
employer.id | string | работодатель, для которого размещается вакансия
manager.id | string | контактное лицо (менеджер) по размещаемой вакансии, по-умолчанию текущий пользователь
response_notifications | boolean | уведомлять о новых откликах
allow_messages | boolean | возможность [переписки с кандидатами](http://inboxemp.hh.ru/) по данной вакансии
response_letter_required | boolean | требовать сопроводительное письмо
accept_handicapped | boolean | указание, что вакансия доступна для соискателей с инвалидностью


<a name="edit"/>
## Редактирование вакансий

`POST /vacancies/{vacancy_id}`

Редактирование происходит по аналогии с созданием вакансии, но есть возможность передачи отдельных полей в объекте для частичного редактирования вакансии. 
Cоставные поля (например, `salary`, `contacts`, `specializations`) можно редактировать только целиком, передавая полный объект. 
К примеру, для изменения валюты необходимо передавать обе границы значений, а для изменения специализации необходимо передать полный список.

### поля доступные для редактирования

поле | описание
-----|----------
name | название 
description | описание
schedule | график работы
experience | требуемый опыт работы
employment | тип занятости
specializations | список специализаций
salary | зарплата
address | адрес
test | тестовое задание
department | департамент 
code | внутренний код вакансии
response_letter_required | необходимость сопроводительного письма при отклике
accept_handicapped | указание, что вакансия доступна для соискателей с инвалидностью
response_notifications | настройка уведомления о новых откликах
allow_messages | возможность переписки с кандидатами по данной вакансии
contacts | контактная информация (для вакансий рабочих специальностей)
custom_employer_name | название компании для анонимных вакансий 
response_url | URL отклика для прямых вакансий

Остальные поля доступны только для чтения, либо их можно задать только при создании вакансии.

<a name="edit_more"/>
# Смена биллинг-типа, менеджера вакансии

Изменение биллингового типа вакансии, а также передача вакансии другому менеджеру компании происходит по аналогии с редактированием `POST /vacancies/{vacancy_id}`.
Единственная особенность — эти поля (`billing_type` и `manager`) необходимо отправлять отдельно от остальных полей вакансии.

```
POST /vacancies/{vacancy_id}
{"billing_type":{"id":"premium"}
```

```
POST /vacancies/{vacancy_id}
{"manager":{"id":"1337"}
```

При передачи этих полей вместе с любыми другими вернется ошибка.


<a name="prolongate"/>
## Продление вакансий

**Продление вакансии по стоимости приравнивается к новой публикации**

Для продления публикации вакансии необходимо отправить запрос `POST /vacancies/{vacancy_id}/prolongate`. 

Существуют ограничения по продлению вакансии, они могут меняться, на данный момент работают следующие правила:

* стандартные вакансии можно продлевать, если с предыдущего продления прошло не менее 3 дней.
* вакансии "стандарт-плюс" возможно продлевать не ранее 5 дней до окончания публикации.
