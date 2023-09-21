# Резюме

* [Список резюме авторизованного пользователя](#mine)
* [Просмотр резюме](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume)
* [Создание резюме](#create)
* [Редактирование резюме](#edit)
* [Публикация и продление резюме](#publish)
* [Информация о статусе резюме и готовности резюме к публикации](#status-and-publication)
* [Клонирование резюме](#clone)
* [Удаление резюме](#delete)
* [Проверка возможности создания резюме](#availability)
* [Условия заполнения полей резюме](#conditions)
  * [Условия заполнения полей нового резюме](#init-conditions)
* [История просмотра резюме](#views)
* [Поиск по вакансиям, похожим на резюме](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume)

<a name="mine"></a>
## Список резюме авторизованного пользователя

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-mine-resumes)

## Просмотр резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume)

<a name="create"></a>
## Создание резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/create-resume)

<a name="edit"></a>
## Редактирование резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/edit-resume)

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

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/create-resume)

<a name="delete"></a>
## Удаление резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/delete-resume)

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

<a name="views"></a>
## История просмотра резюме

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume-view-history)

<a name="similar"></a>
## Поиск по вакансиям, похожим на резюме

Данные доступны только автору резюме.


### Запрос

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume)
