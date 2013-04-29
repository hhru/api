# Общая информация

* Всё API работает по протоколу HTTPS.
* Авторизация осуществляется по протоколу OAuth2.  
* Все данные доступны только в формате JSON.
* Базовый URL — `https://api.hh.ru/`
* Даты форматируются в соответствии с [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601): `YYYY-MM-HHThh:mm:ss±hh:mm`.

### Требования к запросами
В запросе необходимо передавать заголовок `User-Agent`, в противном случе ответом будет `400 Bad Request`. 
Указание в заголовке названия приложения и контактной почты разработчика позволит нам оперативно с вами 
связаться в случае необходимости.
```
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

### Ошибки и коды ответов
API широко использует информирование при помощи кодов ответов. Приложение должно корректно их обрабатывать.

В случае неполадок и сбоев, возможны ответы с кодом `503` и `500`.
При каждой ошибке, помимо кода ответа, в теле ответа может быть выдана дополнительная информация, 
позволяющая разработчику понять причину соответствующего ответа:
```json
{
  "description": "Unknown error. It has been logged"
}
```

В случае, когда передан некорректный аргумент, помимо ответа с кодом `400`, в теле ответа будет информация о названии
неправильного параметра:
```json
{
  "description": "failed to convert page argument to positive integer",
  "bad_argument": "per_page"
}
```

### Пагинация
К любому запросу, подразумевающему выдачу списка объектов, можно в параметрах указать `page=N&per_page=M`. Нумерация идёт 
с нуля, по умолчанию выдаётся первая (нулевая) страница с 20 объектами на странице. Во всех ответах, где доступна пагинация,
единообразный корневой объект:
```json
{
  "found": 1,
  "per_page": 1,
  "pages": 1,
  "page": 0,
  "items": [{}]
}
```

### CORS (Cross-Origin Resource Sharing)
API поддерживает технологию CORS для запроса данных из
браузера с произвольного домена. Этот метод более предпочтителен, чем использование JSONP. Он неограничен методом GET.
Для использования JSONP передайте параметр `?callback=callback_name`. В будущем, поддержка JSONP может быть убрана.

* [CORS specification on w3.org](http://www.w3.org/TR/cors/)
* [HTML5Rocks CORS Tutorial](http://www.html5rocks.com/en/tutorials/cors/)
* [CORS on dev.opera.com](http://dev.opera.com/articles/view/dom-access-control-using-cross-origin-resource-sharing/)
* [CORS on caniuse.com](http://caniuse.com/#feat=cors)
* [CORS on en.wikipedia.org](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)
