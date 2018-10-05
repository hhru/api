# FAQ
Информация актуальна на момент написания, но через какое-то время может устареть.

<a name="invitation_from_negotiation"></a>
<details><summary><strong>Как пригласить соискателя на собеседование?</strong></summary>

### Способ 1.
1. Для приглашения соискателя на собеседование необходимо получить список [коллекций и работодательских состояний откликов/приглашений по вакансии](employer_negotiations.md#collections):

```
GET /negotiations?vacancy_id={vacancy_id}
```
где vacancy_id - id вакансии, для которой есть отклики

#### Ответ

```javascript
{
    "collections": [
        {
            "id": "response",
            "name": "Неразобранные",
            "description": "Описание коллекции",
            "url": "https://api.hh.ru/negotiations/response?vacancy_id=123456",
            // ...
        }
        // ...
    ]
    // ...
}
```
2. Затем, получив url из списка коллекций (параметр ``collections[].url``), нужно сделать запрос на него
```
GET /negotiations/{neg_collection_name}?vacancy_id={vacancy_id}
```
например:
```
GET /negotiations/response?vacancy_id=123456
```
В ответ вернутся действия (параметр ``actions[].url``), которые можно совершить с отлкиком, в данном случае из коллекции response.
#### Ответ

```javascript
{
    "actions": [
        {
            "id": "interview",
            "enabled": true,
            "method": "PUT",
            "url": "https://api.hh.ru/negotiations/interview/123456789",
            "arguments": [
                        {
                            "id": "message",
                            "required": true,
                            "required_arguments": []
                        }
                        //...
            ]
            //...
        }
        // ...
    ]
    // ...
}
```
3. Далее необходимо выполнить запрос для совершения действия по отклику/приглашению
```
PUT /negotiations/{action_id}/{negitiation_id}?message={message_text}
```
например:
```
PUT /negotiations/interview/123456789?message=new_msg
```
Также кроме ``message`` в ``arguments[]`` могут приходить [другие аргументы](employer_negotiations.md#actions-info).

Таким образом, пользователь получит сообщение в ответ на свой отклик и будет приглашен на интервью.

### Способ 2.
1. Для создания приглашения необходимо запросить вакансии работодателя, применимые к выбранному резюме.
Получить эту информацию можно в [списке вакансий работодателя](employer_vacancies_for_invitation.md):
```
GET /employers/{employer_id}/vacancies/active?resume_id={resume_id}
```
#### Ответ

```javascript
{
    "items": [
        {
            "negotiations_actions": [
                {
                    "id": "phone_interview",
                    "name": "Телефонное интервью",
                    "enabled": true,
                    "method": "POST",
                    "url": "https://api.hh.ru/negotiations/phone_interview",
                    "arguments": [
                        {
                            "id": "resume_id",
                            "required": true,
                            "required_arguments": []
                        },
                        {
                            "id": "vacancy_id",
                            "required": true,
                            "required_arguments": []
                        },
                        {
                            "id": "message",
                            "required": true,
                            "required_arguments": []
                        }
                        //...
                    ]
                    //...
                }
            ]
            // ...
        }
    ]
    // ...
}
```
2. Выбрать действие, которое необходимо осуществить (параметр ``negotiations_actions[].url``), и выполнить его, послав запрос
```
POST /negotiations/{action_id}?resume_id={resume_id}&vacancy_id={vacancy_id}&message={message_text}
```
например:
```
POST /negotiations/phone_interview?resume_id=123456&vacancy_id=654321&message=new_msg
```
Также кроме ``resume_id``, ``vacancy_id``, ``message`` в ``arguments[]`` могут приходить [другие аргументы](employer_negotiations.md#actions-info).

Таким образом, соискатель получит сообщение и будет приглашен на телефонное интервью.

Аналогично можно выполнить любые доступные для работодателя действия с откликом.
</details>

<a name="resume_search"></a>
<details><summary><strong>Есть ли в API hh.ru поиск по резюме?</strong></summary>
В API hh.ru на текущий момент поиска по базе резюме нет и в ближайшее время не появится.
</details>
