# Отзывы соискателей о работодателях

* [Получение списка отзывов](#getReviews)
* [Сохранение нового отзыва](#putReview)
* [Объект отзыва](#reviewObject)
* [Справочники](#dictionaries)
  * [Предмет оценки](#target)
  * [Продолжительность трудоустройства](#employmentDuration)
  * [Типы оценок в отзыве](#ratingType)
  * [Типы текстовых полей в отзыве](#textField)


<a name="getReviews"></a>
## Получение списка отзывов

`GET /employers/{employer_id}/reviews`

Параметры запроса:

 Имя            | Обязательный? | Описание
----------------|---------------|---------------------------
 `employer_id`  | Да            | Идентификатор работодателя

Возвращает список [отзывов](#reviewObject) на работодателя с идентификатором `employer_id`.

Успешный ответ:
```json5
{
  "reviews": [
    {
      "employerId": 123, // == employer_id
      "target": "INTERVIEW",
      // ...
    },
    // ...
  ]
}
```


<a name="putReview"></a>
## Сохранение отзыва

> ‼️ Требуется авторизация соискателя

`POST /employers/{employer_id}/reviews`

Параметры запроса:

 Имя            | Обязательный? | Описание
----------------|---------------|---------------------------
 `employer_id`  | Да            | Идентификатор работодателя

Сохраняет новый [отзыв](#reviewObject) на работодателя с идентификатором `employer_id`.

Пример тела запроса:
```json5
{
  "review": {
    // Внимание: поле employerId не включается в объект
    "fromPageWithVacancyId": 456,
    "target": "PREVIOUS_EMPLOYER",
    // ...
  }
}
```

Для описания полей см. [объект отзыва](#reviewObject).

Ответ в случае успешного сохранения:
```
204 No Content
```

<a name="reviewObject"></a>
## Объект отзыва

Пример:
```json5
{
  "employerId": 123,
  "fromPageWithVacancyId": 456,
  "target": "CURRENT_EMPLOYER",
  "employmentDuration": "ONE_TWO_YEARS",
  "city": "Москва",
  "position": "Дегустатор",
  "ratings": {
    "SALARY": 4,
    "WORKPLACE": 5,
    // ...
  },
  "textFields": {
    "ADVANTAGES": "Мне понравилось",
    "DISADVANTAGES": "Мне не понравилось",
    // ...
  },
  "recommendationFlag": true
}
```

Описание полей:

 Имя                      | Тип               | Описание
--------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 `employerId`             | number            | (Только для [получения списка отзывов](#getReviews)) Идентификатор оцениваемого работодателя
 `fromPageWithVacancyId`  | number или null   | (Только для [сохранения нового отзыва](#putReview)) Идентификатор вакансии, со страницы которой был отправлен отзыв, или `null`, если отзыв отправлен со страницы работодателя. 
 `target`                 | string            | [Предмет оценки](#target)
 `employmentDuration`     | string или null   | [Продолжительность трудоустройства](#employmentDuration)
 `city`                   | string или null   | Город
 `position`               | string или null   | Должность
 `ratings`                | object            | Словарь с [типами оценок](#ratingType) и целыми значениями от 1 до 5
 `textFields`             | object            | Словарь с [типами текстовых полей](#textField) и значениями
 `recommendationFlag`     | boolean или null  | Флаг "Посоветовали ли бы работать тут другу?"


<a name="dictionaries"></a>
## Справочники

> ‼️ Внимание! Значения в справочниках могут поменяться в любой момент. Не нужно завязываться на них.

<a name="target"></a>
### Предмет оценки

`GET /employer_reviews/dictionaries/target`

Пример успешного ответа:
```json5
{
  "target": [
    {
      "id": "CURRENT_EMPLOYER",
      "name": "Работаю в компании"
    },
    {
      "id": "PREVIOUS_EMPLOYER",
      "name": "Бывший сотрудник"
    },
    {
      "id": "INTERVIEW",
      "name": "Попытка трудоустройства"
    },
    // ...
  ]
}
```

<a name="employmentDuration"></a>
### Продолжительность трудоустройства

`GET /employer_reviews/dictionaries/employment_duration`

Пример успешного ответа:
```json5
{
  "employmentDuration": [
    {
      "id": "LESS_THAN_ONE_YEAR",
      "name": "Меньше года"
    },
    {
      "id": "ONE_TWO_YEARS",
      "name": "1...2 года"
    },
    // ...
  ]
}
```

<a name="ratingType"></a>
### Типы оценок в отзыве

`GET /employer_reviews/dictionaries/rating_type?target={}`

Параметры запроса:

 Имя        | Обязательный? | Описание
------------|---------------|---------------
 `target`   | Да            | Предмет оценки

Пример успешного ответа:
```json5
{
  "ratingType": [
    {
      "id": "SALARY",
      "name": "Оплата труда"
    },
    {
      "id": "WORKPLACE",
      "name": "Рабочее место"
    },
    // ...
  ]
}
```

<a name="textField"></a>
### Типы текстовых полей в отзыве

`GET /employer_reviews/dictionaries/text_field`

Пример успешного ответа:
```json5
{
  "textField": [
    {
      "id": "ADVANTAGES",
      "name": "Плюсы"
    },
    {
      "id": "DISADVANTAGES",
      "name": "Что можно улучшить?"
    },
    // ...
  ]
}
```
