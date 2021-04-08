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


> ‼️ Обратите внимание на [описание](docs/payable/resume.md) новой модели работы с базой резюме. 

> Доступ к ряду методов для работодателя [платный](docs/payable/employer_methods.md). 

> Для уточнения стоимости API необходимо обратиться к Вашему персональному менеджеру или позвонить по телефону: 
> +7 495 974-64-27 (для Москвы и Подмосковья),  
> +7 812 458-45-45 (для Санкт-Петербурга),  
> 8 800 100-64-27 (для регионов России).

<a name="content"></a>
## Содержание

Пометки в документации:

* ![anonymous](./newbages/anonymous.png) –
  актуально для анонимных запросов, не требует авторизации.
* ![application](./newbages/application.png) – актуально для запросов от имени приложения, требует [авторизацию приложения](docs/authorization_for_application.md)
* ![applicant](./newbages/applicant.png) –
  актуально для запросов от имени соискателя, требует [авторизацию пользователя](docs/authorization_for_user.md).
* ![employer](./newbages/employer_free.png) –
  актуально для бесплатных методов работодателя, требует  [авторизацию пользователя](docs/authorization_for_user.md).
* ![employer with paid access](./newbages/employer_paid.png) –
  актуально для [платных](docs/payable/employer_methods.md) методов работодателя, требует  [авторизацию пользователя](docs/authorization_for_user.md).


<a name="general"></a>
### Общая информация

