# HeadHunter API

**По-русски** | [In english](docs_eng/README.md)

HeadHunter API — это инструментарий для интеграции
[HeadHunter](http://hh.ru/) в ваш продукт.

Для начала ознакомьтесь с [общей информацией](https://api.hh.ru/openapi/redoc#section/Obshaya-informaciya) по работе API,
[часто задаваемыми вопросами](docs/FAQ.md) и
с требованиями к [использованию логотипов](https://dev.hh.ru/articles/logos) и
[названию приложений](https://dev.hh.ru/articles/apps).

Для использования методов, требующих авторизацию пользователя или приложения, вам необходимо
зарегистрировать приложение по адресу [https://dev.hh.ru](https://dev.hh.ru)
и настроить процесс [авторизации](docs/authorization.md).

Зарегистрированное приложение может запрашивать у пользователей hh.ru
разрешение доступа к их персональным данным, без получения и хранения их
логина и пароля.


> ‼️ Обратите внимание, что методы для работы с сообщениями в рамках отклика/приглашения от имени [соискателя](docs/negotiations.md#get_messages) и 
> [менеджера работодателя](docs/employer_negotiations.md#get-messages) устарели, и новые возможности [чатов](https://feedback.hh.ru/knowledge-base/article/1290) в них не будут поддерживаться. 
> В связи с этим переписка может некорректно отображаться. 

> Доступ к ряду методов для работодателя [платный](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya/operation/get-payable-api-method-access). 

> Для уточнения стоимости API необходимо обратиться к Вашему персональному менеджеру или позвонить по телефону: 
> +7 495 974-64-27 (для Москвы и Подмосковья),  
> +7 812 458-45-45 (для Санкт-Петербурга),  
> 8 800 100-64-27 (для регионов России),  
> +375 17 336 03 02, +375 33 336 03 02 (для Республики Беларусь).

## [OpenAPI](https://api.hh.ru/openapi/redoc)

Доступная в [OpenAPI](https://api.hh.ru/openapi/redoc) документация будет со временем дополняться.
Методы, описанные в данной документации и доступные в OpenAPI, имеют соответствующую ссылку.

Спецификация HeadHunter API: [openapi.yml](https://api.hh.ru/openapi/specification/public).

<a name="content"></a>
## Содержание

Пометки в документации:

* <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> –
  актуально для анонимных запросов, не требует авторизации.
* <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> – актуально для запросов от имени приложения, требует [авторизацию приложения](docs/authorization_for_application.md)
* <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> –
  актуально для запросов от имени соискателя, требует [авторизацию пользователя](docs/authorization_for_user.md).
* <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" /> –
  актуально для бесплатных методов работодателя, требует  [авторизацию пользователя](docs/authorization_for_user.md).
* <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> –
  актуально для [платных](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya/operation/get-payable-api-method-access) методов работодателя, требует  [авторизацию пользователя](docs/authorization_for_user.md).


<a name="general"></a>
### Общая информация

* [Общая информация](https://api.hh.ru/openapi/redoc#section/Obshaya-informaciya) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Условия использования сервиса API](https://dev.hh.ru/admin/developer_agreement) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Требования к использованию логотипов](https://dev.hh.ru/articles/logos) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Требования к названию приложений](https://dev.hh.ru/articles/apps) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Авторизация](docs/authorization.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Кэширование](docs/cache.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Ошибки и коды ответов](docs/errors.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Платный доступ для работодателей к некоторым методом API](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya/operation/get-payable-api-method-access) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Новая модель работы с базой резюме (поддержка в API)](docs/payable/resume.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="resources"></a>
<a name="context"></a>
### Контекст

* Информация об авторизованном пользователе или приложении <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * Получение информации об авторизованном пользователе:
    * [Соискатель](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-soiskatele/operation/get-current-user-info)
    * [Работодатель](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/operation/get-current-user-info)
  * [Редактирование информации авторизованного пользователя](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-soiskatele/operation/edit-current-user-info)
  * [Получение информации об авторизованном приложении](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-prilozhenii/operation/get-current-user-info)
* Информация о менеджере
  * [Рабочие аккаунты менеджера](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/operation/get-manager-accounts) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Предпочтения менеджера](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/operation/get-manager-settings) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Информация по активным услугам API для платных методов](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya/operation/get-payable-api-actions) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Локализация](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-locales) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Локализация для резюме](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-locales-for-resume) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Выбор сайта](https://api.hh.ru/openapi/redoc#section/Obshaya-informaciya/Vybor-sajta) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="webhook"></a>
### [Webhook API](https://api.hh.ru/openapi/redoc#tag/Webhook-API)

* [Список уведомлений, на которые подписан пользователь](https://api.hh.ru/openapi/redoc#tag/Webhook-API/operation/get-webhook-subscriptions) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Подписка на уведомления](https://api.hh.ru/openapi/redoc#tag/Webhook-API/operation/post-webhook-subscription) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Удаление подписки](https://api.hh.ru/openapi/redoc#tag/Webhook-API/operation/cancel-webhook-subscription) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Изменение подписки](https://api.hh.ru/openapi/redoc#tag/Webhook-API/operation/change-webhook-subscription) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="resume"></a>
### Резюме

* [Поиск резюме](https://api.hh.ru/openapi/redoc#tag/Poisk-rezyume/operation/search-for-resumes) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Сохраненные поиски резюме](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Список сохраненных поисков резюме](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume/operation/get-saved-resume-searches) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Получение единичного сохраненного поиска резюме](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume/operation/get-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Создание нового сохраненного поиска резюме](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume/operation/create-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Обновление сохраненного поиска резюме](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume/operation/update-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Удаление сохраненного поиска резюме](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume/operation/delete-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Передача сохраненного поиска резюме другому менеджеру](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-rezyume/operation/move-saved-resume-search) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Просмотр резюме](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* Работа с резюме для соискателя <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Работа с телефоном](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Rabota-s-telefonom) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Список резюме авторизованного пользователя](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-mine-resumes) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Просмотр резюме](https://api.hh.ru/openapi/redoc#tag/Prosmotr-rezyume/operation/get-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Создание резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/create-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Редактирование резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/edit-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Публикация и продление резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Publikaciya/operation/publish-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Клонирование резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/create-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Удаление резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/delete-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Проверка возможности создания резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Sozdanie-i-obnovlenie/operation/get-resume-creation-availability) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [История просмотра резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume-view-history) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Условия заполнения полей нового резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Usloviya-zapolneniya-polej/operation/get-new-resume-conditions) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Информация о статусе резюме и готовности резюме к публикации](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resume-status) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Списки видимости резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Получение списков видимости](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti/operation/get-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Получение списка типов видимости резюме](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti/operation/get-resume-access-types) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Добавление компаний в список видимости](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti/operation/add-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Удаление компаний из списка видимости](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti/operation/delete-employer-from-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Очистка списка видимости](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti/operation/delete-resume-visibility-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
    * [Поиск работодателей для добавления в список видимости](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Spiski-vidimosti/operation/get-resume-visibility-employers-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Артефакты (фото, портфолио)](https://api.hh.ru/openapi/redoc#tag/Rabota-s-artefaktami) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Поиск по вакансиям, похожим на резюме](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij-dlya-soiskatelya/operation/get-vacancies-similar-to-resume) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [История откликов/приглашений по резюме](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-resume-negotiations-history) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

<a name="vacancies"></a>
### Вакансии

* [Получение вакансий](docs/vacancies.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Поиск по вакансиям](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij/operation/get-vacancies) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
    * [Кластеры](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij/Klastery-v-poiske-vakansij) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение информации о вакансии](docs/vacancies.md#item) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Особенности работы с вакансиями для соискателя](docs/vacancies_for_applicant.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> 
* [Поиск по вакансиям, похожим на вакансию](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij/operation/get-vacancies-similar-to-vacancy) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Отобранные вакансии](docs/vacancies_for_applicant.md#favorited) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Скрытые вакансии](https://api.hh.ru/openapi/redoc#tag/Skrytye-vakansii) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Скрытые работодатели](https://api.hh.ru/openapi/redoc#tag/Skrytye-rabotodateli) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Сохраненные поиски вакансий](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-vakansij) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Список сохраненных поисков вакансий](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-vakansij/operation/get-saved-vacancy-searches) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Получение единичного сохраненного поиска вакансий](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-vakansij/operation/get-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Создание нового сохраненного поиска вакансий](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-vakansij/operation/create-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Обновление сохраненного поиска вакансий](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-vakansij/operation/update-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Удаление сохраненного поиска вакансий](https://api.hh.ru/openapi/redoc#tag/Sohranennye-poiski-vakansij/operation/delete-saved-vacancy-search) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Работа с вакансиями](docs/employer_vacancies.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Возможные варианты публикации вакансий](docs/employer_vacancies.md#available_types) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Публикация вакансий](docs/employer_vacancies.md#creation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Редактирование вакансий](docs/employer_vacancies.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Продление вакансий](docs/employer_vacancies.md#prolongate) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Список опубликованных вакансий](docs/employer_vacancies.md#active) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Архивация вакансий](docs/employer_vacancies.md#archive) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Список архивных вакансий](docs/employer_vacancies.md#archived) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Удаление вакансий](docs/employer_vacancies.md#hide) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Список удаленных вакансий](docs/employer_vacancies.md#hidden) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Список улучшений для вакансии](https://api.hh.ru/openapi/redoc#tag/Upravlenie-vakansiyami/operation/get-vacancy-upgrade-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Статистика по вакансии](docs/employer_vacancies.md#stats) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Просмотры вакансии](docs/employer_vacancies.md#visitors) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Черновики вакансий](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение списка черновиков](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/operation/get-vacancy-draft-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Удаление черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/operation/delete-vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Создание черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/operation/create-vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Публикация вакансий на основе черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/operation/publish-vacancy-from-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/operation/get-vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Изменение черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/operation/change-vacancy-draft) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="applicants"></a>
### Соискатели

* [Комментарии к соискателю](https://api.hh.ru/openapi/redoc#tag/Kommentarii-k-soiskatelyu) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Авторизация соискателя](https://api.hh.ru/openapi/redoc#tag/Avtorizaciya-soiskatelya) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Соискательские статусы](https://api.hh.ru/openapi/redoc#tag/Soiskatelskie-statusy) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />

<a name="employers"></a>
### Работодатели/компании

* [Поиск компаний](https://api.hh.ru/openapi/redoc#tag/Rabotodatel/operation/search-employer) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Получение информации о компании](https://api.hh.ru/openapi/redoc#tag/Rabotodatel/operation/get-employer-info) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Услуги работодателя](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Авторизация работодателя](https://api.hh.ru/openapi/redoc#tag/Avtorizaciya-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Менеджеры работодателя](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="employer_managers"></a>
### Менеджеры работодателя

* [Менеджеры](docs/employer_managers.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Добавление менеджера](docs/employer_managers.md#add) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Редактирование менеджера](docs/employer_managers.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Удаление менеджера](docs/employer_managers.md#delete) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Справочник менеджеров работодателя](docs/employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение информации о менеджере](docs/employer_managers.md#item) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Дневной лимит просмотра резюме для текущего менеджера](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/operation/get-employer-manager-limits) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="negotiations"></a>
### Переписка (отклики/приглашения)

* [Переписка для соискателя](docs/negotiations.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Получение списка откликов](docs/negotiations.md#get_negotiations) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Получение списка активных откликов](docs/negotiations.md#get_negotiations_active) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Откликнуться на вакансию](docs/negotiations.md#post_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Просмотр отклика/приглашения](docs/negotiations.md#get_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Скрыть отклик](docs/negotiations.md#hide_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Просмотр списка сообщений в отклике](docs/negotiations.md#get_messages) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Отправка сообщений в отклике](docs/negotiations.md#send_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Редактирование сообщения в отклике](docs/negotiations.md#edit_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* Резюме для отклика на указанную вакансию <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Список резюме, которыми можно откликнуться на указанную вакансию](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-suitable-resumes) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Резюме, сгруппированные по возможности отклика на данную вакансию](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Prosmotr-informacii/operation/get-resumes-by-status) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Переписка для работодателя](docs/employer_negotiations.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Модель работы, термины и процедуры](docs/employer_negotiations.md#model) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Общее описание процесса работы с откликами/приглашениями](docs/employer_negotiations.md#flow) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Коллекции и работодательские состояния откликов/приглашений](docs/employer_negotiations.md#collections) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Список откликов/приглашений](docs/employer_negotiations.md#negotiations-list) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Просмотр отклика/приглашения](docs/employer_negotiations.md#get-negotiation) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Работа с сообщениями по отклику/приглашению для работодателя](docs/employer_negotiations.md#get-messages) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Приглашение соискателя на вакансию](docs/employer_negotiations.md#add-invite) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Действия по отклику/приглашению (смена состояния)](docs/employer_negotiations.md#actions) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Отметить отклики прочитанными](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/post-negotiations-topics-read) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Статистика по работе с откликами](docs/employer_negotiations_statistics.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Тексты сообщений](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/get-negotiation-message-templates) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Изменение шаблона ответа соискателю](https://api.hh.ru/openapi/redoc#tag/Otklikipriglasheniya-rabotodatelya/operation/put-mail-templates-item) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Инструменты оценки](docs/assessment.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />


<a name="dictionaries"></a>
### Справочники
* [Справочники в OpenAPI](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Регионы](docs/areas.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Профессиональные роли](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Станции метро в указанном городе](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-metro-stations-in-city) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Станции метро во всех городах](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-metro-stations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Языки](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-languages) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Отрасли компаний](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-industries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Учебные заведения](docs/educational_institutions.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Основная информация об учебных заведениях](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-educational-institutions-dictionary) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Факультеты учебных заведений](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-educational-institutions-dictionary) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Справочники работодателя](docs/employer_dictionaries.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Адреса](https://api.hh.ru/openapi/redoc#tag/Adresa-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Типы и права менеджера](docs/employer_managers.md#dict) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Менеджеры работодателя](docs/employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Департаменты](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/operation/get-employer-departments) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Тесты](https://api.hh.ru/openapi/redoc#tag/Spravochniki-rabotodatelya/operation/get-tests-dictionary) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Регионы вакансий](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/operation/get-employer-vacancy-areas) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Брендированные шаблоны вакансий](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/operation/get-vacancy-branded-templates-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Ключевые навыки](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Прочие справочники](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-dictionaries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="suggests"></a>
### Подсказки (autosuggest, autocomplete)
* [Подсказки в OpenAPI](https://api.hh.ru/openapi/redoc#tag/Podskazki) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Подсказки](docs/suggests.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по названиям университетов](docs/suggests.md#educational_institutions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по организациям](docs/suggests.md#companies) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по специализациям](docs/suggests.md#specializations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по ключевым навыкам](docs/suggests.md#key-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по должностям резюме](docs/suggests.md#resume-positions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по регионам](docs/suggests.md#areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [по ключевым словам поиска вакансий](docs/suggests.md#vacancy-search-keyword) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="salary"></a>
### Банк данных заработных плат

* [Отчёты Банка данных заработных плат](https://api.hh.ru/openapi/redoc#tag/Bank-dannyh-o-zarplatah) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Оценка заработной платы без прогнозов](https://api.hh.ru/openapi/redoc#tag/Bank-dannyh-o-zarplatah/operation/get-salary-evaluation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Справочники Банка данных заработных плат](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Отрасли](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-industries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Уровни специалистов](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-employee-levels) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Профобласти и специализации](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-professional-areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Регионы и города](https://api.hh.ru/openapi/redoc#tag/Spravochniki-Banka-dannyh-zarabotnyh-plat/operation/get-salary-salary-areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="feedback"></a>
## Поддержка, обратная связь, новости

Общайтесь с нами через twitter [@apihhru](https://twitter.com/apihhru) или
через почту api@hh.ru.

Если вы нашли баг в работе HeadHunter API или
[виджетах](https://dev.hh.ru/admin/widgets), загляните в
[issues](https://github.com/hhru/api/issues), возможно, про него мы уже знаем и
чиним. Если нет, лучше всего сообщить о нём там. Там же вы можете оставлять свои
пожелания и предложения.

Если вы нашли проблему на одном из сайтов HeadHunter,
[напишите в поддержку по сайту](https://hh.ru/feedback) или в
[сообщество поддержки](https://feedback.hh.ru/).

За новостями вы можете следить по
[коммитам](https://github.com/hhru/api/commits/master) в этом репозитории.
[RSS](https://github.com/hhru/api/commits/master.atom).

Часто задаваемые вопросы собраны в [FAQ](docs/FAQ.md).
