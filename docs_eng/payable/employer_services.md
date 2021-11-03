# API services for employers

<a name="payable-api-actions"></a>
## Information about active API services for payable methods

You must be authorized under an employer to obtain information.

### Request

```
GET /employers/{employer_id}/services/payable_api_actions/active
```
where `employer_id` is the employer's ID, which can be found in
[current user information](../me.md#employer-info).

### Response

A successful response contains the code `200 OK` and this body:

```json
{
  "items": [
    {
      "id": "12345678",
      "service_type": {
        "id": "API_UNLIMITED",
        "name": "HH API access"
      },
      "activated_at": "2018-02-01T12:00:00+0300",
      "expires_at": "2019-01-31T12:00:00+0300",
      "balance": null
    },
    {
      "id": "12345680",
      "service_type": {
        "id": "API_LIMITED",
        "name": "HH API request packet"
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

Every enabled service is displayed as a separate object in the `items` array,
even if multiple services of the same type are enabled.
If the employer has no active services, the response will return an empty `items` array.

Each element of `items` has the following fields:

Name | Type | Description
---|---|---
id | string | Service ID
service_type | object | [Service type](#service-type)
activated_at | string | Service activation time (in the format [ISO 8601](../general.md#date-format) with to-the-second accuracy `YYYY-MM-DDThh:mm:ss±hhmm`)
expires_at | string| Service expiration time (in the format [ISO 8601](../general.md#date-format) with to-the-second accuracy `YYYY-MM-DDThh:mm:ss±hhmm`)
balance | object, null | [Balance values](#balance)

<a name="service-type"></a>
#### Object `service_type`

Name | Type | Description
---|---|---
id | string | Service type ID
name | string | Localized name of service type

<a name="balance"></a>
#### Object `balance`

Balance is up-to-date for packet services.

Name | Type | Description
---|---|---
initial | numeral | Balance value at the time of service activation
actual | numeral | Current balance value

### Errors

* `403 Forbidden` — current user is not the employer
* `404 Not Found` – the employer named does not exist
* `404 Not Found` – current user has no data viewing rights
