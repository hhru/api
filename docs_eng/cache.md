# Caching

Some API methods have the option to cache responses on the client
side by headers `Etag`, `Cache-Control` and `Expires`.


If `Etag` is returned when requesting a resource in API, for example,
the request:

```
GET /areas/1 HTTP/1.1
Host: api.hh.ru
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

returned the answer:

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

The client can remember the meaning of `Etag` with the response data and
next time when this resource is needed, request information
about changes in the resource by sending `Etag` value in the header `If-None-Match`:

```
GET /areas/1 HTTP/1.1
Host: api.hh.ru
If-None-Match: W/"ai-356a192-57E047847BCE15-RU10e33"
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

If the resource has not changed, it will return a response with a code `304 Not Modified`
and without a body:

```
HTTP/1.1 304 Not Modified
Etag: W/"ai-356a192-57E047847BCE15-RU10e33"
Cache-Control: max-age=1200
Expires: Tue, 03 Oct 2017 07:05:43 GMT
```

If the resource changes, it will return new contents of the resource:

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

The HEAD request can be used when checking by `Etag`; it will work
similarly, but even if the resource has changed, it will return only
headers without a response body.

In addition, when requesting the resource, the response contains headers `Cache-Control` and 
`Expires` for the client to cache the response and use it before the indicated expiration date.

More details in [RFC-7232](https://tools.ietf.org/html/rfc7232).

Caching is supported by the majority of [directories](README.md#dictionaries). 
You can determine support by the presence of `Etag` in the response.
