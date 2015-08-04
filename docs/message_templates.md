# Тексты писем

Работодателю доступны для чтения шаблоны текстов писем, отправляемых соискателю при приглашении на вакансию или отказе. В данный момент существуют следующие шаблоны:

Имя | Описание
----|---------
invite|используется при приглашении соискателя на вакансию
invite_after_response|используется при приглашении после отклика со стороны соискателя
quick_discard_after_response|используется при «отказе одним кликом»
discard_after_response|используется при отказе после отклика
discard_after_interview|используется при отказе после приглашения соискателя на интервью

В будущем список шаблонов может быть расширен.

## Запрос

```
GET /message_templates/{template}?topic_id={topic_id}
GET /message_templates/{template}?vacancy_id={vacancy_id}&resume_id={resume_id}
```

где `template` — название шаблона из списка выше.

Параметры:

Имя | Описание
----|---------
topic_id|Идентификатор существующего топика. Не допускается одновременная передача с другими параметрами.
vacancy_id|Идентификатор вакансии для приглашения. Требует передачи параметра `resume_id`.
resume_id|Идентификатор резюме для приглашения на вакансию. Требует передачи параметра `vacancy_id`.

Рекомендуется не конструировать ссылки самостоятельно, а использовать ссылки, которые содержатся в объекте `templates` в [списке топиков](./employer_negotiations.md#Список-откликовприглашений) и подходящих вакансий:
```json
"templates": [
    {
        "url": "https://api.hh.ru/message_templates/invite?resume_id=bff6f34eff05c3089f0039ed1f6a464f51626c&vacancy_id=80079136",
        "id": "invite"
    }
]
```

## Ответ

Успешный ответ приходит с кодом `200 OK` и содержит

```json
{
    "mail": {
        "text": "Здравствуйте, Иван Иванович! Благодарим Вас за отклик на вакансию... "
    }
}
```

Имя|Тип|Описание
---|---|--------
text|Строка|Текст сообщения, отправляемого соискателю по электронной почте при приглашении/отказе. Может изменяться в зависимости от типа вакансии (например, для анонимной вакансии).

## Ошибки

Код|type|value|Причина
---|----|-----|-------
404|not_found|—|несуществующий шаблон
403|forbidden|—|запрос выполнен с авторизацией анонима/соискателя либо работодателя без подключенной услуги доступа к базе резюме
400|bad_argument|topic_id|<ul><li>передан идентификатор несуществующего топика, топика другого работодателя либо топика, к которому нет доступа у текущего менеджера</li><li>вакансия из топика была заархивирована</li><li>резюме из топика было скрыто/удалено</li></ul>
400|bad_argument|resume_id|передан идентификатор несуществующего резюме либо резюме, недоступного работодателю
400|bad_argument|vacancy_id|передан идентификатор несуществующей/скрытой/архивной вакансии, вакансии другого работодателя либо вакансии, к которой нет доступа у текущего менеджера

В случае, если переданы конфликтующие параметры (`topic_id` одновременно с `resume_id` и/или `vacancy_id`), либо не переданы никакие параметры, запрос вернет
```json
{
    "errors": [
        {
            "type": "bad_argument",
            "value": "topic_id"
        },
        {
            "type": "bad_argument",
            "value": "resume_id"
        },
        {
            "type": "bad_argument",
            "value": "vacancy_id"
        }
    ]
}
```