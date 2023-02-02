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
          "url": "https://hh.ru/employer/invoice/purchase?code=VPREM&count=1",
          "price": {
            "amount": "10152.0",
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
vacancy_billing_type.id | string | тип публикации (справочник [vacancy_billing_type](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries))
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
price.currency | string | Идентификатор валюты (справочник [currency](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries))

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
