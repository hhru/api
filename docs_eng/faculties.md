# List of educational institution faculties

## Request
 
```
GET /educational_institutions/{id}/faculties
```

where `id` – this is the id of an educational institution (`id` field from [tips for colleges](suggests.md#universities)).

## Response

Successful server response is returned with `200 OK` code and contains JSON with a list of faculties, sample response:

```json
[
  {
    "id": "23",
    "name": "Faculty of Physics and Chemistry"
  }
]  
```

Name | Type | Description
--- | ------------ | --------
id | number | Faculty ID
name | string | Faculty name

## Errors

* `404 Not Found` – non-existent college or university selected
