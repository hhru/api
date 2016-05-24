# Manager preferences

<a name="manager_settings"></a>
### Request

`GET /employers/{employer_id}/managers/{manager_id}/settings`

where:

* `employer_id` – employer ID,
* `manager_id` – manager ID.

The easiest way to get URL is to use `manager_settings_url` in
[details on current user (object `manager`)](me.md#manager-info).


### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
  "default_currency": {
    "abbr": "rub.",
    "code": "RUR",
    "name": "Rubles"
  },
  "default_vacancy_branded_template": {
    "id": "default",
    "name": "Standard template"
  },
  "use_sms_notification": true
}
```

Name | Type | Description
--- | --- | ------
default_currency | object | preferred currency for [posting vacancy](employer_vacancies.md#creation)
default_vacancy_branded_template | object, null | preferred [branded employer vacancy template](employer_vacancy_branded_templates.md). `null` – company doesn't use branded vacancy templates.
use_sms_notification | logical | preference for using `send_sms` option [upon applicant invitation](employer_negotiations.md#add-invite)

These preferences **don't affect** default API actions. For example:
branded design template (`default_vacancy_branded_template`) won't
be automatically applied to the posted vacancy if the template is not transferred.
Preferences can use your application to realize the logic
of the field pre-filling.

### Errors

* `404 Not Found` – manager doesn't exist or the review of its options is not available.
* `403 Forbidden` – current user is not a manager.
