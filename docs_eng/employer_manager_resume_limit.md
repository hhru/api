# Manager's limits 
 
* [Daily limit of resume views for current manager](#resume_limit)
 
<a name="resume_limit"></a>
## Daily limit of resume views for current manager
 
### Request
`GET /employers/{employer_id}/managers/{manager_id}/limits/resume`
 
 where `employer_id` is the employer ID, which you can find in [information on the current employer](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/paths/~1me/get).
 where `manager_id` is the manager ID, which you can find in [information on the current user](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/paths/~1me/get).
 
### Response
 
Response example:
```json
{
    "limits": {
        "resume_view": 100
    },
    "spend": {
        "resume_view": 1
    },
    "left": {
        "resume_view": 50
    }
}
```
 
 Name | Type | Description
 --- | --- | ---
 limits | object | limits 
 limits.resume_view | integer | limit for resume views
 spend | object | current values of spending
 spend.resume_view | integer | number of viewed resumes
 left | object | remaining values
 left.resume_view | integer | number of remaining resume views. This value includes the limit of views for the company. As a result, it may be lower than the number of views available to the current user.
 
### Errors
* `404 Not found` - The employer or manager was not found or the user does not have the appropriate privileges
* `403 Forbidden` - Incorrect authorisation
