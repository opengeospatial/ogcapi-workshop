---
title: Security and OGC APIs
---

# Security and OGC APIs

OGC APIs are designed using modern technologies in order to lower the barrier to geospatial data, services, and processes.

## SSL/TLS

OGC APIs can be deployed using HTTP or HTTPS.  It is strongly recommended to deploy any services using HTTPS so that clients
can validate and verify authenticity of your services accordingly.  Depending on how your system is architected, this may mean
applying Secure Sockets Layer/Transport Layer Security (SSL/TLS) on your service host, or if you have a multi-layered deployment
architecture, applying as part of your front-end services, at which point internal/inner communication may or may not be implemented
using HTTP.

## Access control

Open Standards and APIs are not only for Open Data.  Implementing access control (authentication, authorization) is a critical component
of many infrastructures and systems in order to maintain data integrity, authority and trust.  Examples of requiring access control in
OGC APIs includes (but is not limited to):

- securing all endpoints
- securing only specific endpoints
- allowing insert/update/delete capabilities on items in a collection
- allowing insert/update/delete capabilities on collections

Given that access control concerns, implementations and architectures exist for many domains, it is best to leverage industry standards
for implementation.  Given OGC API standards leverage the OpenAPI specification for service descriptions, one can use the OpenAPI
[Security Scheme Object](https://spec.openapis.org/oas/v3.0.3#security-scheme-object) to describe (not implement!) the access control mechanism(s) for the
entire API as well as for a specific path/operation of the API.

Supported OpenAPI security schemes include:

- API key (`apiKey`)
- HTTP authentication (`http`)
- OAuth2 common flows (`oauth2`)
- OpenID Connect Discovery (`openIdConnect`)


Access control using HTTP Basic authentication:
```json
"security": {
  "default": {
    "type": "http",
    "scheme": "basic",
    "description": "Please contact us for access information"
  }
}
```

Access control using an API key:
```json
"security": {
  "default": {
    "type": "apiKey",
    "name": "api-key",
    "in": "query",
    "description": "Please see https://example.org/contact-us for more information"
  }
}
```

Access control using OAuth2:
```json
"security": {
  "default": {
    "type": "oauth2",
    "authorizationUrl": "https://example.org/oauth/authorize",
    "flow": "implicit",
    "description": "Please see https://example.org/contact-us for more information"
    "scopes": {
        "read:roads": "read roads collection",
        "write:roads": "modify roads in the roads collection"
  }
}
```

!!! note
    Implementing the above assumes that the required access control mechanisms are in place.
