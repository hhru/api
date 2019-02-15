# Basic information about educational institutions

## Request

```
GET /educational_institutions?id={id1}&id={id2}&id={id3}
```

where id – list of educational institution IDs. No more than 50 values can be sent.
For example, `?id=39196&id=45470&id=0`

## Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "id": "39196",
            "acronym": "Mendeleev RCTU",
            "text": "Mendeleev Russian Chemical-Technological University",
            "synonyms": null,
            "area": {
                "id": "1",
                "name": "Moscow"
            }
        },
        {
            "id": "45470",
            "acronym": "NICTU n.a. D.I. Mendeleev",
            "text": "Novomoskovsk Institute of Mendeleev Russian Chemical-Technological University",
            "synonyms": null,
            "area": {
                "id": "1924",
                "name": "Novomoskovsk (Tula Oblast)"
            }
        }
    ]
}
```
 
> :warning: If you send the ID of a non-existent university, it will not return any information

The information for each university includes the following fields:

Name | Type | Description
--- | ------------ | --------
id | number | ID
acronym | string | Acronym (abbreviation)
text | string | Full name of the educational institution
synonyms | string or null | Previous names of the educational institution
area | object | region [from directory](areas.md)

## Errors

* `400 Bad Request` – incorrect request arguments or [bulk-request error](errors.md#bulk-request)
* `403 Forbidden` – incorrect authorisation. Awaiting authorisation of user or app