# Лимиты менеджера 

* [Дневной лимит просмотра резюме для текущего менеджера](#resume_limit)

<a name="resume_limit"></a>
## Дневной лимит просмотра резюме для текущего менеджера

### Запрос
`GET /employers/{employer_id}/managers/{manager_id}/limits/resume`

 где `employer_id` - идентификатор работодателя, который можно узнать в [информации о текущем работодателе](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere).
 где `manager_id` - идентификатор менеджера, который можно узнать в [информации о текущем пользователе](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/paths/~1me/get).

### Ответ

Пример ответа:
```json
{
    "limits": {
        "resume_view": 100
    },
    "spend": {
        "resume_view": 1
    },
    "left": {
        "resume_view": 50
    }
}
```

 Имя | Тип | Описание
 --- | --- | ---
 limits | object | лимиты 
 limits.resume_view | integer | лимит на просмотр резюме
 spend | object | текущие значения трат
 spend.resume_view | integer | количество просмотренных резюме
 left | object | оставшиеся значения
 left.resume_view | integer | количество оставшихся просмотров резюме. В этом значении учитывается лимит просмотров на компанию. Из-за этого он может быть меньше, чем доступно текущему пользователю.

### Ошибки
* `404 Not found` - Работодатель или менеджер не найден, или у пользователя нет прав
* `403 Forbidden` - Неподходящая авторизация
