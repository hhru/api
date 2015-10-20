# Locales

In any request to the API, you can indicate the `?locale=` parameter to give the
value of the locale (language).

`GET /locales` returns the list of possible values (available locales) in the
id field.


```json
[
    {
        "id": "RU",
        "name": "Russian"
    },
    {
        "id": "EN",
        "name": "English"
    }
]
```

The directory may have other values.

Example: [https://api.hh.ru/locales?locale=EN](https://api.hh.ru/locales?locale=EN)


## Resume locales

`GET /locales/resume` returns the directory of possible resume locales.
The subcollection of the locale directory.

By changing a locale you can, for example, create a CV in English.

Example: [https://api.hh.ru/locales/resume?locale=EN](https://api.hh.ru/locales/resume?locale=EN)

