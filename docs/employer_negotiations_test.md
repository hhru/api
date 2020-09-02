# Результаты тестов прикрепленных к вакансиям

Данный метод доступен только для работодателей.

### Запрос

`GET /negotiations/{nid}/test/solution`

где `nid` - id отклика.

### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
  "test_result": {
    "name": "name",
    "score": 100,
    "mark": "EXCELLENT",
    "duration": 10,
    "tasks": [
      {
        "question": "В какой работе Ленина появляется знаменитая фраза «Учение Маркса всесильно, потому что оно верно»?",
        "closed_answers": [
          {
            "value": "«Государство и революция»",
            "selected": true,
            "correct": false
          },
          {
            "value": "«Три источника и три составных части марксизма»",
            "selected": false,
            "correct": true
          }       
        ],
        "opened_answer": {
          "value": " «Материализм и эмпириокритицизм»",
          "mark": "UNFAIR"
        }
      },
      {
        "question": "Закончите фразу Маркса: «Философы лишь различным образом объясняли мир, но дело заключается в том…»",
        "closed_answers": [],
        "opened_answer": {
          "value": "чтобы изменить его",
          "mark": "EXCELLENT"
        }
      }
    ]
  }
}
```

 Имя |  Тип   | Описание
 --- | ------ | --------------
name | string | Название теста
score | number | Количество набранных баллов (от 0 до 100)
mark | string | Оценка дифференцированная (`UNFAIR` - от 0 до 14  баллов, `FAIR` - от 15 до 44 баллов, `GOOD` - от 45 до 79 баллов, `EXCELLENT` от 80 до 100 баллов)
duration | number | Время затраченное на выполнение теста в секундах
tasks | array | Задания теста
tasks[].question | string | Вопрос
tasks[].opened_answer | object, null | Открытый ответ на вопрос (в свободной форме)
tasks[].opened_answer.value | string | Ответ на вопрос
tasks[].opened_answer.mark | string | Оценка, которую ставит работодатель на открытый вопрос (`UNFAIR` - 0 баллов, `FAIR` - 30 баллов, `GOOD` - 60 баллов, `EXCELLENT` 100 баллов)
tasks[].closed_answers | array | Закрытые варианты ответов на вопрос (предложенные соискателю)
tasks[].closed_answers[].value | string | Ответ на вопрос
tasks[].closed_answers[].selected | logical | Выбран ли предложенный вариант ответа 
tasks[].closed_answers[].correct | logical | Является ли правильным данный вариант ответа


### Ошибки

* `403 Forbidden` – если текущий пользователь - не работодатель.
* `404 Not Found` – указанный отклик не существует или недоступен текущему пользователю.
