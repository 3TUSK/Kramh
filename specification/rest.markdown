# SMMART API Definition

SMMART API Definition defines a set of Web API endpoints in RESTful style,
which is the primary way of exchanging data among clients (users) and servers
(databases).

## Synopsis

SMMART API defines the following set of RESTful endpoints:

 - `GET /index/:id`, alias `GET /index/:id/info`
 - `PUT /index/:id`, alias `PUT /index/:id/info`
 - `PATCH /index/:id`, alias `PATCH /index/:id/info`
 - `DELETE /index/:id`, alias `DELETE /index/:id/info`
 - `GET /index/:id/versions`
 - `GET /index/:id/versions/:version`
 - `PUT /index/:id/versions/:version`
 - `PATCH /index/:id/versions/:version`
 - `DELETE /index/:id/versions/:version`
 - `GET /search{?q=keywords}`

## Request

For all requests to endpoints listed here, if their request body is not empty,
then they MUST be a valid JSON Object and be UTF-8 encoded. It is RECOMMENDED
that clients have `Content-Type: application/json; charset=utf-8` in their
request headers.

Implementation MAY raise a `HTTP 415 Unsupported Media Type` error in case that
there is a request failing to do so, and return the following JSON Object as
response body:

```json
{
    "error": "Request MUST be UTF-8-encoded"
}
```

Implementation MAY raise a `HTTP 400 Bad Request` error in case that requests
are encoded in UTF-8 and claim to be JSON, but the request body cannot be
parsed as JSON. In this case, the following JSON Object SHOULD be returned:

```json
{
    "error": "Invalid payload"
}
```

## Authentication

It is REQUIRED that all requests with request method of `PUT`, `PATCH` and
`DELETE` have an `Authorization` field (as described in RFC 7235) in their
request header. The content of this header field MUST be a valid JWT Token as
described in RFC 7519. It is left to the implementation to decide which
algorithm is to use; one MAY choose to use an unsecured token as a placeholder.

In case of failure, or absence of authentication, a `HTTP 401 Unauthorized`
error MUST arise, and the response body SHOULD be:

```json
{
    "error": "Authentication failed"
}
```

In case of success of authentication, if the operation is denied for whatever
reason, a `HTTP 403 Forbidden` error MUST arise, and the response body SHOULD be:

```json
{
    "error": "Permission denied"
}
```

## Response

Unless otherwise noted, all responses MUST have `Content-Type` as:

```
Content-Type: application/json; charset=utf-8
```

That said, all responses MUST have a valid JSON Object as its body that is
encoded in UTF-8.

## Error Handling

Although this specification explicitly defines several rules for implementation
to handle error, server MAY wish to return any HTTP Status Code in order to
describe the error on its best effort. Therefore, client MUST NOT assume that
this specification enumerates over all possible cases of error, and MUST handle
responses with caution.

Implementations that wish to raise error are RECOMMENDED to include a JSON
Object in their payload whenever possible, whose content MUST include a field
named `error` at minimum:

```json
{
    "error": "$reason"
}
```

where `$reason` SHOULD be a brief summary of the error.

## Details

### `GET /index/:id`, `GET /index/:id/info`

Return a JSON Object that complies with the Entry Schema, according to the
requested `id`.

If the database cannot find the data with request ID, a `HTTP 404 Not Found`
error SHOULD arise.

### `PUT /index/:id`, `PUT /index/:id/info`

Create a new entry of mod metadata in the target database via putting a JSON
Object that complies with the Entry Schema in the request body.

In case of success, a `HTTP 201 Created` SHOULD arise.

If there has been a mod metadata entry that occupies the requested `id`, a
`HTTP 409 Conflict` error SHOULD arise, and the response body SHOULD be:

```json
{
    "error": "Id ${id} is already used; consider using another id, change to use PATCH verb, or contact site administrator instead."
}
```

### `PATCH /index/:id`, `PATCH /index/:id/info`

Similar to its `PUT` counterpart, this updates the entry of mod metadata with
the requested `id` in the target database via putting the updated JSON Object
that complies with the Entry Schema in the request body.

In case of success, a `HTTP 200 OK` MUST arise.

In case of that there is no such entry with the requested `id`, it is
RECOMMENDED to raise `HTTP 404 Not Found`, but implementation MAY choose to
fall back to the behavior of `PUT /:id` and thus raise `HTTP 201 Created`
instead.

### `DELETE /index/:id`, `DELETE /index/:id/info`

Purge the entire entry of mod metadata from the target database.

In case of success, a `HTTP 200 OK` MUST arise, and the following MUST be
returned:

```json
{
    "info": "Successfully delete the entire mod entry '${id}'"
}
```

Implementing this endpoint is OPTIONAL. In case of not being implemented, a
`HTTP 405 Method Not Allowed` SHOULD arise, and the response body SHOULD be:

```json
{
    "error": "Deletion is not supported."
}
```

### `GET /index/:id/versions`

Return a JSON Object that complies with the Catalog Schema, according to the
requested `id`. This SHOULD always return `HTTP 200` when possible; if there
is no artifacts data belonging to this mod entry, then the `versions` field
in the returned JSON Object SHOULD be empty JSON Array.

### `GET /index/:id/versions/:version`

Return a JSON Object that complies with the Artifact Schema, according to both
the requested `id` and `version`.
If the database cannot find the data with request ID, a `HTTP 404` error
SHOULD arise.

### `PUT /index/:id/versions/:version`

Upload a JSON Object that complies with the Artifact Schema.

If the database cannot find the data with request ID, a `HTTP 404 Not Found`
error SHOULD arise.

If there has already been an artifact entry with the same `id` and `version`
string in the database, a `HTTP 409 Conflict` error SHOULD arise, and the
response body SHOULD be:

```json
{
    "error": "Mod ${id} already has a version '${version}', consider using PATCH, using a different version string, or contact site administrator instead"
}
```

### `PATCH /index/:id/versions/:version`

Similar to its `PUT` counterpart, this updates the specified mod artifact
metadata according to the requested `id` and `version` in the target database
via putting the updated JSON Object that complies with the Artifact Schema in
the request body.

In case of success, a `HTTP 200 OK` MUST arise.

In case of that there is no such entry with the requested `id`, it is
RECOMMENDED to raise `HTTP 404 Not Found`, but implementation MAY choose to
fall back to the behavior of `PUT /index/:id/versions/:version` and thus
raise `HTTP 201 Created` instead.

### `DELETE /index/:id/versions/:version`

Purge the specific `version` entry in the mod entry with identifier of `id`.

In case of success, a `HTTP 200 OK` MUST arise, and the following SHOULD be
returned:

```json
{
    "info": "Successfully delete version ${version} from mod ${id}"
}
```

Implementing this endpoint is OPTIONAL. In case of not being implemented, a
`HTTP 405 Method Not Allowed` SHOULD arise, and the response body SHOULD be:

```json
{
    "error": "Deletion is not supported."
}
```

### `GET /search{?q=keywords}`

Initiate a query in target database with specified `keywords` as criteria, and
return the query result as a single JSON Object.
