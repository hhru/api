# List of vacancy upgrades

This method is available to employers only.

### Request

```
GET /vacancies/{vacancy_id}/upgrades
```

### Response

A successful response contains the code `200 OK` and this body format:

```json
{
  "items": [
    {
      "vacancy_billing_type": {
        "id": "premium",
        "name": "«Premium» Publication",
        "description": "Maximum responses per week..."
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
        "name": "«Standard Plus» publication",
        "description": "Maximum responses per month..."
      },
      "actions": [],
      "without_action": {
        "reason": "Vacancy upgrade quota exceeded"
      }
    }
  ]
}
```

with the following indicated for each `items` element:

Name | Type | Description
---- | --- | ---
vacancy_billing_type.id | string | publication type (directory [vacancy_billing_type](https://github.com/hhru/api/blob/master/docs_eng/dictionaries.md))
vacancy_billing_type.name | string | name of publication type
vacancy_billing_type.description | string | description of vacancy type
actions | array | list of possible actions
without_action | object or null | null where some elements are present in actions or there is an object with a statement of the reason why the vacancy cannot be upgraded to the given type
without_action.reason | string | statement of the reason why the vacancy cannot be upgraded to the given type

for each `actions` element:

Name | Type | Description
---- | --- | ---
type | string | type of action direct_upgrade, activate or buy. [Values for action types](#action_types).
url | string or null | link to action
cart_id | integer or null | ID of the order awaiting activation. Shown for `type=activate`
price | object or null | price. Shown for `type=buy`
price.amount | double | price amount
price.currency | string | currency ID (directory [currency](https://github.com/hhru/api/blob/master/docs_eng/dictionaries.md))

<a name="action_types"></a>
`actions.type` values for action types

Value | Description
---- | --- 
direct_upgrade | there are publications of this vacancy type in the account, vacancy type can be changed at this time
activate | there are publications of this vacancy type in orders that were never activated. Click through on the link shown in `actions.url` and activate the order. Vacancy upgrade will then become available.
buy | no available publications of this vacancy type. They have to be purchased additionally. The link offers a direct path towards purchasing publications of the required type.

### Errors

* `403 Forbidden` — current user is not the employer
* `404 Not Found` — where the vacancy was not found or the user has no viewing rights for the vacancy