* [Общая информация](docs/general.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Условия использования сервиса API](https://dev.hh.ru/admin/developer_agreement) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Требования к использованию логотипов](https://dev.hh.ru/articles/logos) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Требования к названию приложений](https://dev.hh.ru/articles/apps) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Авторизация](docs/authorization.md) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Кэширование](docs/cache.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Ошибки и коды ответов](docs/errors.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Платный доступ для работодателей к некоторым методом API](docs/payable/employer_methods.md) ![employer with paid access](./newbages/employer_paid.png)
* [Новая модель работы с базой резюме (поддержка в API)](docs/payable/resume.md) ![employer](./newbages/employer_free.png)

<a name="resources"></a>
<a name="context"></a>
### Контекст

* [Информация об авторизованном пользователе или приложении](docs/me.md) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Получение информации об авторизованном пользователе](docs/me.md#user-info) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Редактирование информации авторизованного пользователя](docs/me.md#user-edit) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Получение информации об авторизованном приложении](docs/me.md#application-info) ![application](./newbages/application.png)
* Информация о менеджере
  * [Рабочие аккаунты менеджера](docs/manager_accounts.md) ![employer](./newbages/employer_free.png)
  * [Предпочтения менеджера](docs/manager_settings.md) ![employer](./newbages/employer_free.png)
* [Информация по активным услугам API для платных методов](docs/payable/employer_services.md#payable-api-actions) ![employer](./newbages/employer_free.png)
* [Локализация](docs/locales.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Выбор сайта](docs/hosts.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)


<a name="resume"></a>
### Резюме

* [Поиск резюме](docs/resumes_search.md) ![employer with paid access](./newbages/employer_paid.png)
* [Сохраненные поиски резюме](docs/resumes_saved_searches.md) ![employer with paid access](./newbages/employer_paid.png)
  * [Список сохраненных поисков резюме](docs/resumes_saved_searches.md#resumes-saved-search-list) ![employer with paid access](./newbages/employer_paid.png)
  * [Получение единичного сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-item) ![employer with paid access](./newbages/employer_paid.png)
  * [Создание нового сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-create) ![employer with paid access](./newbages/employer_paid.png)
  * [Обновление сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-update) ![employer with paid access](./newbages/employer_paid.png)
  * [Удаление сохраненного поиска резюме](docs/resumes_saved_searches.md#resumes-saved-search-delete) ![employer with paid access](./newbages/employer_paid.png)
  * [Передача сохраненного поиска резюме другому менеджеру](docs/resumes_saved_searches.md#resumes-saved-search-move-to-other-manager) ![employer with paid access](./newbages/employer_paid.png)
* [Просмотр резюме](docs/resumes.md#item) ![applicant](./newbages/applicant.png) ![employer with paid access](./newbages/employer_paid.png)
* [Работа с резюме для соискателя](docs/resumes.md) ![applicant](./newbages/applicant.png)
  * [Список резюме авторизованного пользователя](docs/resumes.md#mine) ![applicant](./newbages/applicant.png)
  * [Создание и редактирование резюме](docs/resumes.md#create_edit) ![applicant](./newbages/applicant.png)
  * [Публикация и продление резюме](docs/resumes.md#publish) ![applicant](./newbages/applicant.png)
  * [Удаление резюме](docs/resumes.md#delete) ![applicant](./newbages/applicant.png)
  * [История просмотра резюме](docs/resumes.md#views) ![applicant](./newbages/applicant.png)
  * [Информация о статусе резюме и готовности резюме к публикации](docs/resumes.md#status-and-publication) ![applicant](./newbages/applicant.png)
  * [Списки видимости резюме](docs/resume_visibility.md) ![applicant](./newbages/applicant.png)
* [Артефакты (фото, портфолио)](docs/artifacts.md) ![applicant](./newbages/applicant.png)
* [Поиск по вакансиям, похожим на резюме](docs/resumes.md#similar) ![applicant](./newbages/applicant.png)
* [История откликов/приглашений по резюме](docs/resume_negotiations_history.md) ![employer with paid access](./newbages/employer_paid.png)

<a name="vacancies"></a>
### Вакансии

* [Получение вакансий](docs/vacancies.md) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Поиск по вакансиям](docs/vacancies.md#search) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
    * [Кластеры](docs/clusters.md) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
    * [Описание использованных параметров](docs/vacancies_search_arguments.md) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Получение информации о вакансии](docs/vacancies.md#item) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Поиск по вакансиям, похожим на вакансию](docs/vacancies.md#similar) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Отобранные вакансии](docs/vacancies.md#favorited) ![applicant](./newbages/applicant.png)
* [Скрытые вакансии](docs/blacklisted.md) ![applicant](./newbages/applicant.png)
* [Сохраненные поиски вакансий](docs/saved_search.md#vacancies-saved-search-list) ![applicant](./newbages/applicant.png)
* [Работа с вакансиями](docs/employer_vacancies.md) ![employer](./newbages/employer_free.png)
  * [Возможные варианты публикации вакансий](docs/employer_vacancies.md#available_types) ![employer](./newbages/employer_free.png)
  * [Публикация вакансий](docs/employer_vacancies.md#creation) ![employer](./newbages/employer_free.png)
  * [Редактирование вакансий](docs/employer_vacancies.md#edit) ![employer](./newbages/employer_free.png)
  * [Продление вакансий](docs/employer_vacancies.md#prolongate) ![employer](./newbages/employer_free.png)
  * [Список опубликованных вакансий](docs/employer_vacancies.md#active) ![employer](./newbages/employer_free.png)
  * [Архивация вакансий](docs/employer_vacancies.md#archive) ![employer](./newbages/employer_free.png)
  * [Список архивных вакансий](docs/employer_vacancies.md#archived) ![employer](./newbages/employer_free.png)
  * [Удаление вакансий](docs/employer_vacancies.md#hide) ![employer](./newbages/employer_free.png)
  * [Список удаленных вакансий](docs/employer_vacancies.md#hidden) ![employer](./newbages/employer_free.png)
* [Статистика по вакансии](docs/employer_vacancies.md#stats) ![employer](./newbages/employer_free.png)

<a name="applicants"></a>
### Соискатели

* [Комментарии к соискателю](docs/applicant_comments.md) ![employer with paid access](./newbages/employer_paid.png)


<a name="employers"></a>
### Работодатели/компании

* [Поиск компаний](docs/employers.md#search) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Получение информации о компании](docs/employers.md#item) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)

<a name="employer_managers"></a>
### Менеджеры работодателя

* [Менеджеры](docs/employer_managers.md) ![employer](./newbages/employer_free.png)
  * [Добавление менеджера](docs/employer_managers.md#add) ![employer](./newbages/employer_free.png)
  * [Редактирование менеджера](docs/employer_managers.md#edit) ![employer](./newbages/employer_free.png)
  * [Удаление менеджера](docs/employer_managers.md#delete) ![employer](./newbages/employer_free.png)
  * [Справочник менеджеров работодателя](docs/employer_managers.md#list) ![employer](./newbages/employer_free.png)
  * [Получение информации о менеджере](docs/employer_managers.md#item) ![employer](./newbages/employer_free.png)
  * [Дневной лимит просмотра резюме для текущего менеджера](docs/employer_manager_resume_limit.md) ![employer](./newbages/employer_free.png)

<a name="negotiations"></a>
### Переписка (отклики/приглашения)

* [Переписка для соискателя](docs/negotiations.md) ![applicant](./newbages/applicant.png)
  * [Получение списка откликов](docs/negotiations.md#get_negotiations) ![applicant](./newbages/applicant.png)
  * [Получение списка активных откликов](docs/negotiations.md#get_negotiations_active) ![applicant](./newbages/applicant.png)
  * [Откликнуться на вакансию](docs/negotiations.md#post_negotiation) ![applicant](./newbages/applicant.png)
  * [Просмотр отклика/приглашения](docs/negotiations.md#get_negotiation) ![applicant](./newbages/applicant.png)
  * [Скрыть отклик](docs/negotiations.md#hide_message) ![applicant](./newbages/applicant.png)
  * [Просмотр списка сообщений в отклике](docs/negotiations.md#get_messages) ![applicant](./newbages/applicant.png)
  * [Отправка сообщений в отклике](docs/negotiations.md#send_message) ![applicant](./newbages/applicant.png)
  * [Редактирование сообщения в отклике](docs/negotiations.md#edit_message) ![applicant](./newbages/applicant.png)
* Резюме для отклика на указанную вакансию ![applicant](./newbages/applicant.png)
  * [Список резюме, которыми можно откликнуться на указанную вакансию](docs/suitable_resumes.md) ![applicant](./newbages/applicant.png)
  * [Резюме, сгруппированные по возможности отклика на данную вакансию](docs/resumes_by_status.md) ![applicant](./newbages/applicant.png)
* [Переписка для работодателя](docs/employer_negotiations.md) ![employer with paid access](./newbages/employer_paid.png)
  * [Модель работы, термины и процедуры](docs/employer_negotiations.md#model) ![employer with paid access](./newbages/employer_paid.png)
  * [Общее описание процесса работы с откликами/приглашениями](docs/employer_negotiations.md#flow) ![employer with paid access](./newbages/employer_paid.png)
  * [Коллекции и работодательские состояния откликов/приглашений](docs/employer_negotiations.md#collections) ![employer with paid access](./newbages/employer_paid.png)
  * [Список откликов/приглашений](docs/employer_negotiations.md#negotiations-list) ![employer with paid access](./newbages/employer_paid.png)
  * [Просмотр отклика/приглашения](docs/employer_negotiations.md#get-negotiation) ![employer with paid access](./newbages/employer_paid.png)
  * [Работа с сообщениями по отклику/приглашению для работодателя](docs/employer_negotiations.md#get-messages) ![employer with paid access](./newbages/employer_paid.png)
  * [Приглашение соискателя на вакансию](docs/employer_negotiations.md#add-invite) ![employer with paid access](./newbages/employer_paid.png)
  * [Действия по отклику/приглашению (смена состояния)](docs/employer_negotiations.md#actions) ![employer with paid access](./newbages/employer_paid.png)
  * [Статистика по работе с откликами](docs/employer_negotiations_statistics.md) ![employer with paid access](./newbages/employer_paid.png)
* [Тексты сообщений](docs/negotiation_message_templates.md) ![employer with paid access](./newbages/employer_paid.png)
* [Инструменты оценки](docs/assessment.md) ![applicant](./newbages/applicant.png) ![employer with paid access](./newbages/employer_paid.png)


<a name="dictionaries"></a>
### Справочники

* [Регионы](docs/areas.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Специализации](docs/specializations.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Метро](docs/metro.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Языки](docs/languages.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Отрасли компаний](docs/industries.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Учебные заведения](docs/educational_institutions.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Основная информация об учебных заведениях](docs/university.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Факультеты учебных заведений](docs/faculties.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Справочники работодателя](docs/employer_dictionaries.md) ![employer](./newbages/employer_free.png)
  * [Адреса](docs/employer_addresses.md) ![employer](./newbages/employer_free.png)
  * [Типы и права менеджера](docs/employer_managers.md#dict) ![employer](./newbages/employer_free.png)
  * [Менеджеры работодателя](docs/employer_managers.md#list) ![employer](./newbages/employer_free.png)
  * [Департаменты](docs/employer_departments.md) ![employer](./newbages/employer_free.png)
  * [Тесты](docs/employer_tests.md) ![employer](./newbages/employer_free.png)
  * [Регионы вакансий](docs/employer_vacancy_areas_active.md) ![employer](./newbages/employer_free.png)
  * [Брендированные шаблоны вакансий](docs/employer_vacancy_branded_templates.md) ![employer](./newbages/employer_free.png)
* [Ключевые навыки](docs/key_skills.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
* [Прочие справочники](docs/dictionaries.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)


<a name="suggests"></a>
### Подсказки (autosuggest, autocomplete)

* [Подсказки](docs/suggests.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по названиям университетов](docs/suggests.md#educational_institutions) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по организациям](docs/suggests.md#companies) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по специализациям](docs/suggests.md#specializations) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по ключевым навыкам](docs/suggests.md#key-skills) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по должностям](docs/suggests.md#positions) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по регионам](docs/suggests.md#areas) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [по ключевым словам поиска вакансий](docs/suggests.md#vacancy-search-keyword) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)


<a name="salary"></a>
### Банк данных заработных плат

* [Отчёты Банка данных заработных плат](docs/salary_reports.md) ![employer](./newbages/employer_free.png)
  * [Оценка заработной платы без прогнозов](docs/salary_reports.md#salary-evaluation) ![employer](./newbages/employer_free.png)
* [Справочники Банка данных заработных плат](docs/salary_dictionaries.md) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Отрасли](docs/salary_dictionaries.md#salary-industries) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Уровни специалистов](docs/salary_dictionaries.md#employee-levels) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Профобласти и специализации](docs/salary_dictionaries.md#professional-areas) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)
  * [Регионы и города](docs/salary_dictionaries.md#salary-areas) ![anonymous](./newbages/anonymous.png) ![application](./newbages/application.png) ![applicant](./newbages/applicant.png) ![employer](./newbages/employer_free.png)


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
