# Поиск резюме

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Методы доступны только для работодателей и требуют наличия [платного доступа для работодателя](/docs/payable/employer_methods.md)


Смотрите также:

* [Просмотр резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#item)
  * [Платные услуги для работодателя связанные с резюме](https://github.com/hhru/api/blob/master/docs/employer_resumes.md#paid-services)

<a name="search-params"></a>
## Запрос

`GET /resumes` вернёт результаты поиска резюме.

Некоторые параметры принимают множественные значения: `key=value&key=value`.

> Внимание! Неизвестные параметры и параметры с ошибкой в названии игнорируются.

* `text` — поисковая фраза. Найдет резюме, в которых встречаются все слова
  заданной фразы. Возможно указание нескольких значений. Каждый дополнительный
  `text` уточняет поиск. В качестве поисковой фразы можно использовать
  [язык поисковых запросов](http://hh.ru/article.xml?articleId=1175).
  Специально для этого поля есть [автодополнение](suggests.md#resume-search-keyword).
  Для тонкой настройки по фразе можно использовать параметры `text.logic`,
  `text.field`, `text.period`. При использовании дополнительных `text.*` полей,
  необходимо указывать весь набор (триаду) параметров. 

* `text.logic` – описывает, как производится поиск. Справочник с возможными
  значениями: `resume_search_logic` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

* `text.field` – описывает, где должны встречаться слова из поисковой фразы
  `text`. В параметре text.field можно укзать несколько значений через запятую,
  например – `?text.field=education,keywords`. Справочник с возможными
  значениями: `resume_search_fields` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

* `text.period` – период для поиска в опыте работы. Параметр имеет смысл
  только для `text.field` равного одному из: `experience`, `experience_company`,
  `experience_position`, `experience_description`, но указывать его необходимо
  всегда  при указании других `text.*`. В этом случае он может быть пустым.

* `age_from`, `age_to` — возраст соискателя в годах, диапазон от и до. Обратите внимание, по умолчанию в выдачу добавляются так же резюме с неуказанным возрастом, для выдачи резюме только с указанным возрастом используйте специальный [label](#resume_search_label) "only_with_age"

* `area` — регион. Справочник с возможными значениями: [/areas](https://github.com/hhru/api/blob/master/docs/areas.md).
  Можно указать несколько значений. По умолчанию выбираются
  резюме, в которых соискатели живут в указанных регионах или готовы в них
  переехать, поменять это поведение можно указанием поля `relocation`.

* `relocation` — готовность к переезду. Справочник с возможными
  значениями: `resume_search_relocation` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
  Необходимо указывать вместе с параметром `area`.

* `period` — в днях, ищет резюме опубликованные за указанный период.
  Если не указан, поиск ведется без ограничений по дате публикации.

* `date_from` – дата, от которой нужно начать поиск. Значение указывается в формате
  [ISO 8601](https://github.com/hhru/api/blob/master/docs/general.md#date-format) -
  `YYYY-MM-DD` или с точность до секунды `YYYY-MM-DDThh:mm:ss±hhmm`. Нельзя передавать вместе с параметром `period`.

* `date_to` – дата, до которой нужно искать. Значение указывается в формате
  [ISO 8601](https://github.com/hhru/api/blob/master/docs/general.md#date-format) -
  `YYYY-MM-DD` или с точность до секунды `YYYY-MM-DDThh:mm:ss±hhmm`. Можно передавать только в паре
  с параметром `date_from`. Нельзя передавать вместе с параметром `period`.

* `education_level` —  уровень образования. Справочник с возможными значениями:
  `education_level` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). Если не указан, поиск
  ведется без ограничений на уровень образования.

* `employment` — тип занятости.
  Справочник с возможными значениями: `employment` в
  [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). Можно указать несколько значений.

* `experience` — опыт работы. Справочник с возможными значениями: `experience`
  в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

* `skill` - ключевые навыки. Указывается один или несколько идентификаторов
  ключевых навыков. Значения можно получить из поля `id` в
  [подсказке по ключевым навыкам](https://github.com/hhru/api/blob/master/docs/suggests.md#key-skills).

* `gender` — пол. Справочник с возможными значениями: `gender` в
  [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). По умолчанию вне зависимости от значения
  параметра будут найдены резюме, в которых пол не указан, убрать такие резюме
  можно с помощью `label=only_with_gender`.

<a name="resume_search_label"></a>
* `label` — дополнительный фильтр. Справочник с возможными значениями:
  `resume_search_label` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). Можно указать
  несколько значений.

* `language` — знание языка. Можно указать несколько значений. Задается в
  формате language.level, где:
     * `language` — значение из справочника [/languages](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-languages),
     * `level` — значение из справочника `language_level`
       [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

* `metro` — линия, либо станция метро. Справочник с возможными значениями:
  [/metro](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-metro-stations).

* `currency` — код валюты. Справочник с возможными значениями: `currency`
  (ключ code) в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

* `salary_from`, `salary_to` — диапазон желаемой заработной платы (ЗП), от и до. Обратите внимание, по умолчанию в выдачу добавляются так же резюме с неуказанной ЗП, для выдачи резюме только с указанной ЗП используйте специальный [label](#resume_search_label) "only_with_salary"

* `schedule` — график работы. Справочник с возможными значениями:
  `schedule` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). Можно указать несколько
  значений.

* `order_by` — сортировка списка резюме. Справочник с возможными значениями:
  `resume_search_order` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

* `citizenship` — страна желаемого гражданства. Возможные значения можно
  посмотреть в справочнике стран. Возможно указание нескольких значений.

* `work_ticket` — страна, в которой есть разрешение на работу. Возможные
  значения можно посмотреть в справочнике стран. Возможно указание нескольких
  значений.

* `educational_institution` – учебные заведения соискателя. В качестве
  параметров используются подсказки по названиям университетов
  [/suggests/educational_institutions](https://github.com/hhru/api/blob/master/docs/suggests.md). Возможно указание
  нескольких значений.

* `search_in_responses` — `true`: искать только по резюме, которыми соискатели
  откликались на вакансии компании текущего пользователя, `false`: искать
  по всем резюме. Если параметр не указан, по умолчанию используется поиск по
  всем резюме.

* `search_by_vacancy_id` — идентификатор вакансии. Поиск будет происходить в откликах на данную вакансию.
  
* `by_text_prefix` — `true`: включает поиск по префиксу. Для каждого параметра `text` будут находиться не только полные 
  совпадения слов, но еще и слова, начинающиеся с `text`. По умолчанию стоит значение `false`.
  
* `driver_license_types` — категории водительских прав. Справочник с возможными значениями:
  `driver_license_types` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
  
* `vacancy_id` — идентификатор вакансии для поиска похожих резюме. Необходимо передавать идентификатор активной или архивной вакансии работодателя.

* `per_page` — количество результатов на страницу (не может превышать 50).

* `page` — номер страницы.

* `professional_role` — профессиональная роль. Элемент справочника
  [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary). Можно указать несколько
  значений.

* `folder` — один или несколько идентификаторов папок с отобранными резюме.
Если данный параметр передан, поиск будет ограничен содержимым указанных папок.
Можно передавать идентификаторы нескольких папок, например: `folder=111&folder=222&folder=333`

* `include_all_folders` — признак, указывающий, нужно ли вести поиск по всем папкам с отобранными резюме.
Если у менеджера есть доступ к избранным папкам, то поиск проходит по умолчанию в избранных папках.
Если передать параметр `include_all_folders=false`, то поиск не будет ограничен папками.
Если будут переданы параметры `folder` и `include_all_folders` в одном запросе, вернется ошибка `400 Bad Request`.

* `job_search_status` — статус поиска работы. 
Справочник с возможными значениями: `job_search_status` в [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-available-user-statuses). 
Можно указать несколько значений.

При указании параметров пагинации (`page`, `per_page`) работает ограничение:
глубина возвращаемых результатов не может быть больше 2000. Например, возможен
запрос `per_page=10&page=199` (выдача с 1991 по 2000 резюме), но запрос с
`per_page=10&page=200` вернёт ошибку (выдача с 2001 до 2010 резюме).

Примеры запросов:

* `GET /resumes?text=программист` – найдет все резюме, в любом месте которого
  встречается заданное слово 'программист'.

* `GET /resumes?text=программист&text=java` – найдет резюме, в любом месте
  которого встречаются слова 'программист' и 'java'.

* `GET /resumes?text=программист%20java&text.logic=any&text.field=everywhere&text.period=all_time` –
  найдет резюме, в любом месте которого встречается любое из слов заданной
  фразы в параметре `text` ('программист' или 'java'). При использовании
  дополнительных полей, они должны быть указаны все.

* `GET /resumes?text=Headhunter&text.logic=all&text.field=experience&text.period=last_three_years` –
  найдет все резюме, в опыте работы которых за последние 3 года встречается
  'Headhunter'.

* `GET /resumes?text=менеджер%20проекта&text.logic=all&text.field=experience%2Cskills&text.period=last_year&text=ответственный&text.logic=all&text.field=everywhere&text.period=all_time` –
  найдет все резюме, в опыте работы за последний год и ключевых навыках которых
  встречаются слова 'менеджер' и 'проекта', а также слово 'ответственный'
  в любом месте резюме. Отметим, что дополнительные параметры
  `text.logic=all&text.field=experience%2Cskills&text.period=last_year`
  указаны для `text=менеджер%20проекта`, а
  `text.logic=all&text.field=everywhere&text.period=all_time` для параметра
  `text=ответственный`.
  
<a name="search-results"></a>
## Ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "found": 2099341,
    "per_page": 20,
    "page": 0,
    "pages": 250,
    "items": [
        {
            "id": "0123456789abcdef",
            "title": "Начинающий специалист",
            "url": "https://api.hh.ru/resumes/0123456789abcdef",
            "first_name": "Иван",
            "last_name": "Иванов",
            "middle_name": "Иванович",
            "can_view_full_info": true,
            "age": 19,
            "alternate_url": "http://hh.ru/resume/0123456789abcdef",
            "created_at": "2015-02-06T12:00:00+0300",
            "updated_at": "2015-04-20T16:24:15+0300",
            "area": {
                "id": "1",
                "name": "Москва",
                "url": "https://api.hh.ru/areas/1"
            },
            "certificate": [
                {
                    "achieved_at": "2015-01-01",
                    "owner": null,
                    "title": "тест",
                    "type": "custom",
                    "url": "http://example.com/"
                }
            ],
            "education": {
                "primary": [
                    {
                        "name": "Российский государственный социальный университет, Москва",
                        "name_id": "39420",
                        "organization": "Факультет информационных технологий",
                        "organization_id": null,
                        "result": "Информатика",
                        "result_id": null,
                        "year": 2012
                    }
                ]
            },
            "total_experience": {
                "months": 118
            },
            "experience": [
                {
                    "position": "пастух",
                    "start": "2010-01-01",
                    "end": null,
                    "company": "Рога и копыта",
                    "industries": [
                        {
                            "id": "51.643",
                            "name": "Благоустройство и уборка территорий и зданий"
                        },
                        {
                            "id": "29.503",
                            "name": "Земледелие, растениеводство, животноводство"
                        }
                    ],
                    "company_url": "http://example.com/",
                    "area": {
                        "id": "1",
                        "name": "Москва",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "company_id": null,
                    "employer": null
                },
                {
                    "start": "2005-01-01",
                    "end": "2009-03-01",
                    "company": "HeadHunter",
                    "area": {
                        "id": "1",
                        "name": "Москва",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "industries": [
                        {
                            "id": "7.513",
                            "name": "Интернет-компания (поисковики, платежные системы, соц.сети, информационно-познавательные и развлекательные ресурсы, продвижение сайтов и прочее)"
                        }
                    ],
                    "company_url": "http://hh.ru",
                    "company_id": "1455",
                    "employer": {
                        "alternate_url": "http://hh.ru/employer/1455",
                        "id": "1455",
                        "logo_urls": {
                            "90": "http://hh.ru/employer/logo/1455"
                        },
                        "name": "HeadHunter",
                        "url": "https://api.hh.ru/employers/1455"
                    }
                }
            ],
            "gender": {
                "id": "male",
                "name": "Мужской"
            },
            "salary": {
                "amount": 1000000,
                "currency": "RUR"
            },
            "photo": {
                "medium": "http://hh.ru/...",
                "small": "http://hh.ru/...",
                "id": "1337"
            },
            "owner": {
                "comments": {
                    "url": "https://api.hh.ru/applicant_comments/123456",
                    "counters": {
                        "total": 7
                    }
                }
            },
            "negotiations_history": {
                "url": "https://api.hh.ru/resumes/0123456789abcdef/negotiations_history"
            },
            "last_negotiation": {
                "employer_state": {
                    "id": "offer",
                    "name": "Предложение о работе"
                },
                "created_at": "2017-08-10T13:09:28+0300"
            },
            "job_search_status": {
                "id": "active_search",
                "name": "В активном поиске работы"
            }
        }
    ],
    "platform": {
      "id": "headhunter"
    }
}
```

Поля резюме аналогичны [полям при редактировании резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#resume-keys).

Контактная информация (ФИО) будет присутствовать только после [открытия контактой информации в резюме](/docs/payable/resume.md)

Для получения полной информации необходимо запросить [полное резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#item).
У соискателя запрос резюме будет отражён в истории просмотров.

Настройки вывода полей в поиске резюме на сайте не влияют на выдачу в API.

Возвращаемые результаты группируются по соискателю: один и тот же соискатель не может вернуться в выборке несколько раз. 
Если у соискателя есть несколько резюме, которые подходят под запрос, то только одно из его резюме вернется в качестве элемента в массиве `items`. 
Поле `found` содержит количество найденных соискателей. `per_page` работает по этому полю.

Резюме выводится не целиком. В объекте опыта отсутствует описание
(поле `description`), а также должность (поле `position`) доступна только в
последнем опыте. Образование выводится только основное.

Поле `job_search_status` [статус поиска работы](employer_resumes.md#job-search-status-object) можно получить, используя параметр `with_job_search_status=true`.

Дополнительно работодателю выдаются следующие поля:
* `owner.comments.url` — содержит url, GET запрос на который возвращает
[список комментариев к владельцу резюме](https://api.hh.ru/openapi/redoc#tag/Kommentarii-k-soiskatelyu/operation/get-applicant-comments-list)
* `owner.comments.counters.total` — общее количество таких комментариев
* `last_negotiation` — информация о последнем статусе в истории откликов/приглашений. Поля `employer_state` и
`created_at` аналогичны соответствующим полям в
[истории откликов/приглашений по резюме](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-resume-negotiations-history).

## Ошибки

* `400 Bad Request` — в случае ошибки в переданных полях.
* `403 Forbidden` — ошибка авторизации или отсутствие доступа у работодателя. Дополнительно к коду
   могут вернуться [причины ошибки](/docs/errors.md#ошибки-доступа-к-платному-методу).
