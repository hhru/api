# Резюме

* [Просмотр резюме](#item)
* [Короткое представление резюме](#resume-nano)
* [Сокращенное представление резюме](#resume-short)
* [Ссылки на скачивание резюме в нескольких форматах](#download-links)
* [Скрытые поля в резюме](#hidden-fields)


<a name="item"></a>
## Просмотр резюме

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Для работодателя данный метод требует наличия [платного доступа](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya/operation/get-payable-api-method-access)

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume)

<a name="resume-nano"></a>
## Короткое представление резюме

Самое короткое представление резюме:

```json
{
    "id": "502ff8b100018bddf30039ed1f63735f4dda66",
    "title": "консультант",
    "url": "https://api.hh.ru/resumes/502ff8b100018bddf30039ed1f63735f4dda66"
}
```

где:

 Имя  | Тип    | Описание
 ---- | ------ | ---
 id   | строка | Идентификатор резюме
 title | строка | Желаемая должность
 url  | строка | Ссылка на получение полной версии резюме


<a name="resume-short"></a>
## Сокращенное представление резюме

Отличается от полного представления отсутствием некоторых полей. Например, если указано более одно среднего образования - вернется только уровень образования. 

```json
{
    "id": "0123456789abcdef",
    "title": "Начинающий специалист",
    "url": "https://api.hh.ru/resumes/0123456789abcdef",
    "first_name": "Иван",
    "last_name": "Иванов",
    "middle_name": "Иванович",
    "can_view_full_info": true,
    "age": 19,
    "alternate_url": "https://hh.ru/resume/0123456789abcdef",
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
        "primary": [],
        "level": {
            "id": "secondary",
            "name": "Среднее"
        },
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
```

<a name="download-links"></a>
## Ссылки на скачивание резюме

В настоящий момент резюме доступны для скачивания в форматах PDF и RTF.
Соискатель может скачать свои резюме.  
Название скачиваемого файла может содержать имя соискателя или его желаемую должность.

### Запрос

Для скачивания резюме нужно использовать полученный из ответа API url, передавая [стандартные для API заголовки](https://api.hh.ru/openapi/redoc#section/Obshaya-informaciya/Trebovaniya-k-zaprosam).

```
GET https://....(ссылка, полученная в полной или сокращенной выдаче резюме API)
```

### Ответ

Успешный ответ приходит с кодом 200 и содержит в теле запрашиваемый файл.

### Ошибки

* `404 Not Found` - если резюме не существует или недоступно пользователю.
* `429 Too Many Requests` - если превышен лимит просмотров резюме в сутки (при авторизации работодателем).
* `403 Forbidden` - Не хватает услуг для скачивания резюме с контактами

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#resumes).

<a name="hidden-fields"></a>
## Скрытые поля в анонимном резюме

В поле `hidden_fields` содержится список скрытых соискателем полей анонимного резюме. Скрытые поля заменяются на `null`.

Скрываемые поля в зависимости от значения в поле:
* `names_and_photo` — заменяет на `null` значение полей `first_name`, `last_name`, `middle_name` и `photo`.
* `phones` — заменяет на `null` значение поля `contact[].value` с полем `contact[].type`, равным `cell`, `work` или `home`
* `email` — заменяет на `null` значение поля `contact[].value` с полем `contact[].type`, равным `email`
* `other_contacts` — заменяет на `null` значение полей `site[].url`
* `experience` — заменяет на `null` поля `experience[].company`, `experience[].company_id`, `experience[].company_url`, `experience[].employer`; заменяет значение поля `recommendation` на пустой список
