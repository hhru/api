# Statistics on working with responses

* [Employer statistics](#employer-stats)
* [Manager statistics](#manager-stats)

You must be authorized as an employer to obtain information.
A response `403 Forbidden` will be returned if the user is unauthorized or incorrectly authorized.
Manager statistics are available to the manager, as well as to managers with the `main_contact_person` [type](employer_managers.md#dict).

<a name="employer-stats"></a>
## Employer statistics

### Request

```
GET /employers/{employer_id}/negotiations_statistics
```

where `employer_id` - Employer ID that can be obtained from the [information on the current user](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-current-user-info).


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "employer_statistics": {
        "received": 20,
        "viewed_percent": 23,
        "replied_percent": 0,
        "average_reply_time": 1.0,
        "politeness": {
            "index": 62,
            "index_change": 0,
            "hint": "You have a medium value of politeness index. This is good, but you can increase it.",
            "description": "An applicant see the politeness index after he has been responded to a vacancy. The companies with low politeness index lose the applicants trust and may miss suitable candidates.",
            "article_url": "https://hh.ru/article/23734"
        }
    }
}
```

<a name="employer_statistics_field"></a>
#### The object `employer_statistics`

Name | Type | Description
--- | --- | --------
received | number | number of responses to employer jobs received in the last `30 days` (the "Period")
viewed_percent | number or null | percentage of read responses to the employer's jobs for the Period, or `null` if there are no responses
replied_percent | number or null | percentage of responses to employer jobs that have been moved to any other [collection](employer_negotiations.md#term-collection) and accompanied by messages for a Period, or `null` if there are no responses 
average_reply_time | number or null | average time in days between receiving a response to an employer job and sending a message, or `null` if no messages were sent
politeness | object or null | [The object `politeness`](#employer_politeness_field) or `null`, if company [politeness index](https://hh.ru/article/23734)  is not calculated, for example,  the company has no vacancies or responses

<a name="employer_politeness_field"></a>
#### The object `politeness` for the company

Contains information about company [politeness index](https://hh.ru/article/23734).

Name | Type | Description
-----|-----|----------
index | number | company politeness index 
index_change | number | Attention! This param is deprecated, because politeness index is calculated in runtime
hint | string | description about current value of politeness index
description | string | short information about politeness index 
article_url | string | url of orticle about politeness index 

### Errors

* `404 Not found` - The employer was not found, or the user does not have the appropriate privileges

<a name="manager-stats"></a>
## Manager statistics

### Request

```
GET /employers/{employer_id}/managers/{manager_id}/negotiations_statistics
```

where:
* `employer_id` - employer ID that can be obtained from
  the [information on the current user](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/operation/get-current-user-info).
* `manager_id` - manager ID.

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "manager_statistics": {
        "received": 20,
        "viewed_percent": 23,
        "replied_percent": 0,
        "average_reply_time": 1.0,
        "politeness": {
            "index": 19,
            "index_change": 0,
            "hint": "You have a low value of politeness index, but You can increase it",
            "description": "An applicant see the politeness index after he has been responded to a vacancy. The companies with low politeness index lose the applicants trust and may miss suitable candidates.",
            "article_url": "https://hh.ru/article/23734"
        }
    }
}
```

<a name="manager_statistics_field"></a>
#### The object `manager_statistics`

Name | Type | Description
--- | --- | --------
received | number | number of responses to manager jobs received in the last `30 days` (the "Period")
viewed_percent | number или null | percentage of read responses to the manager's jobs for the Period, or `null` if there are no responses
replied_percent | number или null | percentage of responses to manager jobs that have been moved to any other [collection](employer_negotiations.md#term-collection) and accompanied by messages for a Period, or `null` if there are no responses 
average_reply_time | number или null | average time in days between receiving a response to a manager job and sending a message, or `null` if no messages were sent
politeness | object or null | [The object `politeness`](#manager_politeness_field) or `null`, if manager [politeness index](https://hh.ru/article/23734)  is not calculated, for example, the manager has no vacancies or responses

<a name="manager_politeness_field"></a>
#### The object `politeness` for the manager

Contains information about manager [politeness index](https://hh.ru/article/23734). 

Name | Type | Description
-----|-----|----------
index | number | manager politeness index 
index_change | number | Attention! This param is deprecated, because politeness index is calculated in runtime
hint | string | description about current value of politeness index
description | string | short information about politeness index 
article_url | string | url of orticle about politeness index 

### Errors

* `404 Not found` - the employer or manager was not found, or the user does not have the appropriate privileges.
