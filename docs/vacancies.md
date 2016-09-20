# Получение вакансий

* [Просмотр вакансии](#item)
* [Дополнительные поля для автора вакансии](#author)
* [Отобранные вакансии](#favorited)
* [Поиск по вакансиям](#search)
* [Поиск по вакансиям, похожим на вакансию](#similar)
* [Короткое представление вакансии](#nano)
* [Скрытые вакансии](blacklisted.md)

Смотрите также:

<a name="creation"></a>
<a name="creation-example"></a>
<a name="creation_fields"></a>
<a name="allow_messages"></a>
<a name="creation-results"></a>
<a name="conditions"></a>
<a name="edit"></a>
<a name="edit_more"></a>
<a name="other-actions"></a>
<a name="prolongate"></a>
<a name="prolongate-info"></a>
<a name="branded-template-field"></a>

* [Вакансии для работодателя](employer_vacancies.md)
  * [Публикация вакансий](employer_vacancies.md#creation)
  * [Редактирование вакансий](employer_vacancies.md#edit)
  * [Продление вакансий](employer_vacancies.md#prolongate)
  * [Удаление вакансий](employer_vacancies.md#hide)


<a name="item"></a>
## Просмотр вакансии

`GET /vacancies/{vacancy_id}` вернёт подробную информацию по указанной вакансии

Пример: [https://api.hh.ru/vacancies/8252535](https://api.hh.ru/vacancies/8252535)

```json
{
  "description": "...",
  "branded_description": "<style>...</style><div>...</div><script></script>",
  "key_skills": [
    {"name": "Прием посетителей"},
    {"name": "Первичный документооборот"}
  ],
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
  "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=8331228",
  "department": {
    "id": "HH-1455-TECH",
    "name": "HeadHunter::Технический департамент"
  },
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
  "allow_messages": true,
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

`branded_description` - строка с кодом HTML (возможно наличие `<script/>` и
`<style/>`), которая является альтернативой стандартному описанию вакансии.
HTML адаптирован для мобильных устройств и корректно отображается без поддержки
javascript. При этом:

* Контент тянется по ширине на 100% ширины контейнера, и умещается без
  прокрутки в 300px.
* Контент рассчитан на то, что он будет вставлен в обвязку, в которую входит
  название, требуемый опыт работы, регион, тип занятости и рабочего дня
  вакансии, а также ссылка на компанию, опубликовавушю вакансию.
* Изображения, которые могут встретиться в таком описании, адаптированы под
  retina дисплеи.
* Размер шрифта не меньше 12px, размер межстрочного интервала не меньше 16px.

Значение может быть null, если у вакансии отсутствует индивидуальное описание.

При запросе с авторизацией ключ `relations` возвращает значения из справочника
`vacancy_relation` в [/dictionaries](dictionaries.md).

В ключе `negotiations_url` возвращается ссылка для получения списка
откликов/приглашений по данной вакансии текущего пользователя-соискателя (для
других типов пользователей возвращается `null`).

На вакансии с типом `direct` нельзя откликнуться на сайте hh.ru, у этих вакансий
в ключе `response_url` выдаётся URL внешнего сайта (чаще всего это сайт
работодателя с формой отклика)
[Подробнее в документации по откликам](negotiations.md#post_negotiation)

В ключе `contacts` содержится контактная информация. В вакансиях, где контакты
не указаны, возвращается `null`. Все внутренние ключи являются строками либо
null. Список телефонов может быть пустым.

В ключе `test` возвращается информация о прикрепленном тестовом задании к
вакансии. В случае отсутствия теста — `null`, в противном случае объект с ключом
`required`, который указывает на необходимость заполнения теста для отклика.

------

**В данный момент отклик на вакансии с обязательным тестом через API невозможен.**

------

В ключе `key_skills` возвращается информация о ключевых навыках, заявленных в
вакансии.

Возможные значения `billing_type` и `site` доступны в справочниках в
[/dictionaries](dictionaries.md) (`vacancy_billing_type` и `vacancy_site`
соответственно).

В ключе `allow_messages` указано включена ли возможность соискателю писать
сообщения после приглашения.


<a name="author"></a>
## Дополнительные поля вакансии

В случае с запросом вакансии с авторизацией автора, в объекте будут выданы
дополнительные поля:

```json
{
  "expires_at": "2015-01-09T17:03:35+0300",
  "response_notifications": false,
  "manager": {
    "id": "1337"
  },
  "hidden": false,
  "branded_template": {
    "id": "marketing",
    "name": "Маркетинг"
  }
}
```

ключ | тип | описание
---- | --- | --------
expires_at | строка | дата и время окончания публикации вакансии
response_notifications | логический | уведомлять ли менеджера о новых откликах
hidden | логический | удалена ли вакансия (скрыта из архива)

В объекте `manager` — информация о менеджере, который разместил данную вакансию.

В объекте `branded_template` — информация об используемом в вакансии
[брендированном шаблоне](employer_vacancy_branded_templates.md).

Также для автора вакансии в объекте `test` доступен ключ `id`, а в объекте
`address` доступны:

```json
{
  "address": {
    "id": "1448",
    "show_metro_only": false
  }
}
```

Подробнее об этих полях вы можете прочитать в разделе о
[публикации вакансии](#creation_fields).

При запросе с авторизацией менеджера, имеющего доступ к откликам по вакансии,
в объекте будет выдано дополнительное поле с различными счётчиками по вакансии:

```json
{
  "counters": {
    "views": 100500,
    "responses": 5,
    "unread_responses": 3,
    "invitations": 10
  }
}
```

ключ | тип | описание
---- | --- | --------
counters.views | number | количество просмотров вакансии
counters.responses | number | количество откликов на вакансию
counters.unread_responses | number | количество непросмотренных откликов на вакансию
counters.invitations | number | количество приглашений на вакансию

<a name="favorited"></a>
## Отобранные вакансии

Данные методы требуют авторизации соискателем, иначе вернут `403 Forbidden`.

`GET /vacancies/favorited` - возвращает подмножество вакансий, добавленных
пользователем в отобранные.  Пейджинг работает по стандартным page&per_page,
страницы нумеруются с нуля.

`PUT /vacancies/favorited/{vacancy_id}` добавит указанную вакансию в список.
Данная операция — идемпотентная: при добавлении вакансии, которая уже есть в
отобранных, вернётся также `204 No Content`, как и в случае первичного
добавления. Если вакансия не найдена, то сервер вернёт `404 Not Found`, если по
каким-либо причинам не хватает прав положить вакансию в избранное —
`403 Forbidden`. Дополнительно к HTTP коду сервер может вернуть
описание [причины ошибки](errors.md#vacancies_favorited).

`DELETE /vacancies/favorited/{vacancy_id}` удалит вакансию из списка отобранных
авторизованного пользователя. Операция также идемпотентна. При успешном
удалении метод возвращает `204 No Content`.


<a name="search"></a>
## Поиск по вакансиям

`GET /vacancies` вернёт результаты поиска вакансий.

<a name="search-params"></a>
Принимаемые параметры:

Некоторые параметры принимают множественные значения: `key=value&key=value`.

* `text` — текстовое поле.  
Переданное значение ищется в полях вакансии, указанных в параметре `search_field`.  
Доступен язык запросов, как и на основном сайте: [http://hh.ru/article/1175](http://hh.ru/article/1175).  
Специально для этого поля есть [автодополнение](suggests.md#vacancy-search-keyword).

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

* <a name="field-area"></a> `area` — регион.
Справочник с возможными значениями: [/areas](areas.md).    
Возможно указание нескольких значений.  

* `metro` — ветка или станция метро.  
Справочник с возможными значениями: [/metro](metro.md).    
Возможно указание нескольких значений.  

* `specialization` — профобласть или специализация.  
Справочник с возможными значениями: [/specializations](specializations.md).    
Возможно указание нескольких значений.
  
* `industry` - индустрия компании, разместившей вакансию.
Справочник с возможными значениями: [/industries](industries.md).
Возможно указание нескольких значений.
  
* `employer_id` — идентификатор [компании](employers.md).  
Возможно указание нескольких значений.  

* `currency` — код валюты.  
Справочник с возможными значениями: `currency` (ключ code) в [/dictionaries](dictionaries.md).  
Имеет смысл указывать только совместно с параметром `salary`.

* `salary` — размер заработной платы.  
Если указано это поле, но не указано `currency`, то используется значение RUR у `currency`.  
При указании значения будут найдены вакансии, в которых вилка зарплаты близка к
указанной в запросе. При этом значения пересчитываются по текущим курсам ЦБ РФ.
Например, при указании `salary=100&currency=EUR` будут найдены вакансии, где
вилка зарплаты указана в рублях и после пересчёта в Евро близка к 100 EUR.
По-умолчанию будут также найдены вакансии, в которых вилка зарплаты не указана,
чтобы такие вакансии отфильтровать, используйте `only_with_salary=true`.

* `label` — фильтр по меткам вакансий.   
Справочник с возможными значениями: `vacancy_label` в [/dictionaries](dictionaries.md).  
Возможно указание нескольких значений.  

* `only_with_salary` — показывать вакансии только с указанием зарплаты.  
Возможные значения: true или false.  
По умолчанию, используется false.  

* `period` — количество дней, в пределах которых нужно найти вакансии.  
Максимальное значение: 30.

* `date_from` – дата, которая ограничивает снизу диапазон дат публикации
  вакансий.  
  Нельзя передавать вместе с параметром `period`.  
  Значение указывается в формате [ISO 8601](general.md#date-format) -
  `YYYY-MM-DD` или с точность до секунды `YYYY-MM-DDThh:mm:ss±hhmm`.

* `date_to` – дата, которая ограничивает сверху диапазон дат публикации
  вакансий.  
  Необходимо передавать только в паре с параметром `date_from`.  
  Нельзя передавать вместе с параметром `period`.  
  Значение указывается в формате [ISO 8601](general.md#date-format) -
  `YYYY-MM-DD` или с точность до секунды `YYYY-MM-DDThh:mm:ss±hhmm`.

* `top_lat`, `bottom_lat`, `left_lng`, `right_lng` — значение гео-координат.  
При поиске используется значение указанного в вакансии адреса.  
Принимаемое значение — градусы в виде десятичной дроби.  
Необходимо передавать одновременно все четыре параметра гео-координат, иначе вернется ошибка.  

* `order_by` — сортировка списка вакансий.  
Справочник с возможными значениями: `vacancy_search_order` в [/dictionaries](dictionaries.md).   
Если выбрана сортировка по удалённости от гео-точки `distance`, необходимо также задать её координаты `sort_point_lat`,`sort_point_lng`.

* `sort_point_lat`, `sort_point_lng` - значение гео-координат точки, по расстоянию от которой будут отсортированы вакансии. Необходимо указывать только, если `order_by` установлено в `distance`.

* `clusters` — возвращать ли список кластеров для данного поиска, по умолчанию: `false`. Подробнее [/docs/clusters.md](clusters.md).

* `per_page`, `page` — [параметры пагинации](general.md#pagination).


<a name="search-results"></a>

При указании параметров пагинации (page, per_page) работает ограничение: глубина
возвращаемых результатов не может быть больше 2000. Например, возможен запрос
`per_page=10&page=199` (выдача с 1991 по 2000 вакансию), но запрос с
`per_page=10&page=200` вернёт ошибку (выдача с 2001 до 2010 вакансию).

Если параметры переданы с ошибкой, то в ответ вернется `400 Bad request` с
описанием ошибки в теле. Неизвестные параметры и параметры с ошибкой в названии
игнорируются.

В зависимости от текущей авторизации выдача может отличаться, так как для
соискателей применяется фильтрация по
[списку скрытых вакансий и компаний](blacklisted.md).

Выдача может отличаться при выборе [различных сайтов](hosts.md) (параметр
`host`). Однако выбор регионального сайта, например `hh.kz`, не сужает выборку
до данного региона, для ограничения выборки по региону используйте параметр
[`area`](#field-area).

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
      "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=8331228",
      "department": {
        "id": "HH-1455-TECH",
        "name": "HeadHunter::Технический департамент"
      },
      "type": {
        "id": "open",
        "name": "Открытая"
      },
      "id": "8331228",
      "snippet": {
          "requirement": "Высшее образование. Опыт работы в качестве <highlighttext>секретаря</highlighttext>, офис-менеджера. Знание делопроизводства, документооборота. Коммуникативные навыки.",
          "responsibility": "Документооборот (регистрация, отправка, контроль исполнения писем, ведение протоколов, отчетность). Распределение корреспонденции. Прием и распределение телефонных звонков."
      },
    }
  ],
  "page": 0,
  "pages": 13,
  "found": 13,
  "clusters": null
}
```

Пример: [https://api.hh.ru/vacancies](https://api.hh.ru/vacancies)

Где помимо [стандартных полей вакансии](#nano) вернутся дополнительные поля:

ключ | тип | описание
---- |---- |---------
snippet | объект | Дополнительные текстовые снипеты по найденной вакансии. Если в тексте снипета встретилась поисковая фраза (параметр `text`), она будет подсвечена тегом `highlighttext`.
snippet.requirement | строка, null | Требования по вакансии, если они найдены в тексте описания.
snippet.responsibility | строка, null | Обязанности по вакансии, если они найдены в тексте описания.


<a name="similar"></a>
## Поиск по вакансиям, похожим на вакансию

### Запрос

`GET /vacancies/{vacancy_id}/similar_vacancies`

где `vacancy_id` - идентификатор вакансии.

Принимает те же параметры, что и [поиск по вакансиям](#search-params), и
возвращает результаты в том же виде, что и
[поиск по вакансиям](#search-results).

Дополнительно, если вакансия с идентификатором `vacancy_id` не существует, то в
ответ вернется `404 Not Found`.


<a name="nano"></a>
## Короткое представление вакансии

```json
{
    "id": "7760476",
    "premium": true,
    "address": null,
    "alternate_url": "http://hh.ru/vacancy/7760476",
    "apply_alternate_url": "http://hh.ru/applicant/vacancy_response?vacancyId=7760476",
    "department": {
      "id": "HH-1455-TECH",
      "name": "HeadHunter::Технический департамент"
    },
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
    },
    "archived": "false"
}
```

Здесь:

 Имя | Тип | Описание
 --- | --- | ---
 id | строка | Идентификатор вакансии
 premium | логический | Является ли премиум вакансией
 address | объект, null | [Адрес вакансии](address.md#Адрес)
 alternate_url | строка, null | Ссылка на представление вакансии на сайте
 apply_alternate_url | строка, null | Ссылка на отклик на вакансию на сайте
 department | объект, null | Департамент [из справочника](employer_departments.md), от имени которого размещается вакансия (если данная возможность доступна для компании)
 department.id | строка | ID департамента
 department.name | строка | Название департамента
 salary | объект, null | Оклад
 name | строка | Название вакансии
 area | объект | Регион размещения вакансии
 url | строка, null | Ссылка на полное представление вакансии в api
 published_at | строка | Дата и время публикации вакансии
 employer | объект | Короткое представление работодателя
 response\_letter\_required | логический | Обязательно ли заполнять сообщение при отклике
 type | объект | Тип вакансии, один из элементов `vacancy_type` в [Справочнике](dictionaries.md)
 archived | логический | Находится ли данная вакансия в архиве

`url` и `alternate_url` могут принимать значение `null` в случае, если подробная
информация о вакансии недоступна (например, вакансия была удалена).
