# New resume database management model (supported in API)

[We are enacting a new schedule of rates for resume database access as of August 1, 2020](https://hh.ru/article/26941), which uses flat candidate contact quotas.

Employers subscribed to the new rate plan are expected to expressly expose contact details when viewing resumes from the database.

The website has a dedicated "Show Contacts" button to open contact information. In API, the appropriate [links in `actions`](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume) will arrive when [resumes are retrieved by their ID](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume)

> Read the terms of service by following the [link](https://hh.ru/conditions) (para. 3.40.)

> Answers to most questions can be found in the [article](https://hh.ru/article/27029)

For employers who are YET to switch to the new model or never use resume database search in API (and instead only receive responses and invites to their vacancies), nothing will change in the current API behavior—no tweaking is necessary.

## API changes for employers using the database access service with the option to view contact info

Employers subscribed to certain service configurations (more on this in "API and Process Automation" block of the [article](https://hh.ru/article/27029)) will be offered more options on API:

* [Resume search](https://api.hh.ru/openapi/en/redoc#tag/Resume-search/operation/search-for-resumes)
* [Saved resume searches](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/get-saved-resume-searches)

There is a special [method](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-method-access) they can use to find out if they have access to the options listed above

<a name="contact-data"></a>
## Viewing of resumes with contact info

> !Note that there is a cap on the number of requests for the [resume viewing method](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume) in relation to resumes retrieved through the use of [resume database search](https://api.hh.ru/openapi/en/redoc#tag/Resume-search/operation/search-for-resumes). To receive your current request quota, there is a special [method](https://api.hh.ru/openapi/en/redoc#tag/Employer-services/operation/get-payable-api-actions) you can use , "id": "API_LIMITED". Once the quota is exceeded, an error will return when a request is lodged for the [resume viewing method](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume).

Where not a single manager has thus far viewed a resume with contact info, in all places where that [full](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume)
or short resume appears, the resume will be displayed without the contact info (null in the respective fields).

From the moment when a manager of the company has viewed a resume with contact info, the resume will start to be displayed with contact info in all places and for all
managers for as long as the current database access service with the option of viewing contact info remains enabled.

To view and download a resume with contact info in API, dedicated [links in `actions`](https://api.hh.ru/openapi/en/redoc#tag/Resume-view/operation/get-resume) will arrive when resumes are retrieved by their ID.
When those links are used, the contact will be debited to the client. The contact will also be debited when the candidate is invited to fill a vacancy.
However, the debit will happen once only: either when the resume is viewed with the contact info, or when the candidate is offered to fill one of the vacancies in the company.
There will be no debit where the candidate responded first. In this case, the contact info will be visible immediately, without any further action.

Where the employer is subscribed to database access service with the option of viewing contact details, there will be a single debit per contact view.
Where a manager of the company has viewed (whether on the website or via API) a resume with contact info, the resume in question will from that moment on
be available, contacts and all, to any manager of the company.

Contact info is deemed to include:
* Last name (`last_name`), given name (`first_name`), patronymic (`middle_name`);
* Contact phone number (`contact`, `type`==`cell`);
* e-mail (`contact`, `type`==`email`);
* Links to social media profiles or other websites (`site`);
* Photograph (`photo`).

## Viewing contact info in an "anonymous" resume

> Note that when contact details are requested, it may transpire that the user has hidden their contact details. In this case, the viewing will be debited regardless while the reply body will return null in the respective contact data fields. To safeguard against this eventuality, make sure the fields you want are available in hidden_fields the resume.
