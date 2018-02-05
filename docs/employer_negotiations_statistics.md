# Статистика по работе с откликами

* [Статистика работодателя](#employer-stats)
* [Статистика менеджера](#manager-stats)

Для получения информации необходимо авторизоваться под работодателем.
Для пользователя без авторизации или для неправильно авторизованного пользователя вернется ответ `403 Forbidden`.

<a name="employer-stats"></a>
## Статистика работодателя

### Запрос

```
GET /employers/{employer_id}/negotiations_statistics
```

 где `employer_id` - идентификатор работодателя, который можно узнать в
 [информации о текущем пользователе](me.md#employer-info).

### Ответ

Пример ответа:

```json
{
    "employer_statistics": {
        "received": 20,
        "viewed_percent": 23,
        "viewed_percent_change": 10,
        "replied_percent": 0,
        "replied_percent_change": -15,
        "average_reply_time_in_days": 1.0
    }
}
```

Объект `employer_statistics` включает следующие поля:

| Имя | Тип | Описание |
|-----|-----|----------|
| received | number | количество откликов на вакансии работодателя, полученных за последние `30 дней` (далее период) |
| viewed_percent | number или null | процент прочитанных откликов на вакансии работодателя за период или `null` при отсутствии откликов |
| viewed_percent_change | number или null | изменение viewed_percent по сравнению с предыдущим периодом или `null` при отсутствии откликов |
| replied_percent | number или null | процент откликов на вакансии работодателя, перемещенных в любую другую [коллекцию](employer_negotiations.md#term-collection) с отправкой сообщения за период или `null` при отсутствии откликов |
| replied_percent_change | number или null | изменение replied_percent по сравнению с предыдущим периодом или `null` при отсутствии откликов |
| average_reply_time_in_days | number или null | среднее время в днях между получением отклика на вакансии работодателя и отправкой сообщения или `null` при отсутствии отправленных сообщений |

### Ошибки

* `404 Not found` - Работодатель не найден, или у пользователя нет прав

<a name="manager-stats"></a>
## Статистика менеджера

### Запрос

```
GET /employers/{employer_id}/managers/{manager_id}/negotiations_statistics
```

где:

* `employer_id` - идентификатор работодателя, который можно узнать в
  [информации о текущем пользователе](me.md#employer-info).
* `manager_id` - идентификатор менеджера.

### Ответ

Пример ответа:

```json
{
    "manager_statistics": {
        "received": 20,
        "viewed_percent": 23,
        "viewed_percent_change": 10,
        "replied_percent": 0,
        "replied_percent_change": -15,
        "average_reply_time_in_days": 1.0
    }
}
```

### Ошибки

* `404 Not found` - Работодатель или менеджер не найден, или у пользователя нет прав.
Статистика менеджера доступна самому менеджеру, а также менеджерам с [типом](employer_managers.md#dict) `main_contact_person`.

Объект `manager_statistics` включает следующие поля:

| Имя | Тип | Описание |
|-----|-----|----------|
| received | number | количество откликов на вакансии менеджера, полученных за последние `30 дней` (далее период) |
| viewed_percent | number или null | процент прочитанных откликов на вакансии менеджера за период или `null` при отсутствии откликов |
| viewed_percent_change | number или null | изменение viewed_percent по сравнению с предыдущим периодом или `null` при отсутствии откликов |
| replied_percent | number или null | процент откликов на вакансии менеджера, перемещенных в любую другую [коллекцию](employer_negotiations.md#term-collection) с отправкой сообщения за период или `null` при отсутствии откликов |
| replied_percent_change | number или null | изменение replied_percent по сравнению с предыдущим периодом или `null` при отсутствии откликов |
| average_reply_time_in_days | number или null | среднее время в днях между получением отклика на вакансии менеджера и отправкой сообщения или `null` при отсутствии отправленных сообщений |
