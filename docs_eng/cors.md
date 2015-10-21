# Cross-Origin Resource Sharing (CORS)

API supports the CORS technology for requesting browser data from any domain.
This method is preferable to JSONP. Moreover, unlike JSONP, it is not limited by
the GET method.

To debug requests using CORS, a special URL is available in API: `/cors`. It
supports the HEAD, GET, POST, PUT, DELETE methods. A request with any of these
methods will return the standard response:

```json
{
    "method": "GET",
    "time": "2013-11-18T13:23:17+0400",
    "origin": null,
}
```

| Name   | Type         | Description                                               |
|--------|--------------|-----------------------------------------------------------|
| method | string       | method used in the request (HEAD, GET, POST, PUT, DELETE) |
| time   | string       | current time                                              |
| origin | string, null | Origin title value in the request, or null                |
