# Ошибки и коды ответов

API широко использует информирование при помощи HTTP кодов ответов. Приложение
должно корректно их обрабатывать.

При каждой ошибке, помимо кода ответа, в теле ответа выдаётся
дополнительная информация, позволяющая разработчику понять 
причину ошибки.

Все ошибки выдаются в формате:

```json
{
    "errors": [
        {
            "type": "...",
            "value": "..."
        }
    ]
}
```

Одновременно может выдаваться несколько ошибок.
Ключ `type` присутствует в каждом объекте массива `errors` и содержит текстовый
идентификатор класса ошибки. Ключ `value` опционален и конкретизирует данные
об ошибке.

> Помимо описанных выше `errors`, API может выдавать дополнительно другие ключи,
> оставленные для обратной совместимости. **Использовать их не рекомендуется.**


<a name="general-errors"></a>
## Ошибка в запросе

В случае невозможности найти запрашиваемый ресурс вернётся ответ
`404 Not Found` и в массиве `errors` будет объект:

```json
{
    "type": "not_found"
}
```

При ошибке в параметрах запроса (к примеру,
`GET https://api.hh.ru/vacancies/?employer_id=foo`) в ответ придёт
`400 Bad Request`, в массиве ошибок будет объект:

```json
{
    "type": "bad_argument",
    "value": "employer_id"
}
```

<a name="system-errors"></a>
## Системная ошибка

Если в данный момент сервис не может обработать запрос, но он его корректно
понял, то в ответ придёт `503 Service Unavailable` и `type` будет содержать
`service_unavailable`.

В случае непредвиденной ситуации API вернёт 500.

В редких случаях ошибки с 5** кодами могут возвращаться с телом не содержащим
валидный json. Приложение должно в таких случаях ориентироваться только на код
ответа.


## Общие ошибки запроса

<a name="user-agent"></a>
### Неверный User-Agent

