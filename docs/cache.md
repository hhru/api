# Кэширование

В некоторых методах API имеется возможность кэширования ответов на стороне
клиента по заголовкам `Etag`, `Cache-Control` и `Expires`.


Если при запросе ресурса в API, был возвращён заголовок `Etag`, например,
запрос:

```
GET /areas/1 HTTP/1.1
Host: api.hh.ru
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

вернул ответ:

```
HTTP/1.1 200 OK
Etag: W/"ai-356a192-57E047847BCE15-RU10e33"
Content-Type: application/json; charset=UTF-8
Content-Length: 61
Expires: Tue, 03 Oct 2017 07:01:04 GMT
Cache-Control: max-age=1200

{
    "areas": [],
    "id": "1",
    "name": "Москва",
    "parent_id": "113"
}
```

Клиент может запомнить значение заголовка `Etag` вместе с данными ответа и в
следующий раз, когда будет необходим данный ресурс, запросить информацию
об изменении ресурса, передав значение `Etag` в заголовке `If-None-Match`:

```
GET /areas/1 HTTP/1.1
Host: api.hh.ru
If-None-Match: W/"ai-356a192-57E047847BCE15-RU10e33"
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

Если ресурс не поменялся, вернётся ответ с кодом `304 Not Modified`, не
содержащий тела:

```
HTTP/1.1 304 Not Modified
Etag: W/"ai-356a192-57E047847BCE15-RU10e33"
Cache-Control: max-age=1200
Expires: Tue, 03 Oct 2017 07:05:43 GMT
```

Если ресурс изменился, вернётся новое содержание ресурса:

```
HTTP/1.1 200 OK
Etag: W/"ai-34e7018-356a192b7913b0-RU73fda"
Content-Type: application/json; charset=UTF-8
Expires: Tue, 03 Oct 2017 07:10:31 GMT
Cache-Control: max-age=1200

{
    "areas": [],
    "id": "1",
    "name": "Москва",
    "parent_id": "777"
}
```

При проверке по `Etag` возможно использование HEAD запроса, он будет работать
аналогично, но даже в случае, если ресурс изменился, будет возвращены только
заголовки без тела ответа.

Кроме того, при запросе ресурса, в ответе есть заголовки `Cache-Control` и
`Expires`, которые позволяют клиенту закэшировать ответ и использовать его до
истечения указанного срока действия.

Более подробно в [RFC-7232](https://tools.ietf.org/html/rfc7232).


Кэширование поддерживается большинством
[справочников](../README.md#dictionaries). Определить поддержку можно по наличию
заголовка `Etag` в ответе.
