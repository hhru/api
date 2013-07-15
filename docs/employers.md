Работодатель / компания
=======================

`GET /employers/{employer_id}` возвращает данные о компании с ссылкой на выдачу вакансий этой компании.

```json
{
	"name": "HeadHunter",
	"type": "company",
	"id": "1455",
	"site_url": "http://hh.ru",
	"description": "...",
	"vacancies_url": "https://api.hh.ru/vacancies?employer_id=1455",
	"trusted": true,
	"alternate_url": "http://hh.ru/employer/1455",
	"logo_urls": {
		"90": "http://hh.ru/employer-logo/289027.png",
		"240": "http://hh.ru/employer-logo/289169.png",
		"original": "http://hh.ru/file/2352807.png"
	}
}
```

`vacancies_url` — ссылка на поисковую выдачу вакансий данной компании.

`logo_urls` — изображения логотипа компании разных размеров. `original` — это необработанный логотип, который может быть большого размера. Если изначально загруженный компанией логотип меньше, чем 240px и/или 90px по меньшей стороне, то в соответствующих ключах будут ссылки на изображения оригинального размера.

`type` — тип компании (прямой работодатель, кадровое агентство и т.п.). Возможные значения описаны в [коллекции справочников](dictionaries.md) под ключом `employer_type`. 

---

Пример: [https://api.hh.ru/employers/1455](https://api.hh.ru/employers/1455)