Подробнее про [заголовок User-Agent](general.md#request-requirements).

HTTP code | type | value | описание
----------|------|-------|-----------
400 | bad_user_agent | unset | заголовок User-Agent не передан
400 | bad_user_agent | blacklisted | значение User-Agent в чёрном списке


## Ошибки авторизации

Подробнее [про авторизацию](authorization.md).


<a name="oauth-get-errors"></a>
### Описание ошибок при получении/обновлении токенов

Описание полей:

Имя | Тип | Значение 
--- | --- | --------
error | строка | Одно из значений, [описанных в стандарте RFC 6749](http://tools.ietf.org/html/rfc6749#section-5.2). Например, `invalid_request`, если какой либо из обязательных параметров не был передан
error_description | строка | Дополнительное описание ошибки


Ниже приведены некоторые возможные ошибки с описанием.

<table>
<tr><th>HTTP code</th><th>error</th><th>error_description</th><th>описание</th></tr>

<tr>
    <td rowspan=8>400</td>
    <td rowspan=8>invalid_request</td>
    <td>account not found</td>
    <td>Ошибка может возникнуть, если передана неправильная пара client_id и client_secret</td>
</tr>
<tr>
    <td>account is locked</td>
    <td>Пользовательский аккаунт заблокирован. Пользователь должен обратиться в <a href="https://github.com/hhru/api#feedback">службу поддержки сайта</a></td>
</tr>
<tr>
    <td>password invalidated</td>
    <td>Пароль от пользовательского аккаунта устарел. Пользователь должен восстановить пароль на сайте <a href="https://hh.ru">https://hh.ru</a></td>
</tr>
<tr>
    <td>login not verified</td>
    <td>Пользовательский аккаунт не подтвержден. Пользователь должен обратиться в <a href="https://github.com/hhru/api#feedback">службу поддержки сайта</a></td>
</tr>
<tr>
    <td>bad redirect url</td>
    <td>Передан неправильный redirect_url</td>
</tr>
<tr>
    <td>token is empty</td>
    <td>Не передан refresh_token</td>
</tr>
<tr>
    <td>token not found</td>
    <td>Передан не правильный refresh_token</td>
</tr>
<tr>
    <td>code not found</td>
    <td>Переданный authorization_code не найден</td>
</tr>

<tr>
    <td>400</td>
    <td>invalid_client</td>
    <td>client_id or client_secret not found</td>
    <td>Ошибка может возникнуть в случае, если данный client_id не найден или был удален, передан неправильный client_secret</td>
</tr>

<tr>
    <td rowspan=8>400</td>
    <td rowspan=8>invalid_grant</td>
    <td>token has already been refreshed</td>
    <td>Ошибка возникает при попытке воспользоваться refresh-токеном второй раз</td>
</tr>
<tr>
    <td>token not expired</td>
    <td>Ошибка возникает при попытке обновить действующий access-токен. access-токен можно обновлять только после того, как он истек</td>
</tr>
<tr>
    <td>token was revoked</td>
    <td>Токен был отозван. Например, токен отзывается, если время действия пароля истекло</td>
</tr>
<tr>
    <td>bad token</td>
    <td>Передано неправильное значение токена</td>
</tr>
<tr>
    <td>code has already been used</td>
    <td>authorization_code уже был использован (его можно использовать только один раз)</td>
</tr>
<tr>
    <td>code expired</td>
    <td>authorization_code истек</td>
</tr>
<tr>
    <td>code was revoke</td>
    <td>authorization_code был отозван (это происходит, если время действия пароля истекло)</td>
</tr>
<tr>
    <td>token deactivated</td>
    <td>Токен был деактивирован. Токен деактивируется после того, как пользователь сменил пароль</td>
</tr>

<tr>
    <td>400</td>
    <td>unsupported_grant_type</td>
    <td>unsupported grant_type</td>
    <td>Возникает, если передать неправильное значение в поле grant_type</td>
</tr>

<tr>
    <td>403</td>
    <td>forbidden</td>
    <td>app token refresh too early</td>
    <td>Возникает, если запрашивать token приложения чаще чем раз в пять минут</td>
</tr>

</table>


<a name="oauth"></a>
### Ошибки использования авторизации

В случае, если вы
[совершаете авторизованный запрос](authorization.md#check-access_token)
в api и предоставленная авторизация по каким-либо причинам не действительна,
вернётся ошибка с `type` `oauth` и, возможно, одним из перечисленных `value`.

HTTP code | type | value | описание
----------|------|-------|-----------
403 | oauth | bad_authorization | токен авторизации не существует или не валидный
403 | oauth | token_expired | время жизни access_token завершилось, необходимо [выполнить обновление access_token](authorization.md#refresh_token)
403 | oauth | token_revoked | токен отозван пользователем, приложению необходимо [запросить новую авторизацию](authorization.md)
403 | oauth | application_not_found | ваше приложение было удалено


<a name="employer_payable_methods"></a>
## Ошибки доступа к платному методу

В случае, если вы запрашиваете один из [платных методов](/payable/employer_payable_methods.md) 
без купленного доступа, вернётся следующая ошибка:

HTTP code | type | value | описание
----------|------|-------|-----------
403 | api_access_payment | action_must_be_payed | запрос платного метода при отсутствии оплаченного доступа


<a name="service-errors"></a>
## Ошибки отдельных ресурсов

В тех случаях, когда сервис способен выдать более подробную информацию об
ошибке, она будет выдана в теле ответа. В этом случае скорее всего
код ответа будет 400, 403, 409, 429, но возможны и другие.

Как минимум, приложение должно корректно обрабатывать HTTP статусы ответов.
Для более удобной работы с приложением, рекомендуется также обрабатывать
пришедший тип ответа. Приведенные ниже таблицы содержат неполный список ошибок,
он может расширяться.


<a name="artifacts"></a>
### Артефакты

При загрузке артефактов помимо прочих возможны следующие ошибки:

HTTP code | type | value | описание
----------|-----|--------|-----------
400 | bad_argument | file | не указан файл, либо указано несколько
400 | bad_argument | type | некорректное значение параметра type
400 | bad_argument | description | слишком длинное описание
400 | artifacts | limit_exceeded | превышено количество артефактов
400 | artifacts | image_too_large | размер файла больше допустимого
400 | artifacts | unknown_format | неизвестный формат файла
403 | forbidden | — | ошибка прав доступа


<a name="negotiations"></a>
### Переписка (отклики/приглашения)

Помимо [общих ошибок](#general-errors), могут быть возвращены следующие ошибки:

HTTP code | type | value | описание
----------|------|-------|-----------
400 | negotiations | vacancy_not_found | вакансия не найдена
403 | negotiations | invalid_vacancy | вакансия из отклика/приглашения была архивирована либо скрыта
400 / 403 | negotiations | resume_not_found | резюме из отклика/приглашения было скрыто, либо удалено, либо не найдено
403 | negotiations | already_applied | уже есть отклик/приглашение на указанную связку resume_id+vacancy_id
403 | negotiations | test_required | для отклика необходимо пройти тест (в данный момент, отклик на такие вакансии через API недоступен)
403 | negotiations | resume_visibility_conflict | невозможно откликнуться на анонимную вакансию резюме с видимостью "белый список"
403 | negotiations | edit_forbidden | редактирование сообщения недоступно
403 | negotiations | application_denied | общая ошибка запрета отклика в случае, когда дополнительная информация недоступна
400 / 403 | negotiations | limit_exceeded | превышен лимит количества откликов/приглашений
403 | negotiations | wrong_state | действие по отклику/приглашению в данном статусе невозможно
403 | negotiations | empty_message | передан пустой текст письма
403 | negotiations | too_long_message | передан слишком длинный текст письма
403 | negotiations | address_not_found | переданный к действию по адрес не существует, либо принадлежит другому работодателю
403 | negotiations | not_enough_purchased_services | не хватает оплаченных услуг, обычно [доступа к базе резюме](https://hh.ru/price#dbaccess)
403 | negotiations | in_a_row_limit | превышено количество последовательных сообщений в переписке, оппонент должен ответить на сообщение, чтобы появилась возможность писать вновь
403 | negotiations | overall_limit | превышен лимит сообщений
403 | negotiations | no_invitation | переписка недоступна, так как в отклике ещё не было приглашения
403 | negotiations | message_cannot_be_empty | сообщение в переписке не может быть пустым
403 | negotiations | disabled_by_employer | возможность переписки по отклику отключена работодателем
403 | negotiations | resume_deleted | отправить сообщение невозможно, так как резюме, с которым совершался отклик, удалено или скрыто
403 | negotiations | archived | отправить сообщение невозможно, так как вакансия, на которую совершался отклик, заархивирована



<a name="vacancies_favorited"></a>
### Отобранные вакансии

Помимо кода ошибки при
[добавлении в список отобранных вакансий](vacancies.md#favorited) могут
быть возвращены следующие ошибки:

HTTP code | type | value | описание
----------|------|-------|-----------
403 | vacancies_favorited | vacancy_archived | вакансия уже архивирована и не может быть добавлена в отобранное
403 | vacancies_favorited | limit_exceeded | превышен лимит количества отобранных вакансий


<a name="vacancies-create-n-edit"></a>
### Публикация и редактирование вакансий

Помимо кода ошибки при [публикации](employer_vacancies.md#creation) и
[редактировании](employer_vacancies.md#edit) вакансии могут быть возвращены
следующие ошибки:

HTTP code | type | value | reason | описание
----------|------|-------|-------|---------
400 | bad_json_data | *field_name* | *reason* | ошибка в поле вакансии, где *field_name* – ключ поля верхнего уровня, поле reason может не присутствовать
403 | vacancies | not_enough_purchased_services | | купленных услуг для публикации или обновления данного типа вакансии не достаточно
403 | vacancies | quota_exceeded | | квота менеджера на публикацию данного типа вакансии закончилась
403 | vacancies | duplicate | | аналогичная вакансия уже опубликована, данную ошибку можно форсировано отключить (при [добавлении](employer_vacancies.md#creation-ignore-duplicates) и [редактировании](employer_vacancies.md#edit-ignore-duplicates))
403 | vacancies | creation_forbidden | | публикация вакансий недоступна текущему менеджеру
403 | vacancies | unavailable_for_archived | | редактирование недоступно для архивной вакансии
403 | vacancies | conflict_changes | | конфликтные изменения данных вакансии ([подробнее](employer_vacancies.md#edit_more))
403 | vacancies | can_not_accept_kids | | публикация вакансий для поиска соискателей от 14 лет недоступна ([подробнее](employer_vacancies_accept_kids.md#accept-kids))

#### Причины возникновения ошибок

reason | описание 
-------|---------
is_empty | пустое значение
wrong_size | значение имеет неправильный размер
is_too_short | значение имеет слишком маленький размер
is_too_long | значение имеет слишком большой размер
currency_code_is_invalid | валюта заработной платы введена некорректно
chosen_area_is_not_a_leaf_or_not_exist | местоположение вакансии введено неверно (например, передали id, которого нет) или не является конечным регионом (город, населенный пункт)
email_in_description | в описании вакансии содержится email
anonymous_vacancy_contains_address | в анонимной вакансии не должен содержаться адрес работодателя
anonymous_vacancy_has_real_company_name | в названии вакансии не должно содержаться название компании работодателя
only_for_anonymous_type | действие доступно только для анонимных вакансий
address_is_disabled | адрес недоступен
vacancy_type_employer_billing_type_mismatch | тип вакансии не совместим с текущим биллинг-типом
only_for_direct_type | действие доступно только для прямых вакансий
address_is_empty_with_checked_show_metro_flag | введен пустой адресс с указанием показывать метро
address_has_no_metro_but_checked_show_metro_flag | по введенному адресу не доступно метро, но указана опция показывать метро
default_vacancy_branded_template_is_invalid_or_not_enough_purchased_services | в запросе указан шаблон, который отсутствует в списке доступных шаблонов (этот список можно получить запросом https://github.com/hhru/api/blob/master/docs/employer_vacancy_branded_templates.md#list). Также шаблон может отсутствовать в списке доступных шаблонов, если не оплачена услуга использования [брендированного шаблона вакансии](https://hh.ru/price?from=menu#branding) 
department_code_prohibited_in_anonymous_vacancy | нельзя указать код подразделения для анонимной вакансии
branded_template_prohibited_in_anonymous_vacancy | использование брендированного шаблона невозможно для анонимной вакансии

<a name="vacancies-prolongate"></a>
### Продление вакансии

Помимо кода ошибки при [продлении](employer_vacancies.md#prolongate) вакансии могут быть
возвращены следующие ошибки:

HTTP code | type | value | описание
----------|------|-------|---------
403 | vacancies | not_enough_purchased_services | купленных услуг для продления данного типа вакансии не достаточно
403 | vacancies | quota_exceeded | квота менеджера на публикацию данного типа вакансии закончилась
403 | vacancies | prolongation_forbidden | продление вакансий недоступно текущему менеджеру
403 | vacancies | unavailable_for_archived | продление недоступно для архивной вакансии
403 | vacancies | too_early | продление раньше времени


<a name="employer_managers"></a>
### Менеджеры работодателя

Помимо [общих ошибок](#general-errors) при [добавлении](employer_managers.md#add) и
[редактировании](employer_managers.md#edit) менеджера работодателя могут быть возвращены следующие ошибки:

HTTP code | type | value | reason | описание
----------|------|-------|--------|---------
400 | managers | *field_name* | | ошибка в поле *field_name*
403 | managers | email | already_exist | менеджер с такой почтой уже существует
403 | managers |  | creation_limit_exceeded | достигнут лимит на создание менеджеров
403 | managers | *field_name* | not_editable | поле *field_name* недоступно для редактирования


<a name="resumes"></a>
### Работа с резюме

Помимо [общих ошибок](#general-errors) при
[получении](resumes.md#item) и [обновлении](resumes.md#create_edit) резюме могут
быть возвращены следующие ошибки:

HTTP code | type | value | описание
----------|------|-------|---------
400 | bad_argument | with_contact | не правильное значение поля `with_contact`
400 | resumes | total_limit_exceeded | превышено допустимое количество резюме (актуально только для соискателей)
429 | resumes | view_limit_exceeded | превышен лимит просмотров резюме в сутки (актуально только для работодателей)


<a name="vacancies_blacklist"></a>
### Добавление в список скрытых вакансий

Помимо [общих ошибок](#general-errors) при
[добавлении в список скрытых вакансий](blacklisted.md#vacancies)
могут быть возвращены следующие ошибки:

HTTP code | type | value | описание
----------|------|-------|---------
400 | vacancies_blacklist | limit_exceeded | превышен лимит на количество вакансий в списке скрытых
404 | vacancies_blacklist | not_found | вакансия для добавления в список не найдена


<a name="employers_blacklist"></a>
### Добавление в список скрытых компаний

Помимо [общих ошибок](#general-errors) при
[добавлении в список скрытых вакансий компаний](blacklisted.md#employers)
могут быть возвращены следующие ошибки:

HTTP code | type | value | описание
----------|------|-------|---------
400 | employers_blacklist | limit_exceeded | превышен лимит на количество вакансий в списке скрытых
404 | employers_blacklist | not_found | вакансия для добавления в список не найдена


<a name="resume-visibility-lists"></a>
### Списки видимости резюме

<a name="resume-visibility-lists-get"></a>
#### Получение списков видимости

HTTP code | type | value | описание
----------|------|-------|---------
400 | bad_argument | per_page | передано невалидное количество элементов на странице (максимум 100)

<a name="resume-visibility-lists-add"></a>
#### Добавление компаний в список

HTTP code | type | value | описание
----------|------|-------|---------
400 | resume_visibility_list | unknown_employer | передан неизвестный идентификатор работодателя
400 | resume_visibility_list | limit_exceeded | превышен лимит списка видимости
400 | resume_visibility_list | too_many_employers | передано слишком много работодателей

<a name="resume-visibility-lists-remove"></a>
#### Удаление компаний из списка

HTTP code | type | value | описание
----------|------|-------|---------
400 | bad_argument | id | передан невалидный идентификатор работодателя
400 | resume_visibility_list | too_many_employers | передано слишком много работодателей

<a name="bulk-request"></a>
#### bulk-запрос

HTTP code | type | value | reason | описание
----------|------|-------|---------|--------- 
400 | bad_argument | id | too_many_bulk_items | слишком много id
400 | bad_argument | id | | передан невалидный идентификатор

<a name="manager-accounts"></a>
### Рабочие аккаунты менеджера
HTTP code | type | value | описание
----------|------|-------|-----------
403 | manager_extra_accounts | manager_extra_account_not_found | В заголовке передан некорректный id аккаунта
403 | manager_accounts | used_manager_account_forbidden | [Рабочий аккаунт заблокирован](#manager-accounts-blocked)

<a name="manager-accounts-blocked"></a>
В случае, если аккаунт пользователя заблокирован, придет ошибка вида:
```json
{
    "errors": [
    {
        "type": "manager_accounts",
        "value": "used_manager_account_forbidden",
        "allowed_accounts": [
            {
                "id": "1",
                "employer": {
                    "id": "12345678",
                    "name": "Alpha Corp."
                }
            },
            {
                "id": "2",
                "employer": {
                    "id": "87654321",
                    "name": "Beta Inc."
                }
            }
        ]
    }
  ]
}
```
где `allowed_accounts` содержит массив доступных для этого токена аккаунтов
Элементы массива аналогичны [результату, выдаваемому в списке рабочих аккаунтов](manager_accounts.md#account-info)
