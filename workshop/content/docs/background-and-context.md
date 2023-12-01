---
title: Background and context
---

# Background and context

The geospatial domain has a long history of efforts focused on data discovery, access, and visualization.

This page provides background and history of geospatial web services, web mapping, and distributed computing platforms.

## Geospatial API evolution

The 1990s saw the initial implementation of Service-Oriented Architecture (SOA).  The first OGC Web Map Service (WMS)
standard was published in 1999, providing a vendor-neutral approach to visualizing maps of geospatial data on a web
page.  Web services had strong roots in [XML-RPC (eXtensible Markup Language over Remote Procedure Call)](http://xmlrpc.com/)
and [CORBA](https://www.omg.org/spec/CCM), and standards and technologies such as SOAP, WSDL and UDDI began to emerge
as as means to describe, discover, and perform request/response workflow  a web interface.

The 2000s saw continued development of OGC Web Service standards such as Web Feature Service (WFS), Catalogue Service
for the Web (CSW), Web Coverage Service (WCS), Web Processing Service (WPS), and others.  In addition, Geography Markup Language (GML)
became an official OGC standard in support of standardized (vector) data exchange over the Internet.  Web services
were typically designed with the concept of a relational database model (RDBMS) as the backend data/metadata repository.

In the mid 2000s, JavaScript, AJAX and slippy maps/tiles began to emerge in the web mapping domain, which provided
Web 2.0 design patterns which resulted in more responsive maps on web pages over the Web.

## Realities of web service architectures

OGC Web service standards provided state of the art approaches for data discovery, access, and visualization.  At
the same time, as the concept of Web architecture evolved, various characteristics of Web service standards showed
room for improvement in order to evolve:

- XML: while XML was/is a proven and extensible encoding/representation, working with XML in a web development
  environment proved cumbersome (parsing into dedicated objects).  As well, the verbose nature of XML proved expensive
  for working over the Web for transferring large payloads of data
- Building a specialized transport layer on top of HTTP: HTTP (the protocol) itself provided native request/response
  mechanisms (error codes, content negotiation), which were typically additional defined within Web service standards.
  For example, an HTTP 400 exception natively communicates a faulty request, whereas an HTTP 200 exception indicates
  a successful response.  Web service standards were commonly developed where a 200 response could indicate a faulty
  request (where the client would have to inspect the content of an HTTP response, instead of the actual HTTP status
  code
- Specifications: Web service specifications were typically feature complete and developed with a 100% solution in mind,
  which proved challenging to implement a fully complient server or client, for example
- Web challenges: Web service specifications were difficult to implement for web developers and typically required
  specialized domain expertise in geospatial to interpret and understand specification requirements.  In addition, Web
  services were difficult to integrate with mainstream Internet search engines

## Being webby: a new paradigm

In 2017, the W3C published the [Spatial Data on the Web Best Practices](https://www.w3.org/TR/sdw-bp), which provided
recommendations on data formats, identifiers, access, licensing, and provenance.  The goal of this best practice was
to provide a baseline of recommendations to integrate geosaptial data and services with mainline Web practices and 
design patterns.  In addition, the OGC published the OGC API Whitepaper describing, discussing APIs and next steps
for the OGC at the time.  It became obvious that a "clean break" was needed, in order for OGC APIs to becoe more
"of the Web" and lower barrier for non-domain experts.

A new paradigm emerged, which highlighted the following concepts:

- being webby (humans, search engines)
- developer friendly
- lightweight specification development
- moving from service oriented to resource oriented: removing HTTP use as a tunnel:
    - service oriented: `/ows?request=GetFeature&typename=roads&featureid=5`
    - resource oriented: `/api/collections/roads/items/5`
- modular specification development
  - core and extension specifications, allowing for low barrier implementation and adoption for mass market/the Web
 
In 2018, the OGC began to ran various hackathons, starting work on WFS3 (now OGC API - Features - Part 1: Core), as well as a Weather on the Web
API (now OGC API - Environmental Data Retrieval).  This represented the origins of the OGC API movement!

The development and working processes of OGC standards development themselves evolved during this time.  OGC API specifications began to be
developed on public GitHub repositories, allowing for anyone in the public to discuss and collaboration for a given OGC API standard in the
open on GitHub.  In addition, the specifications themselves began to be developed in AsciiDoc (an open format for documentation/markup), and
made available as HTML pages (and PDF).  Collaborative tools used by OGC also proliferated, such as Gitter/Element as well as Discourse.

!!! note
    OGC standards, while primarily developed on GitHub, continue to be voted on by OGC members.

## Summary

Geospatial Web Services and APIs have been a long running activity in the geospatial domain.  OGC API standards are designed on the lessons
learned of past efforts, and built to be low barrier, with a focus on resources (data/content!) using modern web development
principles and practices.
