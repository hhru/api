# Переписка (отклики/приглашения) для соискателя

*Документация по переписке для работодателя доступна в [отдельной статье](employer_negotiations.md).*

В процессе использования сайта соискатели выбирают вакансии.  Для того чтобы
связаться с работодателем на предмет трудоустройства, соискатель может
откликнуться на выбранную вакансию. Так же и работодатель, найдя интересное
резюме, может предложить соискателю рассмотреть вакансию (приглашение).

Для указанных целей служат специальные сущности — отклики/приглашения.  В них
может быть указана вакансия, резюме и переписка соискателя с работодателем, в
каждый момент времени такие сущности находятся в одном из состояний. Переход
между состояниями сопровождается появлением сообщений с опциональным текстовым
описанием и прочими полями. Сообщения со статусом `null` не переводят весь
отклик в новое состояние.

* [Получение списка откликов](#get_negotiations)
* [Получение списка активных откликов](#get_negotiations_active)
* [Откликнуться на вакансию](#post_negotiation)
* [Просмотр отклика/приглашения](#get_negotiation)
* [Скрыть отклик](#hide_message)
* [Просмотр списка сообщений в отклике](#get_messages)
* [Отправка нового сообщения](#send_message)
* [Редактирование сообщения в отклике](#edit_message)


<a name="get_negotiations"></a>
## Получение списка откликов

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/get-negotiations)

<a name="get_negotiations_active"></a>
## Получение списка активных откликов

### Запрос

Для получения списка активных откликов используйте параметр `status=active` в запросе [списка откликов](#get_negotiations)
 ```
 GET /negotiations?status=active
 ```

До 20.04.20 для запроса активных вакансий использовался ресурс:

```
GET /negotiations/active
```

В настоящее время он является устаревшим и поддерживается для обратной совместимости.

<a name="post_negotiation"></a>
## Откликнуться на вакансию

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/apply-to-vacancy)

<a name="get_negotiation"></a>
## Просмотр отклика/приглашения

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/get-negotiation-item)

<a name="hide_message"></a>
## Скрыть отклик
> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/hide-active-response)


<a name="get_messages"></a>
## Просмотр списка сообщений в отклике

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/get-negotiation-messages)

<a name="send_message"></a>
## Отправка нового сообщения

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/send-negotiation-message)

<a name="edit_message"></a>
## Редактирование сообщений в отклике

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Perepiska-(otklikipriglasheniya)-dlya-soiskatelya/operation/edit-negotiation-message)
