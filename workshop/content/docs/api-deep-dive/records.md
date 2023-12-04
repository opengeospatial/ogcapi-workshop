---
title: OGC API - Records
---

# OGC API - Records

!!! abstract Audience
    Students that are familiar with web services and APIs, and want to have
    an overview of OGC API - Records standard

!!! abstract "Learning Objectives"
    At the completion of the module students will be able to:

    - Explain what the OGC API - Records standard is
    - Describe what can be done with OGC API - Records implementations
    - Understand the main resources offered by OGC API - Records implementations
    - Understand how to retrieve a description of the capabilities of an
      OGC API - Records implementation
    - Understand how to issue requests to an implementation of OGC API - Records
    - Be able to find an OGC API - Records endpoint and use it through a client

## Introduction

[OGC API - Records](https://ogcapi.ogc.org/records) is a multi-part draft specification that offers the capability to
create, modify, and query metadata on the Web. The draft specification enables the
discovery of geospatial resources by standardizing the way collections of descriptive
information about the resources (metadata) are exposed.  The draft specification also
enables the discovery and sharing of related resources that may be referenced from
geospatial resources or their metadata by standardizing the way all kinds of records
are exposed and managed.  Part 1 covers read-only access to records and simple query
capabilities.  Additional capabilities that address specific needs will be specified
in additional parts. Capabilities for richer queries or to create, update or delete
records will be specified in additional parts.

!!! note
    OGC API - Records leverages [OGC API - Features](features.md#usage) as a baseline with similar
    URL endpoints and request/response workflow, for the Searchable Catalog and Local.

### Background

> History

  OGC API - Records standard work was started in 2018 and originally referred to as
  **OGC CAT4.0**.  It has since followed the development of OGC API - Features as a baseline.

> Versions

  **OGC API - Records - Part 1: Core** is currently in draft and is planned to be
  submitted to the OGC Architecture Board (OAB) in December 2023 for public review
  in Q1 2024.

> Test suite

  There are no test suites currently implemented; they will be made available once
  the specification is approved, and an executable test suite (ETS) is made availabe
  as per of OGC CITE.

> Implementations

  Implementations can be found on the [implementations page](https://github.com/opengeospatial/ogcapi-records/blob/master/implementations.md).


#### Usage

OGC API - Records supports 3 main deployment patterns:

- Crawlable catalog: browse and navigation of a set of metadata records via links
- Searchable catalog: API capability to query and filter a collection of metadata records based on serch criteria (bbox, datetime, q, etc.)
- Local resources catalog: searchable catalog functionality applied at the collection level of an API

OGC API - Records also supports a core queryable model.  That is, a set of common queryable properties that can be used against any
OGC API - Records server regardless of the metadata format/standard and/or the design of the underlying metadata repository.

!!! note
    For the purposes of this deep dive, we will focus on the Searchable catalog deployment pattern.

#### Relation to other standards

OGC Catalogue Service for the Web (CSW): The CSW standard is more appropriate when working with client applications that only support classic OGC Web Services. Note as well that CSW adopts a core metadata model based on Dublin Core by default. In contrast, OGC API - Records includes recommendations to support HTML and GeoJSON as encodings, where practical. Implementations of OGC API - Records may also optionally support XML metadata formats, such as ISO 19115/19139.


### Overview of Resources

**OGC API - Records - Part 1: Core** defines the resources listed in
the following table.

<table>
  <tr>
    <th>Resource</th>
    <th>Method</th>
    <th>Path</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Landing page</td>
    <td>GET</td>
    <td>/</td>
    <td>This is the top-level resource, which serves as an entry point.</td>
  </tr>
  <tr>
    <td>Conformance declaration</td>
    <td>GET</td>
    <td>/conformance</td>
    <td>This resource presents information about the functionality that is implemented by the server.</td>
  </tr>
  <tr>
    <td>API definition</td>
    <td>GET</td>
    <td>/api</td>
    <td>This resource provides metadata about the API itself. Note use of /api on the server is optional and the API definition may be hosted on completely separate server.</td>
  </tr>
  <tr>
    <td>Record collections</td>
    <td>GET</td>
    <td>/collections</td>
    <td>This resource lists the record collections that are offered through the API.</td>
  </tr>
  <tr>
    <td>Record collection</td>
    <td>GET</td>
    <td>/collections/{collectionId}</td>
    <td>This resource describes the record collection identified in the path.</td>
  </tr>
  <tr>
    <td>Records access</td>
    <td>GET</td>
    <td>/collections/{collectionId}/items</td>
    <td>This resource presents the records that are contained in the collection.</td>
  </tr>
  <tr>
    <td>Record core</td>
    <td>GET</td>
    <td>/collections/{collectionId}/items/{recordId}</td>
    <td>This resource presents the record that is identified in the path</td>
  </tr>
</table>

As mentioned earlier, OGC API - Records heavily leverages OGC API - Features as a baseline building block.  While OGC API - Records
allows for any metadata model, a key difference and value add is the ability to describe a core record model and queryables.  This
allows for interoperability and integration across catalogs to be able to describe geospatial resources in a consistent manner.

For example, a metadata repository can be modelled after the ISO 19115 standard, and be exposed via OGC API - Records by means
of "mapping" the ISO elements to the core record model and queryables.

The core record is the atomic unit of information in a catalog.  A full description of the core properties of a record can be
found in <https://docs.ogc.org/DRAFTS/20-004.html#core-properties>.  The core record is a GeoJSON compatible representation
with fixed elements in the `properties` object/block.

### Example

This [demonstration server](https://demo.pygeoapi.io/master) publishes metadata geospatial data through an interface that conforms to OGC API - Records.

An example request that can be used to retrieve data from the Sample metadata records from Dutch Nationaal georegister record collection is <https://demo.pygeoapi.io/master/collections/dutch-metadata?f=html>

Note that the response to the request is HTML in this case.

Alternatively, the same data can be retrieved in GeoJSON format, through the request <https://demo.pygeoapi.io/master/collections/dutch-metadata?f=json>

A client application can then retrieve the GeoJSON document and display or process it.

## Resources

### Landing page

Given OGC API - Records uses OGC API - Common and OGC API - Features as building blocks, please see the [OGC API - Features](features.md#landing-page) deep dive
for a detailed explanation.

### Conformance declarations

Given OGC API - Records uses OGC API - Common and OGC API - Features as building blocks, please see the [OGC API - Features](features.md#conformance-declarations) deep dive
for a detailed explanation.

### API Definition

Given OGC API - Records uses OGC API - Common as a building block, please see the [OGC API - Features](features.md#api-definition) deep dive
for a detailed explanation of an example implementation.

### Records collections

Given OGC API - Records uses OGC API - Common and OGC API - Features as building blocks, please see the [OGC API - Features](features.md#feature-collections) deep dive
for a detailed initial explanation.

OGC API - Records collection descriptions provide the following additional properties:

- A required title for the collection
- A required type for the collection
- A required indicator about the type of the items in the collection (`record`)

Below is an extract from the response to the request <https://demo.pygeoapi.io/master/collections?f=json>
illustrating a single record collection:

```json
{
    "id": "dutch-metadata",
    "type": "Catalog",
    "itemType": "record",
    "title": "Sample metadata records from Dutch Nationaal georegister",
    "description": "Sample metadata records from Dutch Nationaal georegister",
    "keywords":[
        "netherlands",
        "open data",
        "georegister"
    ],
    "links":[
        {
            "type": "application/json",
            "rel": "self",
            "title": "This document as JSON",
            "href": "https://demo.pygeoapi.io/master/collections/dutch-metadata?f=json"
        },
        {
            "type": "application/geo+json",
            "rel": "items",
            "title": "items as GeoJSON",
            "href": "https://demo.pygeoapi.io/master/collections/dutch-metadata/items?f=json"
        }
    ]
}
```

### Records collection

Given OGC API - Records uses OGC API - Common and OGC API - Features as building blocks, please see the [OGC API - Features](features.md#feature-collection) deep dive
for a detailed initial explanation, as well as the [Records collections](#records-collections) description..

### Records access

Given OGC API - Records uses OGC API - Common and OGC API - Features as building blocks, please see the [OGC API - Features](features.md#features) deep dive
for a detailed explanation.

Below is an extract from the response to the request <https://demo.pygeoapi.io/master/collections/dutch-metadata/items?f=json>

```json
{
  "type": "FeatureCollection",
  "numberMatched": 308,
  "numberReturned": 10,
  "features": [
    {
      "id": "35149dfb-31d3-431c-a8bc-12a4034dac48",
      "type": "Feature",
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [
              4.690751953125,
              52.358740234375
            ],
            [
              4.690751953125,
              52.6333984375
            ],
            [
              5.020341796875,
              52.6333984375
            ],
            [
              5.020341796875,
              52.358740234375
            ],
            [
              4.690751953125,
              52.358740234375
            ]
          ]
        ]
      },
      "properties": {
        "created": "2021-12-08",
        "updated": "2022-06-10T01:27:47Z",
        "type": "dataset",
        "title": "Kaartboeck 1635",
        "description": "Data uit kaartboeken van de periode 1635 tot 1775. De kaartboeken werden door het waterschap gebruikt om er op toe te zien dat de eigenaren geen water in beslag namen door demping.\nDe percelen op de kaart zijn naar de huidige maatstaven vrij nauwkeurig gemeten en voorzien van een administratie met de eigenaren. bijzondere locaties van molens werven en beroepen worden in de boeken vermeld. Alle 97 kaarten aan een geven een zeer gedetailleerd beeld van de Voorzaan, Nieuwe Haven en de Achterzaan. De bladen Oost en West van de zaan zijn vrij nauwkeurig. De bladen aan de Voorzaan zijn een schetsmatige weergave van de situatie. De kaart van de Nieuwe Haven si weer nauwkeurig te noemen.",
        "providers": [
          "Team Geo, geo-informatie@zaanstad.nl, Gemeente Zaanstad"
        ],
        "externalIds": [
          {
            "scheme": "default",
            "value": "35149dfb-31d3-431c-a8bc-12a4034dac48"
          }
        ],
        "themes": [
          {
            "concepts": [
              "ARGEOLOGIE",
              "MONUMENTEN",
              "KADASTER",
              "KAARTBOEK",
              "KAARTBOECK",
              "HISTORIE"
            ]
          }
        ],
        "extent": {
          "spatial": {
            "bbox": [
              [
                4.690751953125,
                52.358740234375,
                5.020341796875,
                52.6333984375
              ]
            ],
            "crs": "http://www.opengis.net/def/crs/OGC/1.3/CRS84"
          },
          "temporal": {
            "interval": [
              null,
              null
            ],
            "trs": "http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"
          }
        }
      },
      "links": [
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wms?SERVICE=WMS",
          "rel": "item",
          "title": "geo:kaartboeck",
          "type": "OGC:WMS"
        },
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wfs?SERVICE=WFS",
          "rel": "item",
          "title": "geo:kaartboeck",
          "type": "OGC:WFS"
        },
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wfs?SERVICE=WFS&version=1.0.0&request=GetFeature&typeName=geo:kaartboeck&outputFormat=csv",
          "rel": "item",
          "type": "download"
        },
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wfs?SERVICE=WFS&version=1.0.0&request=GetFeature&typeName=geo:kaartboeck&outputFormat=shape-zip",
          "rel": "item",
          "type": "download"
        }
      ]
    }
```

Note that this document is a valid GeoJSON document.

OGC API - Records supports the same query parameters as specified in OGC API - Features.  In addition, OGC API - Records adds a set of core, fixed
queryables.  An example query based on a "search engine" style search using the **q** parameter is <https://demo.pygeoapi.io/master/collections/dutch-metadata/items?f=json&q=biomassa>

!!! note
    Consult the OGC API - Records - Part 1: Core specification for more information on core queryables.


### Record core

Given OGC API - Records uses OGC API - Common and OGC API - Features as building blocks, please see the [OGC API - Features](features.md#feature) deep dive
for a detailed explanation.

## Summary

OGC API - Records provides functionality for working with metadata data on the Web. This deep dive provided an overview of the standard and the various Resources and endpoints that are supported.
