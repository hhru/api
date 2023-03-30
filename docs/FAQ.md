# FAQ
Информация актуальна на момент написания, но через какое-то время может устареть.

<a name="api_payment"></a>
<details><summary><strong>Сколько стоит API?</strong></summary>

Для уточнения стоимости API Вам необходимо обратиться к Вашему персональному менеджеру или позвонить по телефону: 
+7 495 974-64-27 (для Москвы и Подмосковья),  
+7 812 458-45-45 (для Санкт-Петербурга),  
8 800 100-64-27 (для регионов России),
+375 17 336 03 02, +375 33 336 03 02 (для Республики Беларусь).
</details>

<a name="speed_request"></a>
<details><summary><strong>Как долго будет обрабатываться заявка на приложение?</strong></summary>

Заявка на создание приложения должна пройти проверку нескольких отделов, 
этот процесс может занимать до 15 рабочих дней (это явно указано на форме регистрации). 
Мы можем предоставить информацию о статусе заявки, но не влиять на скорость/обсуждение/результат.
</details>

<a name="invitation_from_negotiation"></a>
<details><summary><strong>Как пригласить соискателя на собеседование?</strong></summary>

### Вариант 1. Соискатель уже откликнулся на вашу вакансию
1. Для приглашения соискателя на собеседование необходимо получить список [коллекций и работодательских состояний откликов/приглашений по вакансии](employer_negotiations.md#collections):

```
GET /negotiations?vacancy_id={vacancy_id}
```
где vacancy_id - id вакансии, для которой есть отклики

#### Ответ

```json
{
    "collections": [
        {
            "id": "response",
            "name": "Неразобранные",
            "description": "Описание коллекции",
            "url": "https://api.hh.ru/negotiations/response?vacancy_id=123456",
             ...
        }
         ...
    ]
     ...
}
```
2. Затем нужно сделать `GET` запрос по урлу, из поля `colletions[].url` из нужной коллекции.

в данном примере:
```
GET /negotiations/response?vacancy_id=123456
```
В ответ вернутся действия (`actions`), которые можно совершить с откликом (в примере: из коллекции response).
#### Ответ

```json
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
                        ...
            ]
            ...
        }
         ...
    ]
     ...
}
```
3. Для совершения действия по отклику/приглашению необходимо выполнить запрос из списка `actions`, передав аргументы, содержащиеся в поле `arguments`.

в данном примере:
```
PUT /negotiations/interview/123456789?message=new_msg
```

Таким образом, пользователь получит сообщение в ответ на свой отклик и будет приглашен на интервью.

### Вариант 2. Приглашение соискателя, который не откликнулся на вакансию
1. Для создания приглашения необходимо запросить вакансии работодателя, применимые к выбранному резюме.
Получить эту информацию можно в [списке вакансий работодателя](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/get-active-vacancy-list):
```
GET /employers/{employer_id}/vacancies/active?resume_id={resume_id}
```
#### Ответ

```json
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
                        ...
                    ]
                    ...
                }
            ]
             ...
        }
    ]
     ...
}
```
2. Выбрать действие, которое необходимо осуществить (`negotiations_actions`), и выполнить его, послав запрос и передав аргументы, содержащиеся в поле `arguments`

в данном примере:
```
POST /negotiations/phone_interview?resume_id=123456&vacancy_id=654321&message=new_msg
```

Таким образом, соискатель получит сообщение и будет приглашен на телефонное интервью.

Аналогично можно выполнить любые доступные для работодателя действия с откликом.
</details>
