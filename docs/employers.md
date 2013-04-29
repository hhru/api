# Работодатель

### `GET /employers/{employer_id}` – информация о работодателе

```json
{
  "id": "ID",
  "name": "HeadHunter",
  "site_url": "http://www.example.com/",
  "type": "company",
  "vacancies_url": "https://api.hh.ru/vacancy?employer_id=ID",
  "description": "<p>Описание в HTML</p>",
  "alternate_url": "http://example.com/employer/ID",
  "trusted": true,
  "logo_urls": {
    "90": "http://example.com/employer-logo/id1.jpeg",
    "240": "http://example.com/employer-logo/id2.jpeg",
    "original": "http://example.com/employer-logo/id3.jpeg"
  },
  "hr_brand": {
    "winner": [2009, 2010],
    "nominee": 2013
  }
}
```
