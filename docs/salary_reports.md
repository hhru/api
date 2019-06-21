# Отчёты Банка данных заработных плат

* [Оценка заработной платы без прогнозов](#salary-evaluation)
    * [Параметры запроса](#salary-evaluation-params)
    * [Примеры запросов](#salary-evaluation-examples)
    * [Успешный ответ](#salary-evaluation-response)
        * [Параметры косвенной оценки зарплат](#salary-evaluation-response-indirect-calculation)
    * [Ошибки](#salary-evaluation-errors)

<a name="salary-evaluation"></a>
## Оценка заработной платы без прогнозов

Метод для получения оценки заработных плат без прогноза.
Требует [авторизации](authorization.md)
и наличия у пользователя доступа к платным отчётам Банка зарплат (см. https://salary.hh.ru).

```
GET /salary_statistics/paid/salary_evaluation/{area_id}
```

где
* `area_id` — код региона (фед. округа, субъекты федерации, города), по которым будет построена выборка для формирования отчёта. См. [справочник регионов](salary_dictionaries.md#salary-areas).

<a name="salary-evaluation-params"></a>
### Параметры запроса

Имя | Обязательный | Описание
--- | --- | ---
exclude_area | Нет | Коды регионов (федеральные округа, субъекты федерации, города), которые будут исключены из выборки для формирования отчёта в любом случае. Параметр предназначен для получения оценки на региональном рынке с исключением определенных городов/областей.  См. [справочник регионов](salary_dictionaries.md#salary-areas)
employee_level | Нет | Уровни специалистов, которые будут включены в выборку для формирования отчёта. См. [справочник уровней специалистов](salary_dictionaries.md#employee-levels)
industry | Нет | Коды отраслей, по которым будет построена выборка для формирования отчёта.  См. [справочник отраслей](salary_dictionaries.md#salary-industries)
speciality | Нет | Коды профобластей и специализаций, которые будут включены в выборку для формирования отчёта. См. [справочник профобластей и специализаций](salary_dictionaries.md#professional-areas)
extend_sources | Нет | Использовать ли данные из резюме и вакансий, если по указанным параметрам не нашлось данных в Банке Зарплат. Принимает значения `true` или `false`. По умолчанию `false`.
position_name | Нет | Наименование должности. Если указано, сервис самостоятельно определит возможные специализации по указанной должности и отрасли. Если специализации явно указаны в запросе, то параметр игнорируется.

<a name="salary-evaluation-examples"></a>
### Примеры запросов

Зарплаты в России, за исключением Москвы и Санкт-Петербурга, для уровня «Специалист»,
в компаниях с отраслями «Информационные технологии» или «Сельское хозяйство»: 

```
GET /salary_statistics/paid/salary_evaluation/113?
    exclude_area=1&
    exclude_area=2&
    employee_level=specialist&
    industry=7&
    industry=29
```

Зарплаты в Москве с уровнями «Ведущий специалист» и «Эксперт»
в специализациях «Управление разработкой ПО» и «Управление проектами».

```
GET /salary_statistics/paid/salary_evaluation/1?
    employee_level=senior_specialist&
    employee_level=expert&
    speciality=1170001&
    speciality=1170002
```

<a name="salary-evaluation-response"></a>
### Успешный ответ

`200 OK`, в теле ответа содержатся данные по зарплатам и параметры выборки:

```json
{
    "market_salary": {
        "upper": 50000,
        "minimum": 20000,
        "median": 35000,
        "average": 50054,
        "maximum": 52643,
        "bottom": 28500
    },
    "resulting_parameters": {
        "areas": [
            {
                "id": "10010",
                "name": "Южный федеральный округ"
            }
        ],
        "excluded_areas": [
            {
                "id": "1530",
                "name": "Ростовская область"
            }
        ],
        "employee_levels": [
            {
                "id": "specialist",
                "name": "Специалист"
            }
        ],
        "industries": [
            {
                "id": "7",
                "name": "Информационные технологии, системная интеграция, интернет"
            }
        ],
        "specialities": [
            {
                "id": "1200000",
                "name": "Эксплуатация информационных систем"
            }
        ],
        "sources": [
            "SALARIES",
            "RESUMES",
            "VACANCIES"
        ],
        "indirect_calculation": null,
        "positions_count": 1648,
        "employers_count": 21
    }
}
```

Имя | Тип | Описание
----|-----|---------
resulting_parameters | object | Набор параметров, по которым происходил расчёт
resulting_parameters.areas | array | Коды регионов (фед. округа, субъекты федерации, города)
resulting_parameters.excluded_areas | array или null | Исключённые коды регионов (фед. округа, субъекты федерации, города)
resulting_parameters.employee_levels | array или null | Уровни специалистов, включаемые в выборку в целевом регионе
resulting_parameters.industries | array или null | Отрасли
resulting_parameters.specialities | array или null | Профобласти
resulting_parameters.sources | array | Используемые источники данных
resulting_parameters.indirect_calculation | object или null | [Параметры косвенной оценки зарплатных значений](#salary-evaluation-response-indirect-calculation)
employers_count | number | Количество работодателей, данные которых участвуют в выборке
positions_count | number | Количество записей о сотрудниках в анкетах, по которым построена выборка
market_salary | object | Рыночный диапазон зарплатных значений
market_salary.maximum | number | Максимальные значения (90-й процентиль)
market_salary.upper | number | Верхняя граница рыночного диапазона (75-й процентиль)
market_salary.median | number | В среднем по рынку (медиана)
market_salary.average | number | Среднее расчетное значение
market_salary.bottom | number | Нижняя граница рыночного диапазона (25-й процентиль)
market_salary.minimum | number | Минимальные значения (10-й процентиль)


<a name="salary-evaluation-response-indirect-calculation"></a>
#### Параметры косвенной оценки зарплат

Поле `resulting_parameters.indirect_calculation` присутствует в ответе только при запросе данных
по одному региону и содержит параметры косвенной оценки зарплат. 

В примере выше вместо `"indirect_calculation": null` может быть объект вида:

```json
{
    "indirect_employee_levels": [
        {
            "id": "senior_specialist",
            "name": "Ведущий специалист"
        }
    ],
    "indirect_areas":[
        {
            "id": "1",
            "name": "Москва"
        }
    ],
    "indirect_regional_ratio": 0.4375
}
```

Имя | Тип | Описание
----|-----|---------
indirect_calculation.indirect_areas | array или null | Регионы, использованные для косвенного расчёта
indirect_calculation.indirect_employee_levels | array или null | Уровни специалистов, включённые в выборку в регионе, использованном для косвенного расчёта
indirect_calculation.indirect_regional_ratio | number | Региональный коэффициент, который был использован для получения косвенной оценки зарплат

Ответ, приведённый выше, означает, что:
* в запрошенном регионе «Южный ФО» (`resulting_parameters.areas`)
* по запрошенному уровню «Специалист» (`resulting_parameters.employee_levels`) данных о зарплатах не нашлось
* но удалось сделать косвенный расчёт
    * относительно уровня «Ведущий специалист» (`resulting_parameters.indirect_calculation.indirect_employee_levels`)
    * в регионе «Москва» (`resulting_parameters.indirect_calculation.indirect_areas`)
    * коэффициент составил 0.4375 (`resulting_parameters.indirect_calculation.indirect_regional_ratio`).

<a name="salary-evaluation-errors"></a>
### Ошибки

* `400 Bad Request` — ошибка в параметрах.
* `403 Forbidden` — нет доступа, или пользователь не авторизован.
* `404 Not Found` — нет данных для указанных параметров.
