# Список улучшений для вакансии

Данный метод доступен только для работодателей. 

### Запрос

```
GET /vacancies/{vacancy_id}/upgrades
```

### Ответ

Успешный ответ приходит с кодом `200 ОК` и содержит тело следующего формата:

```json
{
  "items": [
    {
      "vacancy_billing_type": {
        "id": "premium",
        "name": "Публикация «Премиум»",
        "description": "Максимум откликов в течение недели..."
      },
      "actions": [
        {
          "type": "direct_upgrade"
        },
        {
          "type": "activate",
          "cart_id": "5967035",
          "url": "https://hh.ru/employer/invoice/finish?cartId=5967035"
        },
        {
          "type": "buy",
          "url": "https://hh.ru/employer/create_cart?products=%5B%7B%22code%22%3A+%22VPPL%22%2C+%22price%22%3A+1284200%2C+%22pricePerOne%22%3A+1284200%2C+%22count%22%3A+1%2C+%22period%22%3A+%2230%22%2C+%22currency%22%3A+%22RUR%22%2C+%22region%22%3A+%222000231%22%2C+%22professionalArea%22%3A+%5B%220%22%5D%2C+%22products%22%3A+%7B%220%22%3A+%7B%22code%22%3A+%22VPREM%22%2C+%22count%22%3A+1%2C+%22products%22%3A+%7B%7D%7D%7D%7D%5D&source=API",
          "price": {
            "amount": "12842.0",
            "currency_code": "RUR"
          }
        }
      ],
      "without_action": null
    },
    {
      "vacancy_billing_type": {
        "id": "standard_plus",
        "name": "Публикация «Стандарт плюс»",
        "description": "Максимум откликов в течение месяца..."
      },
      "actions": [],
      "without_action": {
        "reason": "Превышено количество улучшений вакансии"
      }
    }
  ]
}
```

где для каждого элемента `items`:

Имя | Тип | Описание
---- | --- | ---
vacancy_billing_type.id | string | тип публикации (справочник [vacancy_billing_type](https://github.com/hhru/api/blob/master/docs/dictionaries.md))
vacancy_billing_type.name | string | название типа публикации
vacancy_billing_type.description | string | описание типа вакансии
actions | array | список возможных действий
without_action | object или null | null в случае, если присутствуют элементы в actions или объект с описанием причины, по которой не возможно улучшение вакансии до данного типа
without_action.reason | string | описание причины, по которой не возможно улучшение вакансии до данного типа

для каждого элемента `actions`:

Имя | Тип | Описание
---- | --- | ---
type | string | тип действия direct_upgrade, activate или buy. [Значения типов действия](#action_types). 
url | string или null | ссылка на действие
cart_id | integer или null | идентификатор заказа, ожидающего активации. Присутствует для `type=activate` 
price | object или null | стоимость. Присутствует для `type=buy`
price.amount | double | значение цены
price.currency | string | Идентификатор валюты (справочник [currency](https://github.com/hhru/api/blob/master/docs/dictionaries.md))

<a name="action_types"></a>
Значения типов действия `actions.type`

Значение | Описание
---- | --- 
direct_upgrade | публикации вакансий данного типа есть на счету, в данный момент можно менять тип вакансии  
activate | есть публикации вакансий данного типа в не активированных заказах. Необходимо перейти по ссылке, указанной в `actions.url` и активировать заказ. После чего будет доступна улучшение вакансии. 
buy | нет доступных публикации вакансий данного типа. Необходимо докупить таковые. Ссылка позволяет напрямую перейти к покупке публикаций нужного типа.  

### Ошибки

* `403 Forbidden` — текущий пользователь не является работодателем
* `404 Not Found` — если вакансия не найдена или у пользователя нет прав на просмотр данной вакансии
