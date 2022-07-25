# Hidden vacancies

Applicants can "hide" specific or all vacancies
from a specific employer. These vacancies will not be returned when
[searching by vacancies](vacancies.md#search).


<a name="vacancies"></a>
## Vacancies

`GET /vacancies/blacklisted` returns a [subset of vacancies](vacancies.md#search) hidden by the user.
Authorisation is required, otherwise it will return `403 Forbidden.` Pagination works with the standard `page & per_page`;
pages are numbered from `0.` In addition, the `"limit_reached": true/false` key is returned in the root object, which
indicates whether the maximum number of items in the list is exceeded.

`PUT /vacancies/blacklisted/{vacancy_id}` adds the selected vacancy to the list of hidden. This operation is idempotent:
if you add a vacancy that is already in the list `204 No Content`, the server will return the same result as when it was first added.
If the vacancy is not found, the server will return `404 Not Found`. If for some reason you do not have sufficient rights to add
a vacancy to the list — `403 Forbidden`. If the allowed number of items in the list is exceeded — `400 Bad Arguments`.
In addition to the HTTP code, the server can return a description of the [error reason](errors.md#vacancies_blacklist).

`DELETE /vacancies/blacklisted/{vacancy_id}` will delete the vacancy from the list of authorised users.
This operation is idempotent. After successful deletion, the method returns `204 No Content.`


<a name="employers"></a>
## All vacancies from an employer

In addition to adding individual vacancies, it is possible to add all vacancies from a particular company.

`GET /employers/blacklisted` returns a [subset of employers](https://api.hh.ru/openapi/en/redoc#tag/Employer/paths/~1employers/get) hidden by the user.
Authorisation is required, otherwise it will return `403 Forbidden`. Pagination is available; pages are numbered from '0.'
In addition, the `"limit_reached": true/false` key is returned in the root object, which indicates whether
the maximum number of items in the list is exceeded. 

`PUT /employers/blacklisted/{employer_id}` the specified employer will be added to the list. This operation is idempotent. If
the employer was not found, the server will return `404 Not Found`. If for some reason you do not have sufficient privileges to add
an employer to the list — `403 Forbidden`. If the allowed number of items in the
list is exceeded — `400 Bad Arguments`. 

In addition to the HTTP code, the server can return a description of the [error reason](errors.md#employers_blacklist).

`DELETE /employers/blacklisted/{employer_id}` the employer will be deleted from the the authorised user's list of hidden companies.
This operation is idempotent. After successful deletion, the method returns `204 No Content`.
