# Черновики вакансий

* [получение списка черновиков вакансий](#draft_list)
* [удаление черновика](#draft_delete)
* [публикация вакансии на основе черновика](#draft_publish)

<a name="draft_list"></a>
## Получение списка черновиков вакансий

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts/get)

<a name="draft_delete"></a>
## Удаление черновика

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts~1{draft_id}/delete)

### Запрос

```DELETE /vacancies/drafts/{draft_id}```

В случае успешного выполнения запроса, будет возвращён статус `204 No Content`.

### Ошибки

* `403 Forbidden` — текущий пользователь не является работодателем
* `404 Not Found` — если черновик не найден или у пользователя нет прав на удаление данного черновика


<a name="draft_publish"></a>

## Публикация вакансии на основе черновика

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts/post)

``` POST /vacancies/drafts/{draft_id}/publish```

дополнительно можно указать query-параметры:

* `ignore_duplicates=true` - форсировать
  [добавление дубликата](employer_vacancies.md#creation-ignore-duplicates).

* `with_professional_roles=true` - для публикации вакансии из черновика с профессиональными ролями вместо специализаций

При указании параметра `with_professional_roles=true` поле `specializations` перестает быть обязательным и игнорируется, а поле `professional_roles` становится обязательным.  

Запрос для публикации вакансии из черновика по его draft_id. Результатом работы запроса станет создание списка вакансий в количестве равном количеству городов в черновике (одна и более). При этом произойдет удаление черновика.    

Правила размещения вакансии и другую полезную информацию смотрите в разделе [Вакансии для работодателя](employer_vacancies.md) 

### Ответ

При успешном выполнении запроса вернется `201 Created`.

```
HTTP/1.1 201 Created

```

В теле ответа возвращается массив с идентификаторами опубликованных вакансий:

```json
{
    "vacancy_ids": [78789890, 78789891, 78789892]
}
```

### Ошибки

* `400 Bad Request` – ошибки в полях при добавлении вакансии.
* `403 Forbidden` – добавление вакансий недоступно данному пользователю.
* <a name="creation-ignore-duplicates"></a> `403 Forbidden` –
  добавление вакансии недоступно, так как вакансия с похожими
  данными уже опубликована у данного работодателя. Если вы уверены, что
  добавление дубликата необходимо, вы можете добавить к запросу параметр
  `POST /vacancies/drafts/{draft_id}/publish?ignore_duplicates=true`.
* `404 Not Found` — если черновик не найден

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#vacancies-create-n-edit).
