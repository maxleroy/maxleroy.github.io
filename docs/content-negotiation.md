---
layout: page
title: Content negotiation
nav_order: 2
---

## <a href="#content-negotiation" id="content-negotiation" class="headerlink"></a> Content Negotiation

### <a href="#content-negotiation-clients" id="content-negotiation-clients" class="headerlink"></a> Client Responsibilities

Clients **MUST** send all JSON:API data in request documents with the header
`Content-Type: application/vnd.api+json` without any media type parameters.

Clients that include the JSON:API media type in their `Accept` header **MUST**
specify the media type there at least once without any media type parameters.

Clients **MUST** ignore any parameters for the `application/vnd.api+json`
media type received in the `Content-Type` header of response documents.

### <a href="#content-negotiation-servers" id="content-negotiation-servers" class="headerlink"></a> Server Responsibilities

Servers **MUST** send all JSON:API data in response documents with the header
`Content-Type: application/vnd.api+json` without any media type parameters.

Servers **MUST** respond with a `415 Unsupported Media Type` status code if
a request specifies the header `Content-Type: application/vnd.api+json`
with any media type parameters.

Servers **MUST** respond with a `406 Not Acceptable` status code if a
request's `Accept` header contains the JSON:API media type and all instances
of that media type are modified with media type parameters.

> Note: The content negotiation requirements exist to allow future versions
of this specification to use media type parameters for extension negotiation
and versioning.