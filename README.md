# HeadHunter API

**По-русски** | [In english](https://github.com/hhru/api/blob/master/docs_eng/README.md)

HeadHunter API — это бесплатный инструментарий для интеграции
[HeadHunter](http://hh.ru/) в ваш продукт.

Для начала ознакомьтесь с [общей информацией](https://github.com/hhru/api/blob/master/docs/general.md) по работе API и
с требованиями к [использованию логотипов](https://dev.hh.ru/articles/logos) и
[названию приложений](https://dev.hh.ru/articles/apps).

Для использования сервисов, требующих авторизацию пользователя, вам необходимо
зарегистрировать приложение по адресу [https://dev.hh.ru](https://dev.hh.ru)
и настроить процесс [авторизации](https://github.com/hhru/api/blob/master/docs/authorization.md).


<a name="content"></a>
## Содержание

Пометки в документации:

* <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> –
  актуально для анонимных запросов, не требует авторизации.
* <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> –
  актуально для запросов от имени соискателя, требует авторизацию.
* <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" /> –
  актуально для запросов от имени работодателя, требует авторизацию.


<a name="general"></a>
### Общая информация

* [Общая информация](https://github.com/hhru/api/blob/master/docs/general.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Условия использования сервиса API](https://dev.hh.ru/admin/developer_agreement) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Требования к использованию логотипов](https://dev.hh.ru/articles/logos) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Требования к названию приложений](https://dev.hh.ru/articles/apps) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Авторизация](https://github.com/hhru/api/blob/master/docs/authorization.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Ошибки и коды ответов](https://github.com/hhru/api/blob/master/docs/errors.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resources"></a>
<a name="context"></a>
### Контекст

* [Информация об авторизованном пользователе](https://github.com/hhru/api/blob/master/docs/me.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Предпочтения менеджера](https://github.com/hhru/api/blob/master/docs/manager_settings.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Локализация](https://github.com/hhru/api/blob/master/docs/locales.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Выбор сайта](https://github.com/hhru/api/blob/master/docs/hosts.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="resume"></a>
### Резюме

* [Поиск резюме](https://github.com/hhru/api/blob/master/docs/employer_resumes.md#search) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Сохраненные поиски резюме](https://github.com/hhru/api/blob/master/docs/saved_search.md#resumes-saved-search-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Просмотр резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#item) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Работа с резюме для соискателя](https://github.com/hhru/api/blob/master/docs/resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Список резюме авторизованного пользователя](https://github.com/hhru/api/blob/master/docs/resumes.md#mine) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Создание и редактирование резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#create_edit) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Публикация и продление резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#publish) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [История просмотра резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#views) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Артефакты (фото, портфолио)](https://github.com/hhru/api/blob/master/docs/artifacts.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Поиск по вакансиям, похожим на резюме](https://github.com/hhru/api/blob/master/docs/resumes.md#similar) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />

<a name="vacancies"></a>
### Вакансии

* [Получение вакансий](https://github.com/hhru/api/blob/master/docs/vacancies.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Поиск по вакансиям](https://github.com/hhru/api/blob/master/docs/vacancies.md#search) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Получение информации о вакансии](https://github.com/hhru/api/blob/master/docs/vacancies.md#item) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Поиск по вакансиям, похожим на вакансию](https://github.com/hhru/api/blob/master/docs/vacancies.md#similar) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Отобранные вакансии](https://github.com/hhru/api/blob/master/docs/vacancies.md#favorited) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Скрытые вакансии](https://github.com/hhru/api/blob/master/docs/blacklisted.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Работа с вакансиями](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Публикация вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#creation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Редактирование вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#edit) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Продление вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#prolongate) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Список опубликованных вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#active) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Архивация вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#archive) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Список архивных вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#archived) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Удаление вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#hide) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Список удаленных вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancies.md#hidden) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Сохраненные поиски вакансий](https://github.com/hhru/api/blob/master/docs/saved_search.md#vacancies-saved-search-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />

<a name="applicants"></a>
### Соискатели

* [Комментарии к соискателю](https://github.com/hhru/api/blob/master/docs/applicant_comments.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="employers"></a>
### Работодатели/компании

* [Поиск компаний](https://github.com/hhru/api/blob/master/docs/employers.md#search) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Получение информации о компании](https://github.com/hhru/api/blob/master/docs/employers.md#item) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="negotiations"></a>
### Переписка (отклики/приглашения)

* [Переписка для соискателя](https://github.com/hhru/api/blob/master/docs/negotiations.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Получение списка откликов](https://github.com/hhru/api/blob/master/docs/negotiations.md#get_negotiations) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Откликнуться на вакансию](https://github.com/hhru/api/blob/master/docs/negotiations.md#post_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Просмотр отклика/приглашения](https://github.com/hhru/api/blob/master/docs/negotiations.md#get_negotiation) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Просмотр списка сообщений в отклике](https://github.com/hhru/api/blob/master/docs/negotiations.md#get_messages) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
  * [Отправка сообщений в отклике](https://github.com/hhru/api/blob/master/docs/negotiations.md#send_message) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Список резюме для отклика на указанную вакансию](https://github.com/hhru/api/blob/master/docs/suitable_resumes.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" />
* [Переписка для работодателя](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Модель работы, термины и процедуры](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#model) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Общее описание процесса работы с откликами/приглашениями](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#flow) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Коллекции и работодательские состояния откликов/приглашений](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#collections) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Список откликов/приглашений](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#negotiations-list) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Просмотр отклика/приглашения](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#get-negotiation) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Работа с сообщениями по отклику/приглашению для работодателя](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#get-messages) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Приглашение соискателя на вакансию](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#add-invite) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [Действия по отклику/приглашению (смена состояния)](https://github.com/hhru/api/blob/master/docs/employer_negotiations.md#actions) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Тексты сообщений](https://github.com/hhru/api/blob/master/docs/negotiation_message_templates.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Инструменты оценки](https://github.com/hhru/api/blob/master/docs/assessment.md) <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="dictionaries"></a>
### Справочники

* [Регионы](https://github.com/hhru/api/blob/master/docs/areas.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Специализации](https://github.com/hhru/api/blob/master/docs/specializations.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Метро](https://github.com/hhru/api/blob/master/docs/metro.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Языки](https://github.com/hhru/api/blob/master/docs/languages.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Отрасли компаний](https://github.com/hhru/api/blob/master/docs/industries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Справочники работодателя](https://github.com/hhru/api/blob/master/docs/employer_dictionaries.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Адреса](https://github.com/hhru/api/blob/master/docs/employer_addresses.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Менеджеры](https://github.com/hhru/api/blob/master/docs/employer_managers.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Департаменты](https://github.com/hhru/api/blob/master/docs/employer_departments.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Тесты](https://github.com/hhru/api/blob/master/docs/employer_tests.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Регионы вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancy_areas_active.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
  * [Брендированные шаблоны вакансий](https://github.com/hhru/api/blob/master/docs/employer_vacancy_branded_templates.md) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
* [Прочие справочники](https://github.com/hhru/api/blob/master/docs/dictionaries.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


<a name="suggests"></a>
### Подсказки (autosuggest, autocomplete)

* [Подсказки](https://github.com/hhru/api/blob/master/docs/suggests.md) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по названиям университетов](https://github.com/hhru/api/blob/master/docs/suggests.md#educational_institutions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по организациям](https://github.com/hhru/api/blob/master/docs/suggests.md#companies) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по специализациям](https://github.com/hhru/api/blob/master/docs/suggests.md#specializations) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по ключевым навыкам](https://github.com/hhru/api/blob/master/docs/suggests.md#key-skills) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по должностям](https://github.com/hhru/api/blob/master/docs/suggests.md#positions) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по регионам](https://github.com/hhru/api/blob/master/docs/suggests.md#areas) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по ключевым словам поиска резюме](https://github.com/hhru/api/blob/master/docs/suggests.md#resume-search-keyword) <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />
 * [по ключевым словам поиска вакансий](https://github.com/hhru/api/blob/master/docs/suggests.md#vacancy-search-keyword) <img src="http://hhru.github.io/api/badges/anon.png" alt="anonymous" /> <img src="http://hhru.github.io/api/badges/app.png" alt="applicant" /> <img src="http://hhru.github.io/api/badges/emp.png" alt="employer" />


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
[напишите в поддержку по сайту](http://hh.ru/feedback) или в
[сообщество поддержки](http://feedback.hh.ru/).

За новостями вы можете следить по
[коммитам](https://github.com/hhru/api/commits/master) в этом репозитории.
[RSS](https://github.com/hhru/api/commits/master.atom).
