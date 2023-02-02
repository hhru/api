# Website selection

HeadHunter API allows you to obtain data from all of the HeadHunter group of
companies websites.

In particular:

* hh.ru
* rabota.by
* hh1.az
* hh.uz
* hh.kz
* headhunter.ge
* headhunter.kg

Requests for data on all the websites should be made to `https://api.hh.ru/`.

If you need to track the specific websites, you can add `?host=` parameter to
your request. Default is `hh.ru`.

Example: to obtain [localizations](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-locales) available on hh.kz, you should
make a GET-request to `https://api.hh.ru/locales?host=hh.kz`.
