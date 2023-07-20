# Резюме

* [Список резюме авторизованного пользователя](#mine)
* [Просмотр резюме](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume)
* [Создание и редактирование резюме](#create_edit)
* [Публикация и продление резюме](#publish)
* [Информация о статусе резюме и готовности резюме к публикации](#status-and-publication)
* [Клонирование резюме](#clone)
* [Удаление резюме](#delete)
* [Проверка возможности создания резюме](#availability)
* [Условия заполнения полей резюме](#conditions)
  * [Условия заполнения полей нового резюме](#init-conditions)
  * [Условия заполнения контактов в резюме](#conditions-contacts)
  * [Дополнительные правила заполнения полей резюме](#conditions-other)
* [Статусы резюме](#status)
* [Видимость резюме](#access_type)
  * [Списки видимости резюме](#visibility_lists)
  * [Получение списка типов видимости резюме](#get_access_types)
* [История просмотра резюме](#views)
* [Поиск по вакансиям, похожим на резюме](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume)

<a name="mine"></a>
## Список резюме авторизованного пользователя

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-mine-resumes)

## Просмотр резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume)

<a name="create_edit"></a>
## Создание и редактирование резюме

`POST /resumes` — добавление резюме.

`PUT /resumes/{resume_id}` — редактирование существующего. В качестве тела
запроса используется json в том же формате, что отдается при GET запросе. При
этом для полей с данными справочников из передаваемой JSON-структуры
используются только id передаваемых данных. Например, в резюме в поле владения
языками, указан русский как родной:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Русский",
            "level": {
                "id": "l1",
                "name": "Родной"
            }
        }
     ]
   }
```

Для того, чтобы добавить английский с уровнем знания «B2 — Средне-продвинутый», необходимо отправить следующий JSON:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Русский",
            "level": {
                "id": "l1",
                "name": "родной"
            }
        },
        {
            "id": "eng",
            "level": {
                "id": "b2"
            }
        }
    ]
  }
```

Первый элемент списка — это русский, который у нас уже был в языках, а второй —
это новый элемент, английский, который мы хотим добавить. Поля `language.name` и
`language.level.name`, в данном случае, не мешают, но и не несут полезную
информацию.

При отправке данные заменяют уже существующие данные указанного параметра.
Каждый параметр можно отправлять отдельно от остальных.

<a name="resume-keys"></a>
> Также ознакомьтесь с правилами заполнения параметров резюме в разделе [Условия заполнения полей резюме](#conditions)

<a name="resume-edit-params"></a>
Параметры:

* `last_name` — фамилия;
* `first_name` — имя;
* `middle_name` — отчество;
* `birth_date` — день рождения (ГГГГ-ММ-ДД);
* `gender` — пол. Элемент справочника [gender](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
* `photo` — фотография пользователя. см. [артефакты](https://api.hh.ru/openapi/redoc#tag/Rabota-s-artefaktami);
* `portfolio` — портфолио пользователя. см. [артефакты](https://api.hh.ru/openapi/redoc#tag/Rabota-s-artefaktami);
* `area` — город проживания. Элемент справочника [areas](areas.md);
* `metro` — ближайшая станция метро. Элемент справочника [metro](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-metro-stations). Если передать метро не принадлежащее переданной `area`, поле проигнорируется
  Имеет смысл указывать только для `area` с метро;
* `relocation` — возможен ли переезд в другой город. Состоит из полей:
    * `type` — элемент справочника [relocation_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
    * `area` — город, в который возможен переезд (список). Имеет смысл
      только с соответствующим полем `type`. Элемент справочника
      [areas](areas.md);
* `business_trip_readiness` — готовность к командировкам. Элемент справочника
  [business_trip_readiness](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `contact` — контактная информация (список). 
Про обязательность полей и данных смотрите в [условиях заполнения контактов](#conditions-contacts). 
Состоит из полей:
    * `type` — элемент справочника [preferred_contact_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
    * `value` — значение контакта. Для телефона состоит из четырех полей (`country `, `city`, `number`, `formatted`),
      для электронного адреса — строка.
    * `preferred` — предпочитаемый вид связи (`true` или `false`);
    * `comment` — комментарий к контакту;
* `site` — присутствие на других сайтах. Состоит из полей:
    * `type` — тип сайта. Элемент справочника
      [resume_contacts_site_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
    * `url` — ссылка на профиль, либо идентификатор на стороннем сайте/сервисе;
* `title` — желаемая должность;
* `professional_roles` — профессиональные роли соискателя (список). Элемент справочника
  [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary);
* `salary` — желаемая зарплата. Состоит из полей:
    * `amount` — сумма;
    * `currency` — идентификатор [валюты](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
* `employments` — занятость. Элементы справочника [employment](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `schedules` — график работы. Список из элементов справочника [schedule](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `education` — образование. Состоит из полей:
    * `elementary` — среднее образование (список). Обычно заполняется только
       при отсутствии высшего образования. Состоит из полей:
        * `year` — год окончания;
        * `name` — название учебного заведения;
    * `additional` — курсы повышения квалификации (список). Состоит из полей:
        * `organization` — организация, проводившая курс;
        * `name` — название курса;
        * `result` — специальность / специализация;
        * `year` — год окончания;
    * `attestation` — тесты, экзамены (список):
        * `organization` — организация, проводившая тест или экзамен;
        * `name` — название тест или экзамена;
        * `result` — специальность / специализация;
        * `year` — год сдачи;
    * `primary` — образование выше среднего (список). Состоит из полей:
        * `name` — название учебного заведения;
        * `name_id` — идентификатор учебного заведения, можно получить из
          [подсказок по названиям вузов](https://api.hh.ru/openapi/redoc#tag/Podskazki/operation/get-educational-institutions-suggests);
        * `organization` — факультет;
        * `organization_id` — идентификатор факультета, можно получить из
          [справочника факультетов](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-educational-institutions-dictionary);
        * `result` — специальность / специализация;
        * `result_id` — идентификатор специальности / специализации, можно
          получить из
          [подсказок по специализациям](suggests.md#specializations);
        * `year` — год окончания;
    * `level` — уровень образования. Элемент справочника
      [education_level](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `language` — владение языками (список). 
    * `id` - значение из справочника [languages](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-languages) 
    * `level` - значение из справочника [language_level](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)
* `experience` — опыт работы (список). Состоит из полей:
    * `company` — организация;
    * `company_id` — идентификатор организации, можно получить из
      [подсказок по организациям](suggests.md#companies);
    * `area` — регион расположения организации. Элемента справочника
      [areas](areas.md);
    * `company_url` — сайт компании;
    * `industries` — отрасли компании. Элемент справочника
      [/industries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-industries)
    * `position` — должность;
    * `start` — начало работы (ГГГГ-ММ-ДД);
    * `end` — окончание работы (ГГГГ-ММ-ДД);
    * `description` — обязанности, функции, достижения;
* `skills` — дополнительная информация, описание навыков в свободной форме;
* `skill_set` — ключевые навыки (список уникальных строк).
* `citizenship` — гражданство (список). Элемента справочника [areas](areas.md);
* `work_ticket` — разрешение на работу (список). Элемента справочника
  [areas](areas.md);
* `travel_time` — желательное время в пути до работы. Элемент справочника
  [travel_time](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries);
* `recommendation` — рекомендации (список). Состоит из полей:
    * `name` — имя;
    * `position` — должность;
    * `organization` — организация;
* `resume_locale` — локаль резюме. Элемент справочника [локали резюме](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-locales-for-resume).
* `driver_license_types` - cписок категорий водительских прав соискателя. Элемент справочника [тип водительских прав](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
* `has_vehicle` - наличие личного автомобиля у соискателя
* `hidden_fields` - [скрытые поля](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume) в резюме (список). Элемент справочника [resume_hidden_fields](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).
* `access` - [видимость резюме](#access_type)
    * `type` - тип видимости. Элемент справочника [resume_access_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries)

Параметры, берущиеся из [подсказок](suggests.md) (`name_id`, `organization_id`,
`result_id`, `company_id`), являются опциональными. При этом, если
данные параметры указаны, то в момент сохранения происходят проверки на их
корректность. В случае ошибок заполнения, таких как передача несуществующих
идентификаторов или не связанных друг с другом идентификаторов университета и
факультета, будет возвращён статус `HTTP 400 Bad Request` с указанием
родительского поля, в котором произошла ошибка (`education`, `experience`).
Дополнительно, при указании в опыте работы `company_id` название компании будет
подменено на название компании из подсказок.

### Ответ

Успешный ответ на создание резюме приходит с кодом `201 Created`, в заголовке
Location при этом будет url созданного резюме:

```
Location: /resumes/0123456789abcdef
```

Успешный ответ на обновление резюме приходит с кодом `204 No Content` и не
содержит тела.


### Ошибки

* `403 Forbidden` – запрос не от соискателя.
* `400 Bad Request` - ошибка в полях резюме. Дополнительно придет 
[расширенная информация](#resume-validation) по ошибкам.
* `404 Not Found` – резюме не найдено или недоступно текущему пользователю
  (при обновлении)
* `400 Bad Request` - превышено допустимое количество резюме (при создании).
  Дополнительно [будет указана ошибка](errors.md#resumes)
  с `type=resumes`, `value=total_limit_exceeded`.


<a name="resume-validation"></a>
### Ошибки в использовании полей при создании и редактировании резюме

При создании и редактировании резюме значения в полях проходят проверки (валидация) - формат использования полей и 
значений (см. [Параметры](#resume-edit-params)), существование данных, бизнес правила. 

При ошибках в ответ придет `400 Bad Request` с телом:
```json
{
    "errors": [
        {
            "type": "bad_json_data",
            "value": "year",
            "reason": "min_value",
            "description": "Значение ниже допустимого",
            "pointer": "/education/additional/1/year"
        },
        {
            "type": "bad_json_data",
            "value": "access",
            "reason": "required",
            "description": "Идентификатор доступа к резюме является обязательным полем",
            "pointer": "/access/type/id"
        }
    ]
}
```

Имя | Тип | Описание
--- | --- | ---
type | string | Класс ошибки (всегда принимает значение `bad_json_data`)
reason | string | Причина ошибки
value | string | Поле, в котором обнаружена ошибка
description | string | Описание ошибки для пользователя
pointer | string | [Указатель на данные](#error-pointer) с ошибкой во входящем сообщении

Ошибка валидации расширяет [стандартную ошибку API](errors.md#general-errors).

Возможные причины ошибок:

Код | Пояснение
--- | ---
required | поле является обязательным для заполнения
not_found | не найдено значение по переданному id
faculty_without_university | нельзя установить факультет без университета
not_in_dictionary | не найдено значение по переданному id в справочнике
not_a_leaf | значение не должно содержать потомков
end_date_before_start_date | значение `end` меньше `start`
not_country | значение area должно быть страной (см. [справочник стран](areas.md#countries))
more_than_one_native_language | указано более одного родного языка
must_contain_unique | переданные значения должны быть уникальны
from_different_profareas | переданные значения из разных отраслей
duplicate | значение уже было использовано
bad_image_type | переданное значение неправильного типа (для portfolio необходимы значения из `get /artifacts/portfolio`, для photo - `get /artifacts/photo`) 
processing | объект в процессе обработки
preferred_must_be_unique | предпочитаемый тип связи должен быть уникальным 
preferred_contact_not_specified | предпочитаемый тип связи не указан или не указано значение контакта
need_country_city_number_or_formatted | телефон в контактах указан в неверном формате (см. [условия заполнения контактов в резюме](#conditions-contacts))
invalid | ошибка в значении поля (поля должны соответствовать [условиям заполнения](resumes.md#conditions))
greater_than_max | значение больше максимума 
less_than_min | значение меньше минимума
earlier_than_min | указанная дата раньше минимально возможной
later_than_max | указанная дата позже максимально возможной
length_less_than_min | количество символов в поле меньше минимума
length_greater_than_max | количество символов в поле больше максимума
size_less_than_min | количество элементов меньше минимума
size_greater_than_max | количество элементов больше максимума
send_metro_without_area | не передано значение поля `area` при заполненном метро
not_belong_this_city | указанного метро нет в указанном городе
required_with_not_started_career | необходимо отправлять опыт работы, если специализация не начало карьеры
not_match_regexp | значение не соответствует регулярному выражению
more_than_one | передано более одного email
not_available | недопустимое значение

<a name="error-pointer"></a>
`pointer` для указания использует формат JsonPointer [RFC 6901](https://tools.ietf.org/html/rfc6901).
Например, `/education/additional/1/year` значит, что ошибка в поле из сообщения (`year` - должно быть числом):
```json
{
    "title": "Программист Python",
    "education": {
        "additional": [
            {
                "name": "Курс начальной подготовки",
                "organization": "Проводившая организация",
                "result": "Общие знания Python",
                "year": 2006
            },
            {
                "name": "Курс повышения квалификации",
                "organization": "Проводившая организация",
                "result": "Углубленные знания Python",
                "year": "2012 - ошибка"
            }
        ]
    },
    "salary": {
        "amount": 100500,
        "currency": "RUR"
    }
}
```


<a name="publish"></a>
## Публикация резюме

`POST /resumes/{resume_id}/publish`

При первой публикации резюме оно становится доступно для использования.

Повторная публикация означает обновление даты резюме. Ключ `next_publish_at`
у резюме указывает время, когда можно обновить резюме.


### Ответ

В случае успешной публикации вернётся код ответа `204 No Content` без тела.

### Ошибки

* `429 Too Many Requests` - если обновление ещё недоступно.
* `400 Bad Request` - если публикация или продление невозможны. Возможные причины:
  * не заполнены обязательные поля (чтобы понять, что именно не заполнено, можно вызвать урл [получения резюме](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume) и посмотреть поле `mandatory`),
  * не отредактированы поля после блокировки модератором,
  * резюме находится на проверке у модератора.
* `403 Forbidden` - если операция публикации резюме недоступна из-за отсутствия
  прав (например, для работодателя).


<a name="status-and-publication"></a>
## Информация о статусе резюме и готовности резюме к публикации

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume-status)

<a name="clone"></a>
## Клонирование резюме

`POST /resumes?source_resume_id={resume_id}`

В случае успешного клонирования вернётся код ответа `201 Created`, а в заголовке
`Location` ответа будет содержаться ссылка на новое резюме.

Для клонирования можно использовать только собственные резюме, иначе код ответа
будет `404 Not Found`.


<a name="delete"></a>
## Удаление резюме

```
DELETE /resumes/{resume_id}
```

где `resume_id` – идентификатор резюме.

Метод доступен только для соискателей. Резюме удаляется без возможности
восстановления. Все связанные с ним отклики исчезают.

### Ответ

В случае успешного удаления вернётся код ответа `204 No Content` без тела.

### Ошибки

* `403 Forbidden` – запрос не от соискателя.
* `404 Not Found` – резюме не найдено или недоступно текущему пользователю.


<a name="availability"></a>
## Проверка возможности создания резюме

### Запрос

```
GET /resumes/creation_availability
```

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "is_creation_available": true,
    "max": 20,
    "created": 2,
    "remaining": 18
}
```

где:

Имя  | Тип    | Описание
---- | ------ | ---
is_creation_available  | boolean | Флаг, который показывает, доступно ли создание новых резюме для данного пользователя
max | number | Максимально возможное количество резюме
created  | number | Количество уже созданных резюме
remaining  | number | Количество доступных для создания резюме

### Ошибки

* `403 Forbidden` – запрос не от соискателя.


<a name="conditions"></a>
## Условия заполнения полей резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Usloviya-zapolneniya-polej/operation/get-resume-conditions)

<a name="init-conditions"></a>
## Условия заполнения полей нового резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Usloviya-zapolneniya-polej/operation/get-new-resume-conditions)

<a name='conditions-contacts'></a>
## Условия заполнения контактов в резюме
При заполнении контактов в резюме необходимо учитывать следующие условия:

* В резюме обязательно должен быть указан email (и он может быть только один).

* В резюме должен быть указан хотя бы один телефон, причём можно указывать
  только один телефон каждого типа.

* Комментарий можно указывать только для телефонов, для email комментарий
  не сохранится.

* В контакте типа 'email' value — это email, а для телефонов — объект.


Пример сообщения для изменения контактов в резюме:
```json
{
    "contact": [
        {
            "type": {
                "id": "email"
            },
            "value": "box@test.ru"
        },
        {
            "type": {
                "id": "cell"
            },
            "value": {
                "country": "7",
                "city": "123",
                "number": "4567890",
                "preferred": true
            }
        },
        {
            "type": {
                "id": "home"
            },
            "value": {
                "formatted": "+7(499)9078456"
            },
            "comment": "Звонить до 21:00"
        }
    ]
}
```

Обязательно указать либо телефон полностью в поле `formatted`, либо все три части телефона по отдельности в
полях `country`, `city` и `number`. Если указано и то, и то, используются данные из разделенного телефона.
В поле `formatted` допустимо указание дополнительных символов: пробелов, скобок, дефисов.
В раздельных полях допустимы только цифры.


<a name='conditions-other'></a>
## Дополнительные правила заполнения полей резюме

Существует ещё несколько правил заполнения резюме, которые не укладываются в
представленный выше формат:

 * Нельзя создавать несколько резюме с одинаковым title.

 * Специализации должны быть из одной профессиональной области.

 * Город проживания должен быть из справочника `/areas` и при этом у выбранного
   города не должно быть потомков, т.е. нельзя указать город проживания
   «Россия».

 * Ближайшая станция метро должна находиться в городе проживания.

 * Для специализаций из профессиональной области *Начало карьеры, студенты*
   (id=15) можно не указывать опыт работы и навыки. Для остальных профобластей
   данные поля должны содержать хотя бы по одной записи.

 * Часть полей резюме являются read-only, их нельзя изменить при помощи
   POST/PUT на /resumes.
 
<a name="status"></a>
## Статус резюме

Ключ `status` определяет текущее состояние резюме и содержит элемент
справочника [resume_status](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries). После создания нового резюме оно
находится в статусе 'not_published'. В этом статусе резюме никому не видно,
пользователь начинает его наполнять и сохранять (незаполненные обязательные поля
можно увидеть в списке `progress.mandatory`). 

После того, как все обязательные поля будут заполнены, флаг `can_publish_or_update` 
будет установлен в `true`, и резюме можно будет
[опубликовать](#publish). Публикация резюме переводит его в статус `published`.
В этом статусе резюме доступно для поиска, если это позволяет
[видимость резюме](#access_type).

После перехода в статус `published`, резюме попадает в поле зрения модераторов и
может быть заблокировано (статус `blocked`), если поля резюме некорректно или
малоинформативно заполнены. Причины блокировки резюме можно найти в
[ключе `moderation_note`](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume-status). Заблокированное резюме
пропадает из поиска и не может быть использовано для отклика на вакансию.

После исправления, резюме можно отправить на повторное рассмотрение модератору.
В этом случае резюме переходит в статус `on_moderation`, откуда может снова
перейти в `blocked` или `published`, в зависимости от решения модератора.

После публикации резюме (статус установлен в `published`) его нельзя перевести
обратно в `not_published`, но можно скрыть, настроив
[видимость резюме](#access_type).

В статусе `published` резюме можно использовать для
[отклика на вакансию](negotiations.md), а так же оно появится в
[списке подходящих для отклика](suitable_resumes.md), если им еще не откликались
на эту вакансию.


<a name="access_type"></a>
## Видимость резюме

У каждого резюме есть настройка видимости `access`, которая определяет, кому будет доступно резюме
в поиске и по прямой ссылке. Формат поля в резюме:

```json
{
    "access": {
        "type": {
            "id": "clients",
            "name": "видно всем компаниям, зарегистрированным на HeadHunter"
        }
    }
}
```

После публикации резюме доступно для поиска всем работодателям. Чтобы это изменить
(например, работа найдена и нужно скрыть резюме из поиска), следует поменять
видимость резюме. За это отвечает ключ `access.type`. Тип видимости —
элемент справочника [resume_access_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries).

<a name="access_type_restrictions"></a>
‼️ С первого сентября 2021 года тип видимости с id `everyone` (видно всему интернету) стал недоступен для сохранения из-за ограничений законодательства.

 Код | Описание
 --- | --------
 no_one | Резюме такого типа никому не видно. Но им можно откликнуться на вакансию, при этом резюме сменит тип на `whitelist`.
 whitelist | Резюме не видно никому, кроме указанных компаний. Если откликнуться на вакансию компании, которая не входит в список, компания автоматически в него попадёт. См. [списки видимости резюме](#visibility_lists).
 blacklist | Резюме доступно для поиска и просмотра всем компаниям, за исключением указанных. Если откликнуться на вакансию компании из черного списка, то компания вычеркивается из него автоматически. См. [списки видимости резюме](#visibility_lists).
 clients | Резюме доступно всем зарегистрированным компаниям на hh.ru.
 everyone | Резюме доступно всем без исключения (всему интернету). Этот тип [не доступен для сохранения](#access_type_restrictions).
 direct | Резюме доступно только по прямой ссылке (ссылка указана в ключе `alternate_url`).

<a name="visibility_lists"></a>
### Списки видимости резюме

Некоторые типы видимости, например `whitelist` и `blacklist`, подразумевают наличие списка работодателей,
для которых резюме должно быть видимо или скрыто. См. [управление списками видимости резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti).


<a name="get_access_types"></a>
### Получение списка типов видимости резюме

#### Запрос

```
GET /resumes/{resume_id}/access_types
```

где:
* `resume_id` — идентификатор резюме

#### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "items": [
        {
            "id": "everyone",
            "name": "видно всему интернету"
        },
        {
            "id": "no_one",
            "name": "не видно никому"
        },
        {
            "id": "clients",
            "name": "видно всем компаниям, зарегистрированным на HeadHunter"
        },
        {
            "id": "whitelist",
            "name": "видно выбранным компаниям",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/whitelist",
            "total": 3,
            "limit": 2000
        },
        {
            "id": "blacklist",
            "name": "скрыто от выбранных компаний",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/blacklist",
            "total": 5,
            "limit": 2000,
            "active": true
        },
        {
            "id": "direct",
            "name": "доступно только по прямой ссылке"
        }
    ],
    "auto_hide_time_options": [
        {
            "id": "month_12",
            "name": "1 год"
        },
        {
            "id": "month_10",
            "name": "10 месяцев",
            "active": true
        },
        {
            "id": "month_8",
            "name": "8 месяцев"
        }
    ]
}
```

Имя | Тип | Описание
----|-----|---------
items | array | Доступные типы видимости резюме.
items[].id | string | Идентификатор типа видимости.
items[].name | string | Имя типа видимости.
items[].active | boolean или null | Выбран ли тип видимости.
items[].list_url | string | Адрес списка (только для типов `blacklist` и `whitelist`).
items[].total | number | Количество компаний, добавленных в соответствующий список видимости (только для типов `blacklist` и `whitelist`).
items[].limit | number | Максимальное количество компаний в списке видимости (только для типов `blacklist` и `whitelist`).
auto_hide_time_options | array | Варианты времени автоскрытия резюме при неактивности пользователя, это поле возвращается только для пользователей rabota.by.
auto_hide_time_options[].id | string | Идентификатор варианта автоскрытия.
auto_hide_time_options[].name | string | Название варианта автоскрытия.
auto_hide_time_options[].active | boolean или null | Выбран ли вариант автоскрытия.


#### Ошибки

* `403 Forbidden` — пользователь не является соискателем.
* `404 Not Found` — резюме с указанным идентификатором не найдено или недоступно текущему пользователю.


См. также [управление списками видимости резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti).


<a name="views"></a>
## История просмотра резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume-view-history)

<a name="similar"></a>
## Поиск по вакансиям, похожим на резюме

Данные доступны только автору резюме.


### Запрос

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume)
