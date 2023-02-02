# Выбор сайта

API HeadHunter позволяет получать данные со всех сайтов группы компании
HeadHunter.

В частности:

* hh.ru
* rabota.by
* hh1.az
* hh.uz
* hh.kz
* headhunter.ge
* headhunter.kg

Запросы к данным на всех сайтах следует направлять на `https://api.hh.ru/`.

При необходимости учесть специфику сайта, можно добавить в запрос параметр
`?host=`. По умолчанию используется `hh.ru`.

Например, для получения [локализаций](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-locales), доступных на hh.kz необходимо
сделать GET запрос на `https://api.hh.ru/locales?host=hh.kz`.
