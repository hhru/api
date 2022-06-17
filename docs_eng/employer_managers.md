# Employer's managers

* [Directory of manager types and privileges](#dict)
* [Adding a manager](#add)
* [Editing a manager](#edit)
* [Deleting a manager](#delete)
* [Directory of employer's managers](#list)
* [Getting information about a manager](#item)

You must be authorised as an employer to obtain information.
A response `403 Forbidden` will be returned if the user is unauthorised or incorrectly authorised.


<a name="dict"></a>
## Directory of manager types and privileges

> Attention! The values in the directories may change at any time. Do not address them directly.

### Request
>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/paths/~1employers~1{employer_id}~1manager_types/get) specification.


<a name="add"></a>
## Adding a manager
>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/paths/~1employers~1%7Bemployer_id%7D~1managers/post) specification.

<a name="edit"></a>
## Editing a manager
>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/paths/~1employers~1%7Bemployer_id%7D~1managers~1%7Bmanager_id%7D/put) specification.


<a name="delete"></a>
## Deleting a manager

Deleting a manager is not immediate and can take a while.
This is why if you request a list of managers **immediately** after successfully deleting a manager the response may include the deleted manager.

### Request

`DELETE /employers/{employer_id}/managers/{manager_id}`

where:

* `employer_id` - Employer ID that can be obtained from the [information on the current user](https://api.hh.ru/openapi/en/redoc#tag/Employer-info/paths/~1me/get).
* `manager_id` - Manager ID.

As a mandatory parameter you must include: `successor_id` — ID of the manager who will receive all data related 
to the deleted manager, in particular: vacancies, applications, files with selected resumes, comments on candidates, automatic searches.

### Response

A successful response contains a code `204 No Content`.

### Errors

* `404 Not Found` – the employer or manager you specified does not exist or the user does not have enough rights to delete
                    this manager
* `400 Bad Request` – parameters in the input JSON contain an error. The system will return the error description in the body.
                      Unknown parameters and parameters with errors in the names are ignored.
* `403 Forbidden`– incorrect authorisation or other reasons to cancel manager deletion

<a name="list"></a>
## Directory of employer's managers

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Employer-managers/paths/~1employers~1{employer_id}~1managers/get)

<a name="item"></a>
## Getting information about a manager

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/paths/~1employers~1{employer_id}~1managers~1{manager_id}/get)
