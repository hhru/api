# List of regions with active vacancies

To filter the list of active vacancies, you can indicate a region in the `area`
parameter. `GET /employers/{employer_id}/vacancy_areas/active` will show the
list of regions that currently have active vacancies.

An example of a successful response:

```json
{
    "found": 1,
    "items": [
        {
            "id": "1",
            "name": "Moscow"
        }
    ],
    "page": 0,
    "pages": 1,
    "per_page": 1
}
```

As opposed to the region directory (`/areas`), this list is a flat, non-treeview
list. It only contains the tree "leaves", without any "embedded" region objects.

### Errors

* `403 Forbidden` – authorization is failed.
