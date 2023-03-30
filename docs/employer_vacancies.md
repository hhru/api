# Вакансии для работодателя

* [Варианты публикации вакансий](#available_types)
* [Публикация вакансий](#creation)
* [Условия заполнения полей при добавлении и редактировании вакансий](#conditions)
* [Редактирование вакансий](#edit)
* [Продление вакансий](#prolongate)
* [Информация о возможности продления вакансии](#prolongate-info)
* [Список опубликованных вакансий](#active)
* [Архивация вакансий](#archive)
* [Список архивных вакансий](#archived)
* [Удаление вакансий](#hide)
* [Список удаленных вакансий](#hidden)
* [Восстановление из удаленных](#restore)
* [Статистика по вакансии](#stats)
* [Просмотры вакансии](#visitors)

Смотрите также:

* [Дополнительные поля для автора вакансии при получении вакансии](vacancies.md#author)


<a name="available_types"></a>
## Варианты публикации вакансий у текущего менеджера

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/operation/get-available-vacancy-types)

<a name="creation"></a>
## Публикация вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/publish-vacancy)

<a name="conditions"></a>
## Условия заполнения полей при добавлении и редактировании вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-vacancy-conditions)

<a name="edit"></a>
## Редактирование вакансий

`PUT /vacancies/{vacancy_id}`

* `ignore_duplicates=true` - игнорировать
  [появление дубликата](#edit-ignore-duplicates), после редактирования вакансии.

Редактирование происходит по аналогии с созданием вакансии, но есть возможность
передачи отдельных полей в объекте для частичного редактирования вакансии.
Cоставные поля (например, `salary`, `contacts`, `professional_roles`) можно
редактировать только целиком, передавая полный объект. Например, для изменения
валюты в зарплате, необходимо передавать также и значения зарплаты, а
для изменения специализации необходимо передать полный список.

### Поля, доступные для редактирования

Имя | Описание
-----|----------
name | название
description | описание
key_skills | ключевые навыки
schedule | график работы
experience | требуемый опыт работы
employment | тип занятости
professional_roles | список профессиональных ролей
salary | зарплата
address | адрес
test | тестовое задание
department | департамент
code | внутренний код вакансии
response_letter_required | необходимость сопроводительного письма при отклике
accept_handicapped | указание, что вакансия доступна для соискателей с инвалидностью
accept_kids | указание, что вакансия доступна для соискателей от 14 лет
response_notifications | настройка уведомления о новых откликах
allow_messages | возможность переписки с кандидатами по данной вакансии
contacts | контактная информация
custom_employer_name | название компании для анонимных вакансий
response_url | URL отклика для прямых вакансий
accept_incomplete_resumes | разрешен ли отклик на вакансию неполным резюме
working_days | рабочие дни
working_time_intervals | временные интервалы работы
working_time_modes | режимы времени работы
accept_temporary | указание, что вакансия доступна для соискателей с временным трудоустройством
branded_template.id | <a name="branded-template-field"></a> брендированное оформление вакансии из [справочника](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/operation/get-vacancy-branded-templates-list)
languages | список языков
driver_license_types | категория водительских прав. Элемент справочника [driver_license_types](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)

Остальные поля доступны только для чтения, либо их можно задать только при создании вакансии.

### Ответ

При успешном обновлении вакансии вернется `204 No Content`.

### Ошибки

* `404 Not Found` – редактируемая вакансия не найдена.
* `403 Forbidden` – редактирование вакансий недоступно данному пользователю.
* `400 Bad Request` – ошибки в полях при редактировании вакансии.
* <a name="edit-ignore-duplicates"></a> `403 Forbidden` –
  изменение вакансии невозможно, так как после изменения, вакансия становится
  похожа на другую вакансию у данного работодателя. Если вы уверены, что
  появление дубликата необходимо, вы можете добавить к запросу параметр
  `PUT /vacancies/{vacancy_id}?ignore_duplicates=true`.

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#vacancies-create-n-edit).

<a name="edit_more"></a>
### Смена биллинг-типа, менеджера вакансии

Возможно только улучшение типа вакансии.

Изменение биллингового типа вакансии, а также передача вакансии другому
менеджеру компании происходит по аналогии с редактированием
`PUT /vacancies/{vacancy_id}`. Единственная особенность — эти поля
(`billing_type` и `manager`) необходимо отправлять отдельно от остальных полей
вакансии.

```
PUT /vacancies/{vacancy_id}
```

```json
{
    "billing_type": {
        "id": "premium"
    }
}
```

и

```
PUT /vacancies/{vacancy_id}
```

```json
{
    "manager": {
        "id": "1337"
    }
}
```

### Ответ

При успешном обновлении биллинг-типа, менеджера вакансии вернется `204 No Content`.

### Ошибки

* `404 Not Found` – редактируемая вакансия не найдена.
* `403 Forbidden` – редактирование вакансий недоступно данному пользователю.
* `403 Forbidden` – поля `billing_type` и `manager` передаются вместе с другими.

Дополнительно к HTTP коду сервер может вернуть описание [причины ошибки](errors.md#vacancies-create-n-edit).


<a name="other-actions"></a>
### Прочие действия

* [архивация](#archive)
* [удаление](#hide)
* [восстановление из удаленных](#restore)


<a name="prolongate"></a>
## Продление вакансий
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/vacancy-prolongation)

## Информация о возможности продления вакансии
> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-prolongation-vacancy-info)

<a name="active"></a>
## Список опубликованных вакансий

> > !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/get-active-vacancy-list)

<a name="archive"></a>
## Архивация вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/add-vacancy-to-archive)

<a name="archived"></a>
## Список архивных вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-hidden-vacancies)

<a name="hide"></a>
## Удаление вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/add-vacancy-to-hidden)

<a name="hidden"></a>
## Список удаленных вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-hidden-vacancies)

<a name="restore"></a>
## Восстановление из удаленных

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/restore-vacancy-from-hidden)

<a name="stats"></a>
## Статистика по вакансии

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-vacancy-stats)

<a name="visitors"></a>
## Просмотры вакансии

`GET /vacancies/{vacancy_id}/visitors`

Возвращает список резюме соискателей, просмотревших вакансию за последнюю неделю. Список отсортирован по убыванию по
дате просмотра. Если у пользователя несколько резюме, то вернется резюме с наиболее поздней датой обновления.

Параметры:

Имя | Обязательный | Описание
--- | ------------ | --------
vacancy_id | да | Идентификатор вакансии
page | нет | Номер страницы, по умолчанию: 0
per_page | нет | Количество выдаваемых элементов на страницу, по умолчанию: 20, максимальное значение: 50


### Ответ

Успешный ответ содержит код ответа `200 OK` и тело:
```json
{
  "found": 12,
  "pages": 1,
  "page": 0,
  "per_page": 20,
  "hidden_on_page": 0,
  "items": [
    {
      "id": "0123456789abcdef",
      "title": "Начинающий специалист",
      "url": "https://api.hh.ru/resumes/0123456789abcdef?topic_id=123456789",
      "first_name": "Иван",
      "last_name": "Иванов",
      "middle_name": "Иванович",
      "age": 19,
      "can_view_full_info": true,
      "alternate_url": "https://hh.ru/resume/0123456789abcdef?vacancyId=123456&t=123456789",
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
            "result": "",
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
              "name": "Интернет-компания  (поисковики, платежные системы, соц.сети, информационно-познавательные и развлекательные ресурсы, продвижение сайтов и прочее)"
            }
          ],
          "company_url": "https://hh.ru",
          "company_id": "1455",
          "employer": {
            "alternate_url": "https://hh.ru/employer/1455",
            "id": "1455",
            "logo_urls": {
              "90": "https://hh.ru/employer/logo/1455"
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
        "medium": "https://hh.ru/...",
        "small": "https://hh.ru/...",
        "id": "1337"
      },
      "owner": {
        "id": "123456",
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
      "download": {
        "pdf": {
          "url": "https://hh.ru/api_resume_converter/0123456789abcdef/ИвановИванИванович.pdf?type=pdf"
        },
        "rtf": {
          "url": "https://hh.ru/api_resume_converter/0123456789abcdef/ИвановИванИванович.rtf?type=rtf"
        }
      }
    }
  ]
}
```

где:

Имя | Тип | Описание
--- | --- | --------
found | число | Количество найденных резюме ( ≥ 0 )
pages | число | Количество страниц с резюме ( ≥ 1 )
per_page | число | Количество элементов на страницу ( > 0 )
page | число | Номер текущей страницы ( ≥ 0 )
hidden_on_page | число | Количество удалённых или скрытых соискателями резюме на странице ( ≥ 0 )

В элементе `items` содержится список [сокращенных представлений резюме](employer_resumes.md#resume-short).

Если соискатель удалил или скрыл резюме от работодателя, то в списке `items` эти резюме будут пропущены, но будут 
учитываться при пагинации (`per_page`) и в количестве найденный резюме (`found`), а поле 
`hidden_on_page` указывает на количество таких пропущенных резюме на странице.

Например

```json
{
  "found": 12,
  "pages": 2,
  "page": 0,
  "per_page": 10,
  "hidden_on_page": 5,
  "items": [
    // ...
  ]
}
```
Такой ответ говорит о том что всего найдено 12 резюме, запрашивается первая страница с `per_page=10`. 
`hidden_on_page=5` в ответе указывает на то, что в списке `items` всего 5 элементов и 5 резюме пропущено.

### Ошибки

* `400 Bad Request` - параметры переданы с ошибкой
* `404 Not Found` - вакансия, по которой запрашиваются посетители,
  не существует или недоступна текущему пользователю

