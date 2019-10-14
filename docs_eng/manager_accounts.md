# Manager work accounts

A Manager may perform actions on behalf of several employers. To interact with API for the purposes of a particular employer, you should use the appropriate Work Account (in site terminology – Implants). 
A User may have multiple Work Accounts, one of which is the primary account. To learn which of the accounts is the primary one, 
get a [list of Manager Work Accounts](#get-manager-accounts). The primary account is used if you send only a token for login 
(learn more [here](#using-account)).

* [Getting a list of User Work Accounts](#get-manager-accounts)
* [Account selection upon request](#using-account)

<a name="get-manager-accounts"></a>
## Getting a list of User Work Accounts

### Request

```
GET /manager_accounts/mine
```

### Response

A successful response contains the code `200 OK` and a body:

```json
{
    "items": [
        {
            "id": "1",
            "employer": {
                "id": "12345678",
                "name": "Alpha Corp."
            }
        },
        {
            "id": "2",
            "employer": {
                "id": "87654321",
                "name": "Beta Inc."
            }
        }
    ],
    "current_account_id": "2",
    "primary_account_id": "1",
    "is_primary_account_blocked": false
}
```

where:

Name | Type | Description
--- | --- | ------
items | list | list of User [Work Accounts](#account-info)
current_account_id | line | Current Work Account ID (same as the value in the header)
primary_account_id | line | Primary Work Account ID
is_primary_account_blocked | logical | is Primary Account blocked

<a name="account-info"></a>
#### `account` object

Name | Type | Description
--- | --- | ------
id | line | Work Account ID
employer | object | [information on company](#employer-info) to which the Work Account is assigned

<a name="employer-info"></a>
#### `employer` object

Name | Type | Description
--- | --- | ------
 id | line | Company ID
 name | line | Company name

### Errors

* `403 Forbidden` – Login Error (User is not a Manager)


<a name="using-account"></a>
## Account selection upon requests

To work on a particular account, you need to send `account_id` value from the [list](#get-manager-accounts) in the header:

```
X-Manager-Account-Id: {account_id}
```

You may use this header in all the methods available for employers.

In the absence of the header, your header may also send `account_id` of the Primary Account, which is also implied by default.


<a name="errors"></a>
## Errors

* `403 Forbidden` – Work Account with the sent `account_id` not found. [Error cause](errors.md#manager-accounts) will be generated additionally to the code
* `403 Forbidden` – login error (upon login requests of non-employers)
