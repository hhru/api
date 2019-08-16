# Адрес

Поле адрес используется в различных ответах API, например, в резюме, откликах,
при просмотре вакансии. Может содержать в себе долготу, широту, информацию о
ближайших станциях метро и другую информацию о местонахождении. Выглядит
следующим образом:

```json
{
    "city": "Москва",
    "street": "улица Годовикова",
    "building": "9с10",
    "description": "на проходной потребуется паспорт",
    "lat": 55.807794,
    "lng": 37.638699,
    "metro_stations": [
        {
            "station_id": "6.8",
            "station_name": "Алексеевская",
            "line_id": "6",
            "line_name": "Калужско-Рижская",
            "lat": 55.807794,
            "lng": 37.638699
        }
    ]
}
```

Имя | Тип | Описание
---- | --- | --------
city | string или null | Город
street | string или null | Улица
building | string или null | Номер дома
description | string или null | Дополнительная информация об адресе
lat | number или null | Географическая широта
lng | number или null | Географическая долгота
metro_stations | array | Список станций метро
metro_stations[].station_id | string | Идентификатор станции метро
metro_stations[].station_name | string | Название станции метро
metro_stations[].line_id | string | Идентификатор линии метро, на которой находится станция
metro_stations[].line_name | string | Название линии метро, на которой находится станция
metro_stations[].lat | number или null | Географическая широта станции метро
metro_stations[].lng | number или null | Географическая долгота станции метро


