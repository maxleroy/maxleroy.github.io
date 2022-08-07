---
layout: page
title: Errors
nav_order: 7
---

## <a href="#errors" id="errors" class="headerlink"></a> Errors

### <a href="#errors-processing" id="errors-processing" class="headerlink"></a> Processing Errors

A server **MAY** choose to stop processing as soon as a problem is encountered,
or it **MAY** continue processing and encounter multiple problems. For instance,
a server might process multiple attributes and then return multiple validation
problems in a single response.

When a server encounters multiple problems for a single request, the most
generally applicable HTTP error code **SHOULD** be used in the response. For
instance, `400 Bad Request` might be appropriate for multiple 4xx errors
or `500 Internal Server Error` might be appropriate for multiple 5xx errors.

### <a href="#error-objects" id="error-objects" class="headerlink"></a> Error Objects

Error objects provide additional information about problems encountered while
performing an operation. Error objects **MUST** be returned as an array
keyed by `errors` in the top level of a JSON:API document.

An error object **MAY** have the following members:

* `id`: a unique identifier for this particular occurrence of the problem.
* `links`: a [links object][links] containing the following members:
    * `about`: a [link][links] that leads to further details about this
      particular occurrence of the problem.
* `status`: the HTTP status code applicable to this problem, expressed as a
  string value.
* `code`: an application-specific error code, expressed as a string value.
* `title`: a short, human-readable summary of the problem that **SHOULD NOT**
  change from occurrence to occurrence of the problem, except for purposes of
  localization.
* `detail`: a human-readable explanation specific to this occurrence of the
  problem. Like `title`, this field's value can be localized.
* `source`: an object containing references to the source of the error,
  optionally including any of the following members:
    * `pointer`: a JSON Pointer [[RFC6901](https://tools.ietf.org/html/rfc6901)]
    to the associated entity in the request document [e.g. `"/data"` for a
      primary data object, or `"/data/attributes/title"` for a specific attribute].
    * `parameter`: a string indicating which URI query parameter caused
      the error.
* `meta`: a [meta object][meta] containing non-standard meta-information about the
  error.
