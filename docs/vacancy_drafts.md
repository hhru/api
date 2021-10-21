# Черновики вакансий

* [получение списка черновиков вакансий](#draft_list)
* [удаление черновика](#draft_delete)
* [публикация вакансии на основе черновика](#draft_publish)

<a name="draft_list"></a>
## Получение списка черновиков вакансий

Запрос для получения доступных черновиков вакансий для текущего менеджера. Если у менеджера несколько рабочих аккаунтов,
можно работать с любым из них согласно инструкции про [рабочие аккаунты менеджера](manager_accounts.md).

### Запрос

```GET /vacancies/drafts```

Дополнительные параметры запроса:
* [параметры пагинации `page` и `per_page`](general.md#pagination)


### Ответ

В случае успешного выполнения запроса, будет возвращён статус `200 OK`. В теле ответа будет содержаться информация о
доступных черновиках:

```json
{
  "items": [
    {
      "areas": [
        {
          "id": "4786",
          "name": "Артышта"
        },
        {
          "id": "4787",
          "name": "Бачатский"
        },
        {
          "id": "1231",
          "name": "Белово"
        }
      ],
      "completed_fields_percentage": 100,
      "draft_id": "1110032",
      "insufficient_publications": [
        {
          "publication_type": "standard",
          "vacancy_type": "open",
          "count": 2
        }
      ],
      "insufficient_quotas": [
        {
          "publication_type": "standard",
          "vacancy_type": "open",
          "count": 1
        }
      ],
      "last_change_time": "2021-05-18T11:20:48+03:00",
      "name": "Заведующий отделом розничных продаж",
      "publication_ready": true,
      "publication_type": "standard",
      "vacancy_type": "open",
      "required_publications": [
        {
          "publication_type": "standard",
          "vacancy_type": "open",
          "count": 3
        }
      ],
      "auto_publication": null
    },
    {
      "areas": [
        {
          "id": "2842",
          "name": "Балыкчы"
        }
      ],
      "completed_fields_percentage": 100,
      "draft_id": "1110031",
      "insufficient_publications": null,
      "insufficient_quotas": null,
      "last_change_time": null,
      "name": "Куратор",
      "publication_ready": true,
      "publication_type": "standard_plus",
      "vacancy_type": "open",
      "required_publications": null,
      "auto_publication": {
        "bill_uid": "4011054/3",
        "cart_id": "5967030"
      }
    }
  ],
  "found": 2,
  "page": 0,
  "pages": 1,
  "per_page": 20
}
```

Имя | Тип | Описание
---- | --- | --------
found | number | Количество найденных черновиков 
pages | number | Количество страниц с черновиками 
per_page | number | Количество элементов на страницу
page | number | Номер текущей страницы 
items | array | Список черновиков

где для каждого элемента `items`:

<a name="item"></a>

Имя | Тип | Описание
---- | --- | --------
id | string | Идентификатор черновика
name | string | Название вакансии
publication_type | string | Тип публикации (справочник [vacancy_billing_type](dictionaries.md))
vacancy_type | string | Тип вакансии (справочник [vacancy_type](dictionaries.md))
areas | array | Коды и название регионов (фед. округа, субъекты федерации, города).
completed_fields_percentage | number | Процент заполнения черновика
insufficient_publications | array или null | Массив [объектов](#publications) с информацией о том, каких публикаций не хватает на счету для публикации вакансии из данного черновика.
insufficient_quotas | array или null | Массив [объектов](#publications) с информацией о том, какие квоты превышены.
required_publications | array или null | Массив [объектов](#publications) с информацией о необходимых публикациях на счету
last_change_time | string или null | Время изменения черновика (в формате [ISO 8601](../general.md#date-format) с точностью до секунды `YYYY-MM-DDThh:mm:ss±hhmm`)
publication_ready | boolean  | Готовность черновика к публикации
auto_publication | object или null | Состояние автопубликации. [Объект](#auto_publication_state) при активной автопубликации, иначе null.

<a name="auto_publication_state"></a>
Активная автопубликация означает что при поступлении оплаты по счету, номер которого указанн в объекте, произойдёт
автоматическая публикация вакансии из данного черновика.   
Формат объекта `Состояние автопубликации`

Имя | Тип | Описание
---- | --- | --------
bill_uid | string | Номер счета
cart_id | string | Идентификатор заказа

<a name="publications"></a>
Формат объекта с количеством публикаций

Имя | Тип | Описание
---- | --- | --------
publication_type | string | Тип публикации (справочник [vacancy_billing_type](https://github.com/hhru/api/blob/master/docs/dictionaries.md))
vacancy_type | string | Тип вакансии (справочник [vacancy_type](dictionaries.md))
count | number | Количество

### Ошибки

* `403 Forbidden` — текущий пользователь не является работодателем

<a name="draft_delete"></a>
## Удаление черновика

### Запрос

```DELETE /vacancies/drafts/{draft_id}```

В случае успешного выполнения запроса, будет возвращён статус `204 No Content`.

### Ошибки

* `403 Forbidden` — текущий пользователь не является работодателем
* `404 Not Found` — если черновик не найден или у пользователя нет прав на удаление данного черновика


<a name="draft_publish"></a>

## Публикация вакансии на основе черновика

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
