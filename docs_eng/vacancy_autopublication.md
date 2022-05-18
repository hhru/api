# Automatic publishing of vacancies

When auto publishing is active for a draft, this means that payment is pending for an invoice linked with the draft. When the payment
has cleared, the vacancy from the draft will be published automatically. To get information about the active auto publications,
refer to the [draft information resource](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft).

## Canceling automatic publication of a vacancy from draft

### Request

```DELETE /vacancies/auto_publication?draft_id=123456```

where `draft_id` is the draft's ID.

### Response

A successful response comes with the code `204 No Content`.

### Errors

* `403 Forbidden` — current user is not the employer
* `404 Not Found` — where the draft cannot be found or the user has no editing rights for the draft
