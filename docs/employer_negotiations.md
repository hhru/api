# Переписка (отклики/приглашения) для работодателя

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Методы требуют наличия [платного доступа для работодателя](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya/operation/get-payable-api-method-access)

*Документация по переписке для соискателя доступна в [отдельной статье](negotiations.md).*

* [Модель работы, термины и процедуры](#model)
* [Общее описание процесса работы с откликами/приглашениями](#flow)
* [Коллекции и работодательские состояния откликов/приглашений](#collections)
* [Список откликов/приглашений](#negotiations-list)
* [Просмотр отклика/приглашения](#get-negotiation)
* [Просмотр списка сообщений в отклике/приглашении](#get-messages)
* [Отправка сообщения в отклике/приглашении](#add-messages)
* [Приглашение соискателя на вакансию](#add-invite)
* [Изменение состояния отклика/приглашения](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/change-negotiation-action)
* [Изменение состояния нескольких откликов/приглашений](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-negotiations-collection-to-next-state)
* [Просмотр предпочитаемой сортировки откликов](#get-preference-order)
* [Изменение предпочитаемой сортировки откликов](#update-preference-order)
* [Отметить отклики прочитанными](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/post-negotiations-topics-read) 


<a name="model"></a>
## Модель работы, термины и процедуры

Отклики и приглашения соответствуют модели, которая выражается в запросах и
ответах API. Если приложение использует модель правильно, то изменение
бизнес-логики откликов и приглашений не будет требовать переработки или
исправления.

В откликах и приглашениях используются понятия:

* *отклик* – объект, порождённый по инициативе соискателя (отклик на вакансию). 
  Отклик всегда происходит одним резюме на одну вакансию.

* *приглашение* – объект, порождённый по инициативе работодателя (приглашение на вакансию). 
  Приглашение всегда происходит к одному резюме на одну вакансию.

Кроме процесса появления объекта, работа с откликом или приглашением происходит
одинаково.

* <a name="term-collection"></a> *коллекция* – набор откликов/приглашений,
  объединённых по определённым критериям. Коллекции используются, когда в вашем
  приложении требуется **отобразить** список откликов/приглашений. Не стоит
  полагаться на то, что в определённые этапы обработки отклика/приглашения
  оно будет входить в известные коллекции, так как эта логика может изменяться.

* <a name="term-state"></a> *соискательское состояние отклика/приглашения* –
  статус отклика/приглашения ([поле `state`](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-collection-negotiations-list)), который **видит соискатель**. Возможные значения
  выдаются [в справочнике `negotiations_state`](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) и
  не зависят от вакансии в отклике/приглашении.

* <a name="term-employer-state"></a> *работодательское состояние отклика/приглашения* –
  статус отклика/приглашения у работодателя. Может отличаться от
  соискательского. Список возможных статусов
  **зависит от вакансии и работодателя**, поэтому список
  [необходимо запрашивать](#states), передавая нужную вакансию.

* <a name="term-action"></a> *действие по отклику/приглашению* – действие, которое
  можно выполнить над откликом/приглашением. В результате действия
  работодательское и соискательское состояния отклика/приглашения могут как
  поменяться, так и остаться прежними.

Не следует путать *действие*, *коллекцию* и *состояние* – они могут быть похожи,
но предназначены для разных целей.


<a name="flow"></a>
## Общее описание процесса работы с откликами/приглашениями

Вся работа с откликами/приглашениями происходит в рамках
**одной выбранной вакансии**. Даже у одного работодателя могут быть вакансии
с различными правилами работы по откликам/приглашениям.

Сначала необходимо получить список
[коллекций и работодательских состояний](#collections). Используйте коллекции
для **получения списков откликов/приглашений**. Предлагайте пользователю
выбирать, какую из коллекций он хочет получить. Для получения всех
откликов/приглашений нужно последовательно получить все коллекции. Список
состояний используется только как справочник.

Для **создания приглашения** необходимо запросить вакансии работодателя,
применимые к выбранному резюме. Получить эту информацию можно в
[списке вакансий работодателя](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-active-vacancy-list), там же
будут указаны необходимые параметры (ключ `arguments`) и состояние созданного
отклика (ключ `resulting_employer_state`). У разных работодателей и разных
вакансий могут быть различные правила и состояния добавляемого отклика. Для
каждой пары *вакансия + резюме* может быть только один отклик/приглашение.

Для создания приглашения, работодатель должен иметь активированный доступ к базе
резюме. Для работы с существующим откликом/приглашением доступ не требуется. Это
позволяет обрабатывать отклики на вакансии, даже не имея доступ к базе резюме.

Если вам необходимо **совершить действие** по отклику/приглашению,
ориентируйтесь на список действий, который будет доступен в
[списке (коллекции) откликов/приглашений](#negotiations-list) и в
[отдельном отклике/приглашении](#get-negotiation). Если действие приводит
к смене состояния по отклику/приглашению, это будет явно указано в ключе
`resulting_employer_state`. Не все действия приводят к смене состояния.

После приглашения соискателя вы можете начать с ним
[свободную переписку](#get-messages). Вы сможете
[отправлять сообщения](#add-messages), а соискатель – вам отвечать.
При необходимости переписку для конкретной вакансии
[можно отключить](https://api.hh.ru/openapi/redoc#tag/Vakansii/operation/get-vacancy) (поле `allow_messages`).

Чтобы соискательский отклик считался просмотренным работодателем необходимо сделать одно из следующих действий:
* запросить список сообщений по урлу, 
пришедшему при запросе [списка (коллекции) откликов/приглашений](#negotiations-list) или 
[отдельного отклика/приглашения](#get-negotiation),
* [запросить сообщения](#get-messages) по отклику
* запросить резюме по урлу, пришедшему при запросе [списка (коллекции) откликов/приглашений](#negotiations-list) 
или [отдельного отклика/приглашения](#get-negotiation)
* с помощью отдельного метода [отметить определенные отклики как прочитанные](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/post-negotiations-topics-read)


<a name="states"></a>
<a name="collections"></a>
## Коллекции и работодательские состояния откликов/приглашений по вакансии

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-negotiations)

<a name="negotiations-list"></a>
## Список откликов/приглашений

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-collection-negotiations-list)

<a name="get-negotiation"></a>
## Просмотр отклика/приглашения

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-negotiation-item)

## Просмотр списка сообщений в отклике/приглашении

<a name="get-messages"></a>
> ‼️ Обратите внимание, что методы для работы с сообщениями в рамках отклика/приглашения от имени [соискателя](docs/negotiations.md#get_messages) и
> [менеджера работодателя](docs/employer_negotiations.md#get-messages) устарели, и новые возможности [чатов](https://feedback.hh.ru/knowledge-base/article/1290) в них не будут поддерживаться.
> В связи с этим переписка может некорректно отображаться.

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-negotiation-messages)

<a name="add-messages"></a>
## Отправка сообщения в отклике/приглашении

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/send-negotiation-message)

<a name="add-invite"></a>
## Приглашение соискателя на вакансию

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/invite-applicant-to-vacancy)

<a name="actions"></a>
<a name="put-on-hold"></a>
<a name="invite"></a>
<a name="discard"></a>
## Действия по отклику/приглашению 

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-negotiations-collection-to-next-state)


<a name="get-preference-order"></a>
## Просмотр предпочитаемой сортировки откликов

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-pref-negotiations-order)

<a name="update-preference-order"></a>
## Изменение предпочитаемой сортировки откликов

### Запрос

> !! Данный метод доступен в [OpenAPI](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-pref-negotiations-order)

