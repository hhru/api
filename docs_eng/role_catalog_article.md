# New catalog of specializations (professional roles). Support in the HeadHunter API.

##### IMPORTANT: Until the integrated system manufacturers support the new catalog, customers can also use the "old" catalog of specializations when publishing, and our service will automatically match the new catalog value to the parameters of the published job ( [more](#backward) ).

Support for using the new specialization catalog (professional roles) is also added to API, as well as [backward compatibility] (#backward) is implemented for integrations that use the old specialization catalog.

All previously published jobs were automatically assigned values from the new professional role catalog, there is no need to additionally modify these jobs.

## Read more about support for the new catalog in the API:

A new catalog of specializations (professional roles, `professional_roles` field) replaces [specializations](specializations.md). Currently, the new catalog of specializations (professional roles) and the outdated catalog of specializations are used in parallel to ensure backward compatibility.

A separate [directory](https://api.hh.ru/openapi/redoc#tag/Spravochniki/paths/~1professional_roles/get) and [prompts (autosuggest, autocomplete)](https://api.hh.ru/openapi/redoc#tag/Spravochniki/paths/~1suggests~1professional_roles/get) are created for the new catalog of specializations (professional roles)

At the moment, support for the new catalog of specializations (professional roles) is not fully completed in the API. Below is a list of methods that support the new catalog (the list will be updated over time)

### For vacancies:


1. [Job posting](employer_vacancies.md#creation) - the `with_professional_roles` parameter and the 'professional_roles' field are added.

2. [Conditions for completing fields when adding and posting jobs](employer_vacancies.md#conditions) - the `with_professional_roles` parameter and the 'professional_roles' field are added.

3. [Viewing jobs](vacancies.md#item) - the `professional_roles` field is added

4. [Draft-based job posting](https://api.hh.ru/openapi/en/redoc#tag/Vacancy-draft/paths/~1vacancies~1drafts~1%7Bdraft_id%7D~1publish/post) - the `with_professional_roles` parameter is added

5. [Vacancy editing](https://github.com/hhru/api/blob/master/docs_eng/employer_vacancies.md#edit) - the `with_professional_roles` parameter is added

#### For resume:

1. [Viewing resumes](resumes.md#item) - the `professional_roles` field is added

2. [Creating and editing resumes](resumes.md#create_edit) - the `with_professional_roles` parameter and the `professional_roles` field are added

3. [Resume posting](resumes.md#publish) - the `with_professional_roles` parameter is added

4. [Conditions for completing the resume fields](resumes.md#conditions) - the `with_professional_roles` parameter and the `professional_roles` field are added

### For search methods:

1. [Resume search](resumes_search.md) - the `professional_role` parameter is added (when using the `specialization` parameter, the backward compatibility mode works, i.e. the value from the 'professional_role' directory will be automatically selected)

2. [Job search](vacancies_search_arguments.md) - the `professional_role` parameter is added (when using the `specialization` parameter, the backward compatibility mode works, i.e. the value from the 'professional_role' directory will be automatically selected)

<a name="backward"></a>
## Backward compatibility of the new catalog in the API:

Backward compatibility will be maintained until **December 1, 2022**. After this deadline, all integrated systems will have to switch completely to the new catalog of specializations (professional roles). Backward compatibility support will be disabled and using [specializations](specializations.md) will result in errors.

The specialization is automatically chosen from the new catalog of specializations (professional roles) after posting a job/resume (previously posted jobs are also automatically assigned values from the new catalog of specializations (professional roles) — no additional steps are required for them) and is based on user experience, as well as user behavior. It means that we will select the best possible vacancy from the new catalog of specializations (professional roles) not on the basis of simple mapping, but on the basis of real user activity (based on statistical patterns in the labor market — groups of resumes and vacancies with applications and invitations to interviews)

For example, when using the job posting method, it is sufficient to pass all the values from the outdated directory of specializations. After posting (with a minor time lag), the most appropriate value from the new directory of specializations (professional roles) will automatically be assigned to this job.
