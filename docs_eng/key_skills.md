# Key skills

> Attention! The values in the directories may change at any time. Do not address them directly.

The method returns information on the requested key skills.

## Request

```
GET /skills?id={id1}&id={id2}&id={id3}
```

where id – a list of key skill identifiers. No more than 50 values can be sent. For example, ?id=2716&id=3019&id=0

## Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "text": "Heating and cooling systems",
            "id": "2716"
        },
        {
            "text": "Cold kitchen",
            "id": "3019"
        }
    ]
}
```

> :warning: If you send the ID of a non-existent key skill, it will not return any information

The information for each key skill includes the following fields:

Name | Type | Description
--- | ------------ | --------
id | number | ID
text | string | Name

## Errors

* `400 Bad Request` – incorrect request arguments or [bulk-request error](errors.md#bulk-request)
* `403 Forbidden` – invalid authorisation. Awaiting user or app authorisation
