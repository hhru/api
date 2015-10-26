# Suggestions

When filling out experience fields, we recommend using suggestion features
(autocomplete, autosuggest). At the moment, available suggestions cover names of
universities, faculties, companies, specializations.

All suggestions work in the same way: they receive text that is a part of the
suggested meaning, and return a list of relevant elements. The text being
searched must contain at least two symbols. In case too short a text is given,
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

Some suggestions take the `locale` mandatory element – a language of
suggestions; the list of available languages is similar to the list of CV
languages and is available on <https://api.hh.ru/locales/resume>. In case a
suggestion needs a language but it has not been given in the query, `RU` is used
by default. If an unsupported language is given, the `400 Bad Request`
error will be returned, with a detailed error description in the response body:

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
* [Region suggestions](#areas)
* [Resume search keyword suggestions](#resume-search-keyword)
* [Vacancy search keyword suggestions](#vacancy-search-keyword)


<a name="educational_institutions"/>
## University name suggestions

In order to obtain university name options from the inserted symbols, you should
send a GET request to `/suggests/educational_institutions` with the following
parameters:

* `text` – a text for searching a university
* `locale` – a suggestion language

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


<a name="companies" />
## Organization suggestions


To receive suggestions on organizations, you should send a
`GET /suggests/companies` request with the following parameters:

* `text` – a text for searching
* `locale` – a suggestion language

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
        "90": "http://hh.ru/employer-logo/289055.png"
      }
    }
  ]
}
```

The data from this suggestion can be used to select a company in work experience
when [working with CVs](resumes.md#create_edit). If you need to search by
companies (employers) that can post vacancies, use the [search by
companies](employers.md#search).



<a name="specializations" />
## Specialization suggestions

To see the list of relevant specializations, you should send a
`GET` request to `/suggests/fields_of_study` with the following parameters:

* `text` – a text for searching specializations
* `locale` – a suggestion language.

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


<a name="key-skills" />
## Key skills suggestions

In order to obtain a suggestion on key skills, you should send a `GET` request
to `/suggests/skill_set` with the mandatory parameter `text`,

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


<a name="positions" />
## Position suggestions

In order to obtain a suggestion on positions, you should send a `GET` request to
`/suggests/positions` with the mandatory parameter `text` – a key skill search
string. We recommend using this data when creating a CV or a vacancy. We remind
that when a CV is created, the user can indicate no more than three
specializations, and all of them must be from the same professional area.

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
          "profarea_id": "26",
          "profarea_name": "Procurement"
        }
      ]
    }
  ]
}
```

<a name="areas" />
## Region suggestions

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/suggests.md.html#areas)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="resume-search-keyword" />
## Resume search keyword suggestions

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/suggests.md.html#resume-search-keyword)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).


<a name="vacancy-search-keyword" />
## Vacancy search keyword suggestions

Documentation translation for this section is in progress.
See
[machine translation](https://z5h64q92x9.net/proxy_u/ru-en.en/http/hhru.github.io/api/rendered-docs/docs/suggests.md.html#vacancy-search-keyword)
powered by
[Yandex.Translate](https://translate.yandex.com/translate).
