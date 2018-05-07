# Employer's test directory

To learn the list of employer's saved tests, you should send the `GET` request
to `/employers/{employer_id}/tests`.

This directory is available only for employers.

If the request is performed successfully, the status `HTTP 200 OK`
will be returned. The employer's test list will be returned in the response
body, for example:

```json
{
    "items": [
        {
            "id": "75169",
            "name": "Basic test of C++ knowledge"
        }, {
            "id": "75168",
            "name": "Logical test"
        }
    ]
}
```

The `items` element contains the list of employer's tests.
Each element from `items` has the following fields:

| Name | Type   | Description     |
|------|--------|-----------------|
| id   | string | Test identifier |
| name | string | Test title      |

### Errors

* `403 Forbidden` - the current user is not allowed to view the employer's tests.
* `404 Not Found` - the employer is not found.
