# API services for employer

<a name="payable-api-actions"></a>
## Information on active API services for paid methods

You must be authorised as an employer to obtain information.

### Request

```
GET /employers/{employer_id}/services/payable_api_actions/active
```
where `employer_id` - employer id, 
you can find the employer's id in the [current user info](me.md#employer-info).

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
  "items": [
    {
      "id": "12345678",
      "service_type": {
        "id": "API_UNLIMITED",
        "name": "Access to the API HH"
      },
      "activated_at": "2018-02-01T12:00:00+0300",
      "expires_at": "2019-01-31T12:00:00+0300",
      "balance": null
    },
    {
      "id": "12345680",
      "service_type": {
        "id": "API_LIMITED",
        "name": "The package of requests to the API HH"
      },
      "activated_at": "2019-02-01T12:00:00+0300",
      "expires_at": "2020-01-31T12:00:00+0300",
      "balance": {
        "actual": 10000,
        "initial": 10000
      }
    }
  ]
}
```

Each enabled service is displayed as a separate object in the `items` array, 
even if there are multiple enabled services of the same type.
If the employer has no active services, the response will have an empty `items` array.

Each element of `items` has the following fields:

Name | Type | Description
---|---|---
id | string | Service ID
service_type | object | [Service type](#service-type)
activated_at | string | Service activation time (according to [ISO 8601](general.md#date-format) accurate to second `YYYY-MM-DDThh:mm:ss±hhmm`)
expires_at | string | Service expiration time (according to [ISO 8601](general.md#date-format) accurate to second `YYYY-MM-DDThh:mm:ss±hhmm`)
balance | object, null | [Balance values](#balance)

<a name="service-type"></a>
#### Object `service_type`

Name | Type | Description
---|---|---
id | string | Service type ID
name | string | Localised name of service type

<a name="balance"></a>
#### Object `balance`

Balance is current for package services.

Name | Type | Description
---|---|---
initial | number | Balance value at the time of service activation
actual | number | Current balance value

### Ошибки

* `403 Forbidden` – current user is not an employer
* `404 Not Found` – specified employer does not exist
* `404 Not Found` – current user does not have the appropriate privileges to view information
