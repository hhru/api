# Statistics on working with responses

* [Employer statistics](#employer-stats)
* [Manager statistics](#manager-stats)

You must be authorized as an employer to obtain information.
A response `403 Forbidden` will be returned if the user is unauthorized or incorrectly authorized.

<a name="employer-stats"></a>
## Employer statistics

### Request

```
GET /employers/{employer_id}/negotiations_statistics
```

where `employer_id` - Employer ID that can be obtained from the [information on the current user](me.md#employer-info).


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "employer_statistics": {
        "received": 20,
        "viewed_percent": 23,
        "viewed_percent_change": 10,
        "replied_percent": 0,
        "replied_percent_change": -15,
        "average_reply_time": 1.0
    }
}
```

The object `employer_statistics` includes the following fields:

Name | Type | Description
--- | --- | --------
received | number | number of responses to employer jobs received in the last `30 days` (the "Period")
viewed_percent | number or null | percentage of read responses to the employer's jobs for the Period, or `null` if there are no responses
viewed_percent_change | number or null | difference between the current viewed_percent value compared to the previous Period, or `null` if there are no responses
replied_percent | number or null | percentage of responses to employer jobs that have been moved to any other [collection](employer_negotiations.md#term-collection) and accompanied by messages for a Period, or `null` if there are no responses 
replied_percent_change | number or null | difference between the current replied_percent value compared to the previous Period, or `null` if there are no responses
average_reply_time | number or null | average time in days between receiving a response to an employer job and sending a message, or `null` if no messages were sent


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
  the [information on the current user](me.md#employer-info).
* `manager_id` - manager ID.

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "manager_statistics": {
        "received": 20,
        "viewed_percent": 23,
        "viewed_percent_change": 10,
        "replied_percent": 0,
        "replied_percent_change": -15,
        "average_reply_time": 1.0
    }
}
```

### Errors

* `404 Not found` - the employer or manager was not found, or the user does not have the appropriate privileges.
Manager statistics are available to the manager, as well as to managers with the `main_contact_person` [type](employer_managers.md#dict).

The `manager_statistics` object includes the following fields:

Name | Type | Description
--- | --- | --------
received | number | number of responses to manager jobs received in the last `30 days` (the "Period")
viewed_percent | number или null | percentage of read responses to the manager's jobs for the Period, or `null` if there are no responses
viewed_percent_change | number или null | difference between the current viewed_percent value compared to the previous Period, or `null` if there are no responses
replied_percent | number или null | percentage of responses to manager jobs that have been moved to any other [collection](employer_negotiations.md#term-collection) and accompanied by messages for a Period, or `null` if there are no responses 
replied_percent_change | number или null | difference between the current replied_percent value compared to the previous Period, or `null` if there are no responses
average_reply_time | number или null | average time in days between receiving a response to a manager job and sending a message, or `null` if no messages were sent
