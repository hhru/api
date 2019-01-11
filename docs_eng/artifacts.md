# Artifacts (photos, portfolios)

Candidates can upload their own files. At the moment these are limited to
images to be attached to resumes (photo and portfolio). On the main site,
this service can be found in the settings, ["images" section](https://hh.ru/applicant/gallery)

After that, these images can be used in the interface for creating/editing
a resume.

* [Get artifacts](#list)
* [Uploading an artifact](#upload)
* [Conditions for uploading artifacts](#conditions)
* [Editing an artifact](#edit)
* [Deleting an artifact](#delete)
* [Attaching a photo/portfolio to a resume](#link-with-resume)


<a name="list"></a>
## Getting artifacts

### Request

```
GET /artifacts/photo
```

```
GET /artifacts/portfolio
```

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "id": "92278992",
            "state": {
                "id": "ok",
                "name": "ok"
            },
            "small": "http://...",
            "medium": "http://...",
            "description": "..."
        }
    ],
    "found": 1,
    "pages": 1,
    "page": 0,
    "per_page": 1
}
```

where for each 'items' element:

<a name="item"></a>

Name | Type | Description
--- | --- | --------
id | string | unique image ID
state | object | current image status
state.id | string | current image status ID
state.name | string | name of the current image status
small | string или null | the url for a cropped image or null if the image is not ready yet
medium | string или null | the url for an average-sized image or null if the image is not ready yet
description | string | description, currently only for `portfolio`

Image statuses:

* `processing` — in process
* `failed` — error, probably format not supported
* `ok` — finished, can be used in the resume

### Errors

* `403 Forbidden` – current user is not a applicant


<a name="upload"></a>
## Uploading an artifact

### Request

```
POST /artifacts
```

To upload a file, send a request `multipart/form-data` with the following parameters:

Name| Required| Description
--- | ------------ | --------
type | yes | type of artifact: `photo` or `portfolio`
description | no | text description, makes sense for `portfolio`
file | yes | file

Restrictions on file types and size can be found in [conditions for uploading artifacts](#conditions).

### Response

Successful response is returned with `201 Created` code and contains:

```json
{
    "id": "123456",
    "medium": null,
    "small": null,
    "state": {
        "id": "processing",
        "name": "in process"
    }
}
```

Response fields are the same as for [element fields in the artifacts list](#item).

### Errors

* `403 Forbidden` – current user is not a applicant
* `400 Bad Request` – error in request parameters or adding an image impossible

In addition to the HTTP code, the server can return a description of the [error reason](errors.md#artifacts).


<a name="conditions"></a>
## Conditions for uploading artifacts

Artifacts uploading conditions are different for each type.

### Request

```
GET /artifacts/photo/conditions
```

```
GET /artifacts/portfolio/conditions
```

### Response

Successful response is returned with `200 OK` code and body:

```json
{
    "fields": {
        "description": {
            "max_length": 255,
            "min_length": 0,
            "required": false
        },
        "file": {
            "max_size": 6291456,
            "mime_type": [
                "image/jpeg",
                "image/png",
                "image/psd"
            ],
            "required": true
        },
        "type": {
            "required": true
        }
    },
    "counters": {
        "max": 20,
        "uploaded": 2
    }
}
```

<a name="conditions-fields"></a>
#### An object `fields`

Name | Type | Description
--- | --- | --------
description | object | conditions for description field
description.required | boolean | is description field required
description.max_length | number | max size of description text field
description.min_length | number | min size of description text field
file | object | conditions for file field
file.max_size | number | max file size
file.mime_type | array | list of allowed files [MIME-types](https://www.iana.org/assignments/media-types/media-types.xhtml)
file.required | boolean | is file field required
type | object | conditions for type field
type.required | boolean | is type field required


<a name="conditions-counters"></a>
#### An object `counters`

Name | Type | Description
--- | --- | --------
max | number | maximum number of artifacts of this type
uploaded | number | number of uploaded artifatcs of this type

### Errors

* `403 Forbidden` – current user is not a applicant


<a name="edit"></a>
## Editing an artifact

```
PUT /artifacts/{id}
```

where `id` is the artifact ID.

Accepted parameters:

* `description` - text description of the image

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – current user is not a applicant
* `404 Not Found` – artifact does not exist or does not belong to the current user
  пользователю
* `400 Bad Request` – error in request parameters or adding an image impossible


<a name="delete"></a>
## Deleting an artifact

```
DELETE /artifacts/{id}
```

where `id` is the artifact ID.

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – current user is not a applicant
* `404 Not Found` – artifact does not exist or does not belong to the current user
  

<a name="link-with-resume"></a>
## Attaching a photo/portfolio to a resume

To attach uploaded photos to the resume, send the artifact `id`
to the [corresponding resume field](resumes.md#resume-fields).
To delete it from the resume indicate `null`.
