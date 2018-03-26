# Suggestions

When filling in the experience and education fields, it is recommended to use
the tips services (autocomplete, autosuggest).

All suggestions work in the same way: they receive text that is a part of the
suggested meaning, and return a list of relevant elements. The text being
searched must contain at least two and less than 3 000 symbols. In case too short or too long a text is given,
`400 Bad Request` will be returned with the error description in the
response body:


```json
{
  "errors": [
    {
      "type": "bad_argument",
      "value": "text"
    }
  ]
}
```

Some tips accept the required element `locale` – the tip language. Supported
languages: `RU`, `EN`, `UA`, `AZ`, `KZ`. In case the tip requires a language,
but it was not included in the request, `RU` language will be used. If an
unsupported language is specified, the `400 Bad Request` error will be
returned with detailed error description in the response body:

```json
{
  "errors": [
    {
      "type": "bad_argument",
      "value": "locale"
    }
  ]
}
```

* [University name suggestions](#educational_institutions)
* [Organization suggestions](#companies)
* [Specialization suggestions](#specializations)
* [Key skills suggestions](#key-skills)
* [Position suggestions](#positions)
* [Region tips](#areas)
* [Tips for vacancy search key words](#vacancy-search-keyword)


<a name="educational_institutions"></a>
## University name suggestions

### Request

In order to obtain university name options from the inserted symbols, you should
send a GET request to `/suggests/educational_institutions` with the following
parameters:

* `text` – a text for searching a university
* `locale` – a suggestion language

### Response

If the request is performed successfully, such a JSON will be returned:

```json
{
  "items": [
    {
      "acronym": "Bauman MSTU",
      "text": "Bauman Moscow State Technical University, Moscow",
      "synonyms": "formerly Bauman MHTS",
      "id": "38921",
      "area": {
        "id": "1",
        "name": "Moscow"
      }
    }
  ]
}
```

The `acronym` and `synonym` fields may be null.

To see the list of college faculties, you can use the
[method of obtaining faculties](faculties.md).


<a name="companies"></a>
## Organization suggestions

### Request

To receive suggestions on organizations, you should send a
`GET /suggests/companies` request with the following parameters:

* `text` – a text for searching
* `locale` – a suggestion language

### Response

If the request is performed successfully, such a response will be returned:

```json
{
  "items": [
    {
      "text": "HeadHunter",
      "id": "1455",
      "url": "http:/hh.ru",
      "industries": [
        {
          "id": "7.541",
          "name": "Internet company"
        }
      ],
      "logo_urls": {
        "90": "https://hh.ru/employer-logo/289055.png"
      }
    }
  ]
}
```

The data from this suggestion can be used to select a company in work experience
when [working with CVs](resumes.md#create_edit). If you need to search by
companies (employers) that can post vacancies, use the [search by
companies](employers.md#search).



<a name="specializations"></a>
## Specialization suggestions

### Request

To see the list of relevant specializations, you should send a
`GET` request to `/suggests/fields_of_study` with the following parameters:

* `text` – a text for searching specializations
* `locale` – a suggestion language.

### Response

If the request is performed successfully, such a response will be returned:

```json
{
  "items": [
    {
      "id": "382",
      "text": "Refrigerating, cryogenic technology and air conditioning (engineer)"
    }
  ]
}
```


<a name="key-skills"></a>
## Key skills suggestions

### Request

In order to obtain a suggestion on key skills, you should send a `GET` request
to `/suggests/skill_set` with the mandatory parameter `text`.

### Response

If the request is performed successfully, such a response will be returned:

```json
{
  "items": [
    {
      "text": "Heat and refrigeration supply systems",
      "id": "2716"
    },
    {
      "text": "Cold shop",
      "id": "3019"
    },
    {
      "text": "Cold calling",
      "id": "3018"
    }
  ]
}
```


<a name="positions"></a>
## Position suggestions

### Request

In order to obtain a suggestion on positions, you should send a `GET` request to
`/suggests/positions` with the mandatory parameter `text` – a key skill search
string. We recommend using this data when creating a CV or a vacancy. We remind
that when a CV is created, the user can indicate no more than three
specializations, and all of them must be from the same professional area.

### Response

If the request is performed successfully, such a response will be returned:

```json
{
  "items":[
    {
      "text": "Business Development Manager",
      "id": "2569",
      "specializations": [
        {
          "id": "17.149",
          "name": "Customer relationship manager",
          "profarea_id": "17",
          "profarea_name": "Procurement"
        }
      ]
    }
  ]
}
```


<a name="areas"></a>
## Region tips

### Request

`GET /suggests/areas` – tip for all regions.

`GET /suggests/area_leaves – tip for all regions that are leaves in the region
`tree.

Both tips accept the following parameters:

* `text` – text for searching a region
* `locale` – tip language

In addition to the region tip, load of the [full region tree](areas.md#areas)
and [a part of the tree from a specific element](areas.md#item) is available.

### Response

```json
{
  "items": [
    {
      "url": "https://api.hh.ru/areas/1",
      "text": "Moscow",
      "id": "1"
    },
    {
      "url": "https://api.hh.ru/areas/2019",
      "text": "Moscow Region",
      "id": "2019"
    }
  ]
}
```


<a name="vacancy-search-keyword"></a>
## Tips for vacancy search key words

### Request

This tip is intended for use in the `text` field when
[searching for vacancies](vacancies.md#search). The tip displays title names,
company names, and other phrases that are often used when searching
for vacancies.

`GET /suggests/vacancy_search_keyword`

Parameters:

* `text` – text for searching a keyword


### Response

```json
{
  "items": [
    {
      "text": "Java"
    },
    {
      "text": "JavaScript"
    },
    {
      "text": "Java programmer"
    }
  ]
}
```
