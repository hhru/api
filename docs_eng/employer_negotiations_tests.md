# Tests solutions

This method allowed only employer authorization 

### Request

`GET /negotiations/{nid}/test/solution`

where `nid` - id of negotiation topic.

### Ответ

Success response should be with status `200 OK` and contains:

```json
{
  "test_result": {
    "name": "name",
    "score": 100,
    "mark": "EXCELLENT",
    "duration": 10,
    "tasks": [
      {
        "question": "How are you?",
        "closed_answers": [
          {
            "value": "fine",
            "selected": true,
            "correct": false
          },
          {
            "value": "good",
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
        "question": "What is your last think about?",
        "closed_answers": [],
        "opened_answer": {
          "value": "api hh.ru",
          "mark": "EXCELLENT"
        }
      }
    ]
  }
}
```

 Имя |   Тип  | Описание
 --- | ------ | ------------
name | string | Test's name
score | number | Score earned by respondent (from 0 to 100)
mark | string | Test's mark (`UNFAIR` - from 0 to 14  points, `FAIR` - from 15 to 44 points, `GOOD` - from 45 to 79 points, `EXCELLENT` from 80 to 100 points)
duration | number | Test's duration in seconds
tasks | array | Test's tasks
tasks[].question | string | Task's question
tasks[].opened_answer | object, null | Answer with any text
tasks[].opened_answer.value | string | Answer's text
tasks[].opened_answer.mark | string | Opened question's mark (`UNFAIR` - 0 points, `FAIR` - 30 points, `GOOD` - 60 points, `EXCELLENT` 100 points)
tasks[].closed_answers | array | Answers with supposed text
tasks[].closed_answers[].value | string | Answer's text
tasks[].closed_answers[].selected | logical | Is current answer selected
tasks[].closed_answers[].correct | logical | Is current answer correct

### Errors

* `403 Forbidden` - Current user is not an employer.
* `404 Not Found` - Topic is not exists or current user has not access to this topic.
