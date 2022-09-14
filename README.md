# HeadHunter API

**По-русски** | [In english](docs_eng/README.md)

HeadHunter API — это инструментарий для интеграции
[HeadHunter](http://hh.ru/) в ваш продукт.

Для начала ознакомьтесь с [общей информацией](docs/general.md) по работе API,
[часто задаваемыми вопросами](docs/FAQ.md) и
с требованиями к [использованию логотипов](https://dev.hh.ru/articles/logos) и
[названию приложений](https://dev.hh.ru/articles/apps).

Для использования методов, требующих авторизацию пользователя или приложения, вам необходимо
зарегистрировать приложение по адресу [https://dev.hh.ru](https://dev.hh.ru)
и настроить процесс [авторизации](docs/authorization.md).

Зарегистрированное приложение может запрашивать у пользователей hh.ru
разрешение доступа к их персональным данным, без получения и хранения их
логина и пароля.


> ‼️ Обратите внимание на [Поддержку нового каталога специализаций (профессиональных ролей)](docs/role_catalog_article.md) . 

> Доступ к ряду методов для работодателя [платный](docs/payable/employer_methods.md). 

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
  актуально для [платных](docs/payable/employer_methods.md) методов работодателя, требует  [авторизацию пользователя](docs/authorization_for_user.md).


<a name="general"></a>
### Общая информация

* [Общая информация](docs/general.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Условия использования сервиса API](https://dev.hh.ru/admin/developer_agreement) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Требования к использованию логотипов](https://dev.hh.ru/articles/logos) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Требования к названию приложений](https://dev.hh.ru/articles/apps) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Авторизация](docs/authorization.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Кэширование](docs/cache.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Ошибки и коды ответов](docs/errors.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Платный доступ для работодателей к некоторым методом API](docs/payable/employer_methods.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Новая модель работы с базой резюме (поддержка в API)](docs/payable/resume.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Новый каталог специализаций (профессиональных ролей). Поддержка в API HH](docs/role_catalog_article.md)  <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="resources"></a>
<a name="context"></a>
### Контекст

* Информация об авторизованном пользователе или приложении <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * Получение информации об авторизованном пользователе:
    * [Соискатель](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-soiskatele/paths/~1me/get)
    * [Работодатель](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-menedzhere/paths/~1me/get)
  * [Редактирование информации авторизованного пользователя](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-soiskatele/paths/~1me/post)
  * [Получение информации об авторизованном приложении](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-prilozhenii/paths/~1me/get)
* Информация о менеджере
  * [Рабочие аккаунты менеджера](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/paths/~1manager_accounts~1mine/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Предпочтения менеджера](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/paths/~1employers~1{employer_id}~1managers~1{manager_id}~1settings/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Информация по активным услугам API для платных методов](https://api.hh.ru/openapi/redoc#tag/Rabotodatelskie/paths/~1employers~1{employer_id}~1services~1payable_api_actions~1active/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Локализация](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1locales/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Локализация для резюме](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1locales~1resume/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Выбор сайта](docs/hosts.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resume"></a>
### Резюме

* [Поиск резюме](docs/resumes_search.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Сохраненные поиски резюме](docs/resumes_saved_searches.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Список сохраненных поисков резюме](docs/resumes_saved_searches.md#resumes-saved-search-list) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Получение единичного сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-item) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Создание нового сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-create) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Обновление сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-update) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Удаление сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-delete) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Передача сохраненного поиска резюме другому менеджеру](docs/resumes_saved_searches.md#resumes-saved-search-move-to-other-manager) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Просмотр резюме](docs/employer_resumes.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Работа с резюме для соискателя](docs/resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Работа с телефоном](https://api.hh.ru/openapi/redoc#tag/Rezyume.-Rabota-s-telefonom) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Список резюме авторизованного пользователя](docs/resumes.md#mine) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Просмотр резюме](docs/resumes.md#item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Создание и редактирование резюме](docs/resumes.md#create_edit) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Публикация и продление резюме](docs/resumes.md#publish) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Удаление резюме](docs/resumes.md#delete) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [История просмотра резюме](docs/resumes.md#views) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Информация о статусе резюме и готовности резюме к публикации](docs/resumes.md#status-and-publication) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Списки видимости резюме](docs/resume_visibility.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Артефакты (фото, портфолио)](docs/artifacts.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Поиск по вакансиям, похожим на резюме](docs/resumes.md#similar) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [История откликов/приглашений по резюме](docs/resume_negotiations_history.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

<a name="vacancies"></a>
### Вакансии

* [Получение вакансий](docs/vacancies.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Поиск по вакансиям](docs/vacancies.md#search) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
    * [Кластеры](docs/clusters.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
    * [Описание использованных параметров](docs/vacancies_search_arguments.md) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение информации о вакансии](docs/vacancies.md#item) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Особенности работы с вакансиями для соискателя](docs/vacancies_for_applicant.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> 
* [Поиск по вакансиям, похожим на вакансию](docs/vacancies.md#similar) <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Отобранные вакансии](docs/vacancies_for_applicant.md#favorited) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Скрытые вакансии](docs/blacklisted.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Сохраненные поиски вакансий](docs/saved_search.md#vacancies-saved-search-list) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
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
* [Список улучшений для вакансии](docs/employer_vacancy_upgrades.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Статистика по вакансии](docs/employer_vacancies.md#stats) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Черновики вакансий](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение списка черновиков](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Удаление черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts~1{draft_id}/delete) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Создание черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts/post) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Публикация вакансий на основе черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts~1{draft_id}~1publish/post) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts~1%7Bdraft_id%7D/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Изменение черновика](https://api.hh.ru/openapi/redoc#tag/Chernoviki-vakansij/paths/~1vacancies~1drafts~1%7Bdraft_id%7D/put) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="applicants"></a>
### Соискатели

* [Комментарии к соискателю](https://api.hh.ru/openapi/redoc#tag/Kommentarii-k-soiskatelyu) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Авторизация соискателя](https://api.hh.ru/openapi/redoc#tag/Avtorizaciya-soiskatelya) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Соискательские статусы](https://api.hh.ru/openapi/redoc#tag/Soiskatelskie-statusy) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />

<a name="employers"></a>
### Работодатели/компании

* [Поиск компаний](https://api.hh.ru/openapi/redoc#tag/Rabotodatel/paths/~1employers/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Получение информации о компании](https://api.hh.ru/openapi/redoc#tag/Rabotodatel/paths/~1employers~1%7Bemployer_id%7D/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Услуги работодателя](https://api.hh.ru/openapi/redoc#tag/Uslugi-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Авторизация работодателя](https://api.hh.ru/openapi/redoc#tag/Avtorizaciya-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Менеджеры работодателя](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Брендированные шаблоны вакансий](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1vacancy_branded_templates/get) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />

<a name="employer_managers"></a>
### Менеджеры работодателя

* [Менеджеры](docs/employer_managers.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Добавление менеджера](docs/employer_managers.md#add) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Редактирование менеджера](docs/employer_managers.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Удаление менеджера](docs/employer_managers.md#delete) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Справочник менеджеров работодателя](docs/employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение информации о менеджере](docs/employer_managers.md#item) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Дневной лимит просмотра резюме для текущего менеджера](https://api.hh.ru/openapi/redoc#tag/Menedzhery-rabotodatelya/paths/~1employers~1%7Bemployer_id%7D~1managers~1%7Bmanager_id%7D~1limits~1resume/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

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
  * [Список резюме, которыми можно откликнуться на указанную вакансию](docs/suitable_resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Резюме, сгруппированные по возможности отклика на данную вакансию](docs/resumes_by_status.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Переписка для работодателя](docs/employer_negotiations.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Модель работы, термины и процедуры](docs/employer_negotiations.md#model) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Общее описание процесса работы с откликами/приглашениями](docs/employer_negotiations.md#flow) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Коллекции и работодательские состояния откликов/приглашений](docs/employer_negotiations.md#collections) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Список откликов/приглашений](docs/employer_negotiations.md#negotiations-list) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Просмотр отклика/приглашения](docs/employer_negotiations.md#get-negotiation) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Работа с сообщениями по отклику/приглашению для работодателя](docs/employer_negotiations.md#get-messages) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Приглашение соискателя на вакансию](docs/employer_negotiations.md#add-invite) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Действия по отклику/приглашению (смена состояния)](docs/employer_negotiations.md#actions) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
  * [Статистика по работе с откликами](docs/employer_negotiations_statistics.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Тексты сообщений](docs/negotiation_message_templates.md) <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />
* [Инструменты оценки](docs/assessment.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" />


<a name="dictionaries"></a>
### Справочники
* [Справочники в OpenAPI](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Регионы](docs/areas.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Специализации](docs/specializations.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Станции метро в указанном городе](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1metro~1{city_id}/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Станции метро во всех городах](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1metro/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Языки](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1languages/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Отрасли компаний](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1industries/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Учебные заведения](docs/educational_institutions.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Основная информация об учебных заведениях](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1educational_institutions/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Факультеты учебных заведений](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1educational_institutions~1%7Bid%7D~1faculties/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Справочники работодателя](docs/employer_dictionaries.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Адреса](https://api.hh.ru/openapi/redoc#tag/Adresa-rabotodatelya) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Типы и права менеджера](docs/employer_managers.md#dict) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Менеджеры работодателя](docs/employer_managers.md#list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Департаменты](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1departments/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Тесты](https://api.hh.ru/openapi/redoc#tag/Spravochniki-rabotodatelya/paths/~1employers~1%7Bemployer_id%7D~1tests/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Регионы вакансий](docs/employer_vacancy_areas_active.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Брендированные шаблоны вакансий](https://api.hh.ru/openapi/redoc#tag/Informaciya-o-rabotodatele/paths/~1employers~1%7Bemployer_id%7D~1vacancy_branded_templates/get) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Ключевые навыки](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1skills/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Прочие справочники](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/paths/~1dictionaries/get) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


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

* [Отчёты Банка данных заработных плат](docs/salary_reports.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Оценка заработной платы без прогнозов](docs/salary_reports.md#salary-evaluation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Справочники Банка данных заработных плат](docs/salary_dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Отрасли](docs/salary_dictionaries.md#salary-industries) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Уровни специалистов](docs/salary_dictionaries.md#employee-levels) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Профобласти и специализации](docs/salary_dictionaries.md#professional-areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Регионы и города](docs/salary_dictionaries.md#salary-areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/client.png" alt="client" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


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
