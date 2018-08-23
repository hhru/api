# General information

* The whole API works using the HTTPS protocol.
* Authorization is performed via the OAuth2 protocol.
* All data is available only in the JSON format.
* The basic URL is `https://api.hh.ru/`
* Requests for [any site of HeadHunter Groups of Companies](hosts.md)
  are available
* <a name="date-format"></a> Dates are formatted according to
  [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601): `YYYY-MM-DDThh:mm:ss±hhmm`.


<a name="request-requirements"></a>
### Request requirements

Your request should send the `User-Agent` header, but if your
HTTP client does not allow it, you can send an `HH-User-Agent` header. If no header is sent,
you will receive the `400 Bad Request` as a response. 
By specifying the name of the application and the developer's contact email in the header, 
you will help us to contact you promptly if required.
The `User-Agent` and `HH-User-Agent` headers are interchangeable. If you send both headers,
only `HH-User-Agent` is processed.

```
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

More detail on [errors in the User-Agent title](errors.md#user-agent).


<a name="request-body"></a>
### Request body format when sending JSON

Data transferred in the request body must meet the requirements:

* Valid JSON (it is acceptable to transfer both minified and
  pretty-printed variants with extra whitespace and line breaks).

* It is recommended to use the UTF-8 encoding without extra escaping
  (`{"name": "Иванов Иван"}`).

* It is also possible to use the ascii encoding with escaping
  (`{"name": "\u0418\u0432\u0430\u043d\u043e\u0432 \u0418\u0432\u0430\u043d"}`).

* Data types in certain fields are supplemented with additional conditions
  described in each specific method. In JSON, data types are `string`, `number`,
  `boolean`, `null`, `object`, `array`.

<a name="response"></a>
### Response
A response that exceeds a certain length will be compressed using gzip.

<a name="errors-and-codes"></a>
### Errors and response codes

API extensively uses informing through response codes.
The application must process them correctly.

In case of failure or breakdown, responses with the `503` and `500` code may be
returned.

When an error occurs, the response body, besides the response code,
may have additional information allowing the developer
to learn the cause of a particular response.

[More detail on possible errors](errors.md).


<a name="deprecated"></a>
### Undocumented fields and request parameters

In responses and API parameters you can find keys that are not described in the
documentation. It usually means that they are left for compatibility with older
versions. It is not recommended to use them. If your application already uses
such keys, switch to using desirable keys described in the documentation.


<a name="pagination"></a>
### Pagination

For every request that presupposes the return of object list you can indicate
`page=N&per_page=M` in the parameters. Numeration starts from zero; the first
(zero) page is returned by default with 20 objects on it. In all responses where
pagination is available, the uniform root object:

```json
{
  "found": 1,
  "per_page": 1,
  "pages": 1,
  "page": 0,
  "items": [{}]
}
```

<a name="cors"></a>
### CORS (Cross-Origin Resource Sharing)

API supports the CORS technology for requesting browser data from any domain.
This method is preferable to JSONP. It is not restricted to the GET method. To
debug CORS, a [special method](cors.md) is available. To use JSONP, transfer the
`?callback=callback_name` parameter.

* [CORS specification on w3.org](http://www.w3.org/TR/cors/)
* [HTML5Rocks CORS Tutorial](http://www.html5rocks.com/en/tutorials/cors/)
* [CORS on dev.opera.com](http://dev.opera.com/articles/view/dom-access-control-using-cross-origin-resource-sharing/)
* [CORS on caniuse.com](http://caniuse.com/#feat=cors)
* [CORS on en.wikipedia.org](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)


<a name="links"></a>
## External links to articles and standards

* [HTTP/1.1](http://tools.ietf.org/html/rfc2616)
* [JSON](http://json.org/)
* [URI Template](http://tools.ietf.org/html/rfc6570)
* [OAuth 2.0](http://tools.ietf.org/html/rfc6749)
* [REST](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
* [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601)
