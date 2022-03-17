# Vacancy drafts

* [getting a list of vacancy drafts](#draft_list)
* [deleting a draft](#draft_delete)
* [publishing a vacancy from draft](#draft_publish)

<a name="draft_list"></a>
## Getting a list of vacancy drafts

A request for retrieval of available vacancy drafts for the current manager. If the manager has multiple work accounts,
they can use any of them according to the instructions on [manager work accounts](manager_accounts.md).

### Request:

```GET /vacancies/drafts```

Additional request parameters:
* [pagination parameters `page` and `per_page`](general.md#pagination)


### Response

A successful response will return the `200 OK` status code. The response body will contain information on
available drafts:

```json
{
  "items": [
    {
      "areas": [
        {
          "id": "4786",
          "name": "Artyshta"
        },
        {
          "id": "4787",
          "name": "Bachatsky"
        },
        {
          "id": "1231",
          "name": "Belovo"
        }
      ],
      "completed_fields_percentage": 100,
      "draft_id": "1110032",
      "insufficient_publications": [
        {
          "publication_type": "standard",
          "vacancy_type": "open",
          "count": 2
        }
      ],
      "insufficient_quotas": [
        {
          "publication_type": "standard",
          "vacancy_type": "open",
          "count": 1
        }
      ],
      "last_change_time": "2021-05-18T11:20:48+03:00",
      "name": "Head of Retail Department",
      "publication_ready": true,
      "publication_type": "standard",
      "vacancy_type": "open",
      "required_publications": [
        {
          "publication_type": "standard",
          "vacancy_type": "open",
          "count": 3
        }
      ],
      "auto_publication": null
    },
    {
      "areas": [
        {
          "id": "2842",
          "name": "Balykchy"
        }
      ],
      "completed_fields_percentage": 100,
      "draft_id": "1110031",
      "insufficient_publications": null,
      "insufficient_quotas": null,
      "last_change_time": null,
      "name": "Supervisor,",
      "publication_ready": true,
      "publication_type": "standard_plus",
      "vacancy_type": "open",
      "required_publications": null,
      "auto_publication": {
        "bill_uid": "4011054/3",
        "cart_id": "5967030"
      }
    }
  ],
  "found": 2,
  "page": 0,
  "pages": 1,
  "per_page": 20
}
```

Name| Type |Description
---- | --- | --------
found | number | Number of drafts found
pages | number | Number of pages with drafts
per_page | number | Number of items per page
page | number | Current page number
items | array | List of drafts

where for each item `items`:

<a name="item"></a>

Name | Type | Description
---- | --- | --------
id | string | Draft ID
name | string | Vacancy name
publication_type | string | Publication type (directory [vacancy_billing_type](dictionaries.md))
vacancy_type | string | Vacancy type (directory[vacancy_type](dictionaries.md))
areas | array | Region codes and names (federal districts, federal subjects, cities).
completed_fields_percentage | number | Percentage of completed fields in a draft
insufficient_publications | array or null | An array [of objects](#publications) with information on the missing publications in the account that are required to publish a vacancy using this draft.
insufficient_quotas | array or null | An array [of objects](#publications) with information on exceeded quotas.
required_publications | array или null | An array [of objects](#publications) with information on the required publications in the account
last_change_time | string or null | Draft modification time (in the following format: [ISO 8601](../general.md#date-format) with second precision `YYYY-MM-DDThh:mm:ss±hhmm`)
publication_ready | boolean  | Is the draft ready to be published?
auto_publication | object or null | Auto-publishing status. [Object](#auto_publication_state) if this feature is enabled, otherwise null.

<a name="auto_publication_state"></a>
With auto-publishing enabled, when the payment is received for the invoice number indicated in the object,
the vacancy based on this draft will be published automatically.   
`Autopublication status` object format

Name | Type | Description
---- | --- | --------
bill_uid | string | Invoice number
cart_id | string | Order ID

<a name="publications"></a>
Object format with the number of publications

Name | Type | Description
---- | --- | --------
publication_type | string | Publication type (directory [vacancy_billing_type](https://github.com/hhru/api/blob/master/docs_eng/dictionaries.md))
vacancy_type | string | Vacancy type (directory [vacancy_type](dictionaries.md))
count | number |Quantity

### Errors

* `403 Forbidden` — the current user is not an employer

<a name="draft_delete"></a>
## Deleting a draft

### Request

```DELETE /vacancies/drafts/{draft_id}```

A successful response will return the `204 No Content` status code.

### Errors

* `403 Forbidden` — the current user is not an employer
* `404 Not Found` — the draft is not found or the user does not have permission to delete the draft


<a name="draft_publish"></a>

## Publishing a vacancy from draft

``` POST /vacancies/drafts/{draft_id}/publish```

You can also specify optional query parameters:

* `ignore_duplicates=true` — force
  [adding a duplicate](employer_vacancies.md#creation-ignore-duplicates).

* `with_professional_roles=true` — to publish a vacancy from draft with professional roles instead of specializations

When you set the `with_professional_roles=true` parameter, the `specializations` field is no longer mandatory and will be ignored, while the `professional_roles` field becomes mandatory.

A request to publish a vacancy from draft according to its draft_id. The request will result in a list of vacancies equal to the number of cities in the draft (one or more). This will delete the draft.

Rules for publishing a vacancy and other useful information can be found in the following section: [Vacancies for employer](employer_vacancies.md)

### Response

A successful response will return the `201 Created`status code.

```
HTTP/1.1 201 Created

```

The response body contains an array of published vacancies' IDs:

```json
{
    "vacancy_ids": [78789890, 78789891, 78789892]
}
```

### Errors

* `400 Bad Request` – errors in filling out the fields when adding a vacancy.
* `403 Forbidden` – this user is not allowed to create vacancies.
* <a name="creation-ignore-duplicates"></a> `403 Forbidden` –
  a vacancy can not be added, since a vacancy with similar
  data has already been published by this employer. If you are sure
  that duplication is necessary, add the following parameter to the request:
  `POST /vacancies/drafts/{draft_id}/publish?ignore_duplicates=true`.
* `404 Not Found` — the draft is not found

In addition to the HTTP code, the server may return a description for
[root causes of the error](errors.md#vacancies-create-n-edit).

