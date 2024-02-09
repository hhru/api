# Переписка (отклики/приглашения) для соискателя

*Документация по переписке для работодателя доступна в [отдельной статье](employer_negotiations.md).*

В процессе использования сайта соискатели выбирают вакансии.  Для того чтобы
связаться с работодателем на предмет трудоустройства, соискатель может
откликнуться на выбранную вакансию. Так же и работодатель, найдя интересное
резюме, может предложить соискателю рассмотреть вакансию (приглашение).

Для указанных целей служат специальные сущности — отклики/приглашения.  В них
может быть указана вакансия, резюме и переписка соискателя с работодателем, в
каждый момент времени такие сущности находятся в одном из состояний. Переход
между состояниями сопровождается появлением сообщений с опциональным текстовым
описанием и прочими полями. Сообщения со статусом `null` не переводят весь
отклик в новое состояние.

* [Получение списка откликов](#get_negotiations)
* [Получение списка активных откликов](#get_negotiations_active)
* [Откликнуться на вакансию](#post_negotiation)
* [Просмотр отклика/приглашения](#get_negotiation)
* [Скрыть отклик](#hide_message)
* [Просмотр списка сообщений в отклике](#get_messages)
* [Отправка нового сообщения](#send_message)
* [Редактирование сообщения в отклике](#edit_message)


<a name="get_negotiations"></a>
## Получение списка откликов

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/get-negotiations)

<a name="get_negotiations_active"></a>
## Получение списка активных откликов

### Запрос

Для получения списка активных откликов используйте параметр `status=active` в запросе [списка откликов](#get_negotiations)
 ```
 GET /negotiations?status=active
 ```

До 20.04.20 для запроса активных вакансий использовался ресурс:

```
GET /negotiations/active
```

В настоящее время он является устаревшим и поддерживается для обратной совместимости.

<a name="post_negotiation"></a>
## Откликнуться на вакансию

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/apply-to-vacancy)

<a name="get_negotiation"></a>
## Просмотр отклика/приглашения


### Запрос

```
GET /negotiations/{nid}
```
где nid - идентификатор отклика.


### Ответ

Возвращаемый объект полностью идентичен отдельному отклику, получаемому в [списке откликов](#get_negotiations)


<a name="hide_message"></a>
## Скрыть отклик
> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/hide-active-response)


<a name="get_messages"></a>
## Просмотр списка сообщений в отклике

### Запрос

```
GET /negotiations/{nid}/messages
```
где:

 * nid - идентификатор отклика

Параметры

 Имя | Тип | Обязательный | Описание
 --- | --- | --- | ---
 page | число | нет | Номер страницы, значение по умолчанию 0
 per_page | число | нет | Количество элементов на страницу, по умолчанию 20

### Ответ:

```json
{
    "found": 1,
    "pages": 1,
    "per_page": 20,
    "page": 0,
    "items": [
        {
            "id": "123",
            "viewed_by_me": true,
            "viewed_by_opponent": true,
            "created_at": "2013-10-07T18:30:57+0400",
            "text": "Вас приглашает очень крупный иностранный банк на зарплату, о которой мечтают арабские шейхи",
            "state": {
                "id": "invitation",
                "name": "Приглашение"
            },
            "author": {
                "participant_type": "employer"
            },
            "address": null,
            "assessments": [
                {
                    "id": "123",
                    "name": "Динамический тест числовых способностей",
                    "actions": [
                        {
                            "id": "proceed",
                            "name": "Перейти к тестированию",
                            "enabled": true,
                            "alternate_url": "https://hh.ru/applicant/assessment/123"
                        }
                    ]
                }
            ],
            "editable": false
        },
        {
            "id": "124",
            "viewed_by_me": true,
            "viewed_by_opponent": false,
            "created_at": "2013-10-08T10:12:23+0400",
            "text": "Верблюда и коня мне!",
            "state": {
                "id": "text",
                "name": "Текст"
            },
            "author": {
                "participant_type": "applicant"
            },
            "address": null,
            "editable": false
        }
    ]
}
```

где:

 Имя | Тип  | Описание
 --- | --- | ---
 found | число | Количество найденных сообщений
 pages | число | Количество найденных страниц с сообщениями
 per_page | число | Количество элементов на страницу
 page | число | Номер текущией страницы (начинается с 0)
 items | массив | Массив сообщений, см. ниже

 Отдельное сообщение имеет следующую структуру:

 Имя | Тип | Описание
 --- | --- | ---
 id | строка | Идентификатор сообщения
 viewed_by_me | логический | Прочитано ли сообщение смотрящим (для сообщений отправленных соискателем - всегда `true`)
 viewed_by_opponent | логический | Прочитано ли сообщение работодателем (для сообщений работодателя - `true`)
 editable | логический | Можно ли редактировать текст сообщения
 created_at | строка | Дата и время создания сообщения
 text | строка | Текст сообщения
 state | объект | Текущее состояние отклика. Возможные значения находятся в справочнике [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) в разделе `negotiations_state`
 author | объект | Кто автор сообщения
 author.participant_type | строка | Роль автора сообщения. Возможные значения находятся в справочнике [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) в разделе `negotiations_participant_type`
 address | объект, null | [Адрес](./address.md), привязанный к отклику/приглашению
 assessments | массив | [инструменты оценки](assessment.md), привязанные к сообщению


<a name="send_message"></a>
## Отправка нового сообщения

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/send-negotiation-message)

<a name="edit_message"></a>
## Редактирование сообщений в отклике

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/edit-negotiation-message)
