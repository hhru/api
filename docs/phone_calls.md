# История звонков

Информация о звонках может присутствовать на [списке откликов соискателя](negotiations.md#get_negotiations) и при просмотре [отклика/приглашения соискателя](negotiations.md#get_negotiation)

Объект выглядит следующим образом:

```json
{
    "picked_up_phone_by_opponent": true,
    "items": [
      {
        "id": 123,
        "status": "call_in_progress",
        "creation_time": "2022-03-04T19:39:58+0300",
        "last_change_time": null,
        "duration_seconds": null
      }
    ]
}
```

где:

Имя | Тип | Описание
 --- | --- | ---
picked_up_phone_by_opponent | boolean | ответил ли абонент соискателю хоть 1 раз 
items | массив | Массив звонков



<a name="phone_call"></a>
## Звонок

Пример завершенного звонка:

```json
{
  "id": 111,
  "status": "call_ended",
  "creation_time": "2022-03-04T19:39:58+0300",
  "last_change_time": "2022-03-04T19:41:58+0300",
  "duration_seconds": 120     
}
```

где:

Имя | Тип | Описание
 --- | --- | ---
id | число | Идентификатор звонка
status | строка | Статус звонка. Разрешенные значения находятся в справочнике [/dictionaries](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) в разделе ```phone_call_status```
creation_time | строка | Дата и время создания звонка
last_change_time | строка | Дата и время обновления звонка
duration_seconds | число | Длительность звонка в секундах
