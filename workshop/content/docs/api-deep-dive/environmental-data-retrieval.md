---
title: OGC API - Environmental Data Retrieval
---

# OGC API - Environmental Data Retrieval

!!! abstract Audience
    Students that are familiar with web services and APIs, and want to have
    an overview of OGC API - Environmental Data Retrieval standard

!!! abstract "Learning Objectives"
    At the completion of the module students will be able to:

    - Explain what the OGC API - Environmental Data Retrieval standard is
    - Describe what can be done with OGC API - Environmental Data Retrieval implementations
    - Understand the main resources offered by implementations of OGC API - Environmental Data Retrieval
    - Understand how to retrieve a description of the capabilities of an implementation of OGC API - Environmental Data Retrieval
    - Understand how to issue requests to an implementation of OGC API - Environmental Data Retrieval
    - Be able to find an OGC API - Environmental Data Retrieval endpoint and use it through a client

## Introduction

OGC API - Environmental Data Retrieval is a standard that provides a
family of lightweight interfaces to access Environmental Data resources.
The standard, which is also called the Environmental Data Retrieval
(EDR) API, addresses two fundamental operations; discovery and query.
Discovery operations allow the API to be interrogated to determine its
capabilities and retrieve information (metadata) about this distribution
of a resource. This includes the API definition of the server as well as
metadata about the Environmental Data resources provided by the server.
Query operations allow Environmental Data resources to be retrieved from
the underlying data store based upon simple selection criteria, defined
by this standard and selected by the client.

!!! note
    This tutorial module is not intended to be a replacement to the actual
    **OGC API - Environmental Data Retrieval** standard. The tutorial
    intentionally focuses on a subset of capabilities in order to get the
    student started with using the standard. Please refer to the [**OGC API -
    Environmental Data Retrieval** standard](https://docs.ogc.org/is/19-086r6/19-086r6.html) for additional detail.

### Background

> History

  Version 1.1.0 was published on 2023-07-27.

> Versions

  **OGC API - Environmental Data Retrieval** version 1.1.0 is the current latest version

> Test suite

  A draft executable test suite is available for:

  -   [OGC API - Environmental Data Retrieval](https://github.com/opengeospatial/ets-ogcapi-edr10)

> Implementations

Implementations can be found on the [implementations page](https://github.com/opengeospatial/ogcapi-environmental-data-retrieval/tree/master/implementations).

#### Usage

**OGC API - Environmental Data Retrieval** provides a family of
lightweight query interfaces to access spatio-temporal data resources by
requesting data at a position, within an area, along a trajectory or
through a corridor. A spatio-temporal data resource is a collection of
spatio-temporal data that can be sampled using the EDR query pattern
geometries.

The standard provides a standard interface for requesting vector
geospatial data consisting of geographic features and their properties.
The benefit of this is that client applications can request source data
from multiple implementations of the API, and then render the data for
display or process the data further as part of a workflow. The standard
enables the data to be accessed consistently with other data. Feature
properties encoded using common data types such as text strings, date
and time can also be accessed consistently.

#### Relation to other OGC Standards

-   OGC API - Features: The EDR API is completely compatible with OGC
    API - Features - Part 1: Core (OGC 17-069r3), in that it
    supports Collections and Items. It extends the Collection
    functionality by allowing 'Instances', a form of 'collection of
    collections'. The EDR API also supports the retrieval of
    spatiotemporal data by named location as well as coordinates.
-   Moving Features: The Moving Features Standards are concerned with
    things that move along a trajectory, and simultaneously change their
    orientation through rigid body rotation. The EDR API does not have
    the concept of orientation, or foliation or prisms. Moving Features
    and EDR API do share a common conceptual definition, from ISO, of a
    Trajectory, but the Moving Features Standards encode trajectories in
    GML, CSV and Moving Features JSON, whereas the EDR API encodes
    trajectories in WKT.
-   Web Coverage Service (WCS) and Coverage Implementation Schema (CIS):
    The primary messaging mechanism of the EDR API is JSON, including
    CoverageJSON, over HTTP(S). Implementations of the EDR API are
    described using the OpenAPI V3.0 specification. The EDR API is
    consistent with the WCS and CIS standards but does not require the
    end user or developer to use the terms Domain and RangeSet. The EDR
    API can also be used to generate a single query against a collection
    of coverages, providing the data coordinate reference systems are
    consistent.
-   The OGC SensorThings API: SensorThings API follows OData's
    specification for requesting entities. In contrast, the EDR API
    makes use of the OpenAPI V3.0 specification for describing resource
    paths, query options, JSON schema, and other aspects. Further, the
    EDR API allows for retrieval of coverage data and HTML responses --
    both of which are not supported by the SensorThings API.
-   Sensor Observation Service (SOS): The EDR API allows for retrieval
    of coverage data and HTML responses -- both of which are not
    supported by the SOS standard. Further, SOS implementations use the
    GetCapabilities operation for providing descriptions of available
    resources. In contrast, the EDR API uses OpenAPI definition
    documents for describing available interfaces.

### Overview of Resources

**OGC API - Environmental Data Retrieval Standard** defines the
resources listed in the following table.

<table>
<caption>Overview of OGC API - EDR resources</caption>
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
    <td>Collections metadata</td>
    <td>GET</td>
    <td>/collections</td>
    <td>Metadata describing the collections of data available from this API.</td>
  </tr>
  <tr>
    <td>Single Collection metadata</td>
    <td>GET</td>
    <td>/collections/{collectionId}</td>
    <td>Metadata describing the collection of data which has the unique identifier {collectionId}.</td>
  </tr>
  <tr>
    <td>Items metadata</td>
    <td>GET</td>
    <td>/collections/{collectionId}/items</td>
    <td>Retrieve metadata about available items.</td>
  </tr>
  <tr>
    <td>Query data</td>
    <td>GET</td>
    <td>/collections/{collectionId}/{queryType}</td>
    <td>Retrieve data according to the query pattern</td>
  </tr>
  <tr>
    <td>Query instances</td>
    <td>GET</td>
    <td>/collections/{collectionId}/instances</td>
    <td>Retrieve metadata about instances of a collection</td>
  </tr>
</table>

### Example

This [demonstration server](http://labs.metoffice.gov.uk/edr) publishes
environmental data through an interface that conforms to the OGC API -
Environmental Data Retrieval standard. A client application is available
[here](http://labs.metoffice.gov.uk/edr/static/html/query.html) .

An example request that can be used to retrieve data from the METAR
Observation collection is
[here](http://labs.metoffice.gov.uk/edr/collections/metar_demo/area?coords=POLYGON%20((-0.729139443718437%2050.6050890914524,-0.82028187418325%2052.0290614422956,1.84563421691251%2052.0991020742953,2.09627590069075%2050.8071099463535,-0.729139443718437%2050.6050890914524))&parameter-name=Metar%20observation&datetime=2021-10-03T20:00Z/2021-10-04T03:00Z&crs=CRS84&f=GeoJSON)
.

Note that the response to the request is GeoJSON in this case.

Alternatively, the same data can be retrieved in CoverageJSON format,
through [this
request](http://labs.metoffice.gov.uk/edr/collections/metar_demo/area?coords=POLYGON%20((-0.729139443718437%2050.6050890914524,-0.82028187418325%2052.0290614422956,1.84563421691251%2052.0991020742953,2.09627590069075%2050.8071099463535,-0.729139443718437%2050.6050890914524))&parameter-name=Metar%20observation&datetime=2021-10-03T20:00Z/2021-10-04T03:00Z&crs=CRS84&f=CoverageJSON)
.

Note that this demonstration server offers data from recent
observations, therefore you may need to update the values of the
```datetime``` parameter to the current day in order to access
available METAR observation.

## Resources

This section provides basic information about the types of resources
that OGC API - Environmental Data Retrieval offers.

Each resource provides **links** that relate to resources. This enables
a client application to navigate the resources, from the landing page
through to the individual features. The server identifies the
relationship between a resource and other linked resources through a
**link relation type**, represented by the attribute ```rel```. The link
relation types used by implementations of the **OGC API - Environmental
Data Retrieval** can be found in [Section
6.2](https://docs.ogc.org/is/19-086r4/19-086r4.html#toc22) of the
standard.

### Landing page

The landing page is the top-level resource that serves as an entry
point. A client application needs to know the location of the landing
page of the server. From the landing page, the client application can
retrieve links to the Conformance declaration, Collection and API
definition paths. An example landing page is at
<http://labs.metoffice.gov.uk/edr>

The link to the API definition is identified through the
```service-desc``` and ```service-doc``` link relation types.

The link to the Conformance declaration is identified through the
```conformance``` link relation type.

The link to the Collections is identified through the ```data``` link
relation type.

An extract from the landing page of a demo server is shown below.

```json
{
"title": "Environmental Data Retrevial API concept demonstrator",
"description": "Example EDR API (not for operational use)",
"keywords": [
  "position",
  "area",
  "cube",
  "trajectory",
  "weather",
  "data",
  "api"
],
"terms_of_service": "None",
"provider": {
  "name": "Organization Name",
  "url": "http://example.org"
},
"contact": {
  "email": "you@example.org",
  "phone": "+001-234-567-89",
  "fax": "+001-234-567-89",
  "hours": "Hours of Service",
  "instructions": "During hours of service.  Off on weekends.",
  "address": "Mailing Address",
  "postalcode": "Zip or Postal Code",
  "city": "City",
  "stateorprovince": "Administrative Area",
  "country": "Country"
},
"links": [
  {
    "href": "http://labs.metoffice.gov.uk/edr/api",
    "hreflang": "en",
    "rel": "service-doc",
    "type": "application/vnd.oai.openapi+json;version=3.0",
    "title": "",
    "variables": null
  },
  {
    "href": "http://labs.metoffice.gov.uk/edr/conformance",
    "hreflang": "en",
    "rel": "conformance",
    "type": "application/json",
    "title": "",
    "variables": null
  },
  {
    "href": "http://labs.metoffice.gov.uk/edr/collections",
    "hreflang": "en",
    "rel": "collection",
    "type": "application/json",
    "title": "",
    "variables": null
  }
]
}
```

### Conformance declaration

An implementation of OGC API - Environmental Data Retrieval describes
the capabilities that it supports by declaring which conformance classes
it implements. The Conformance declaration states the conformance
classes from standards or community specifications, identified by a URI,
that the API conforms to. Clients can then use this information,
although they are not required to. Accessing the Conformance declaration
using HTTP GET returns the list of URIs of conformance classes
implemented by the server. Conformance classes describe the behavior a
server should implement in order to meet one or more sets of
requirements specified in a standard.

Below is an extract from the response to the request
<http://labs.metoffice.gov.uk/edr/conformance>

```json
{
 "conformsTo":[
    "http://www.opengis.net/spec/ogcapi-common-1/1.0/conf/core",
    "http://www.opengis.net/spec/ogcapi-common-2/1.0/conf/collections",
    "http://www.opengis.net/spec/ogcapi-edr-1/1.0/conf/core",
    "http://www.opengis.net/spec/ogcapi-edr-1/1.0/conf/oas30",
    "http://www.opengis.net/spec/ogcapi-edr-1/1.0/conf/html",
    "http://www.opengis.net/spec/ogcapi-edr-1/1.0/conf/geojson",
    "http://www.opengis.net/spec/ogcapi-edr-1/1.0/conf/coveragejson",
    "http://www.opengis.net/spec/ogcapi-edr-1/1.0/conf/wkt"
 ]
 }
```

### API Definition

Given OGC API - Environmental Data Retrieval uses OGC API - Common as a building block, please see the [OGC API - Features](features.md#api-definition) deep dive
for a detailed explanation of an example implementation.

### Collections metadata

Data offered through an implementation of **OGC API - Environmental Data
Retrevial** is organized into one or more feature collections. The
```Collections``` resource provides information about and access to the
list of collections.

For each collection, there is a link to the detailed description of the
collection (represented by the path **/collections/{collectionId}** and
link relation **self**).

The following information is provided by the server to describe each
collection:

-   A local identifier for the collection that is unique for the dataset
-   A list of coordinate reference systems (CRS) in which geometries may
    be returned by the server
-   An optional title and description for the collection
-   An optional extent that can be used to provide an indication of the
    spatial and temporal extent of the collection
-   An optional indicator about the type of the items in the collection
    (the default value, if the indicator is not provided, is
    ```feature```).

For each collection, there are links to retrieve data according to
supported query patterns (represented by the path
**/collections/{collectionId}/{queryType}** and link relation **data**).

For each collection, there is a link to the metadata about items
available in the collection (represented by the path
**/collections/{collectionId}/items** and link relation **items**) and
other information about the collection.

Below is an extract from the response to the request
<http://labs.metoffice.gov.uk/edr/collections>

```json
{
  "links": [
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections",
      "hreflang": "en",
      "rel": "self",
      "type": "application/json"
    },
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections?f=html",
      "hreflang": "en",
      "rel": "alternate",
      "type": "text/html"
    },
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections?f=xml",
      "hreflang": "en",
      "rel": "alternate",
      "type": "application/xml"
    }
  ],
  "collections": [
    {
      "id": "metar_demo",
      "title": "Metar observations EDR demonstrator",
      "description": "API to access 24 hours of Global Metar Observation data (not for operational use)",
      "keywords": [
        "Metar observation",
        "ICAO identifier",
        "Wind Direction",
        "Wind Speed",
        "Wind Gust",
        "Visibility",
        "Air Temperature",
        "Dew point",
        "Runway Visibility",
        "Weather",
        "Sky condition",
        "Mean Sea Level Pressure",
        "Station Level Pressure",
        "description",
        "restrictions",
        "collection",
        "position",
        "radius",
        "area",
        "location"
      ],
      "links": [
        {
          "href": "https://www.aviationweather.gov/metar/help",
          "hreflang": "en",
          "rel": "service-doc",
          "type": "text/html",
          "title": ""
        },
        {
          "href": "https://www.weather.gov/disclaimer",
          "hreflang": "en",
          "rel": "restrictions",
          "type": "text/html",
          "title": ""
        },
        {
          "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/",
          "hreflang": "en",
          "rel": "collection",
          "type": "collection",
          "title": ""
        },
        {
          "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/position",
          "hreflang": "en",
          "rel": "data"
        },
        {
          "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/radius",
          "hreflang": "en",
          "rel": "data"
        },
        {
          "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/area",
          "hreflang": "en",
          "rel": "data"
        },
        {
          "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/locations",
          "hreflang": "en",
          "rel": "data"
        }
      ],
      "extent": {
        "spatial": {
          "bbox": [
            -180.0,
            -89.9,
            180.0,
            89.9
          ],
          "crs": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
        },
        "temporal": {
          "interval": [
            "R36/2021-10-03T01:00Z/PT1H"
          ],
          "trs": "TIMECRS[\"DateTime\",TDATUM[\"Gregorian Calendar\"],CS[TemporalDateTime,1],AXIS[\"Time (T)\",future]"
        }
      },
      "data_queries": {
        "position": {
          "link": {
            "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/position",
            "hreflang": "en",
            "rel": "data",
            "variables": {
              "title": "Position query",
              "query_type": "position",
              "output_formats": [
                "CoverageJSON",
                "GeoJSON",
                "IWXXM"
              ],
              "default_output_format": "GeoJSON",
              "crs_details": [
                {
                  "crs": "CRS84",
                  "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
                }
              ]
            }
          }
        },
        "radius": {
          "link": {
            "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/radius",
            "hreflang": "en",
            "rel": "data",
            "variables": {
              "title": "Radius query",
              "description": "Radius query",
              "query_type": "radius",
              "output_formats": [
                "CoverageJSON",
                "GeoJSON",
                "IWXXM"
              ],
              "default_output_format": "GeoJSON",
              "within_units": [
                "km",
                "miles"
              ],
              "crs_details": [
                {
                  "crs": "CRS84",
                  "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
                }
              ]
            }
          }
        },
        "area": {
          "link": {
            "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/area",
            "hreflang": "en",
            "rel": "data",
            "variables": {
              "title": "Area query",
              "query_type": "area",
              "output_formats": [
                "CoverageJSON",
                "GeoJSON",
                "IWXXM"
              ],
              "default_output_format": "CoverageJSON",
              "crs_details": [
                {
                  "crs": "CRS84",
                  "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
                }
              ]
            }
          }
        },
        "locations": {
          "link": {
            "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/locations",
            "hreflang": "en",
            "rel": "data",
            "variables": {
              "title": "Location query",
              "description": "Location query",
              "query_type": "locations",
              "output_formats": [
                "CoverageJSON",
                "GeoJSON",
                "CSV"
              ],
              "default_output_format": "GeoJSON",
              "crs_details": [
                {
                  "crs": "CRS84",
                  "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
                }
              ]
            }
          }
        }
      },
      "crs": [
        "CRS84"
      ],
      "output_formats": [
        "CoverageJSON",
        "GeoJSON",
        "IWXXM"
      ],
      "parameter_names": {
        "Metar observation": {
          "type": "Parameter",
          "description": "Source Metar observation",
          "unit": {
            "label": "",
            "symbol": {
              "value": "",
              "type": "http://codes.wmo.int/wmdr/DataFormat/FM-15-metar"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/wmdr/DataFormat/FM-15-metar",
            "label": "Metar observation"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "ICAO identifier": {
          "type": "Parameter",
          "description": "ICAO identifier",
          "unit": {
            "label": "",
            "symbol": {
              "value": "",
              "type": "https://en.wikipedia.org/wiki/ICAO_airport_code"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/bufr4/b/01/_063",
            "label": "ICAO identifier"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Wind Direction": {
          "type": "Parameter",
          "description": "Wind Direction",
          "unit": {
            "label": "degree true",
            "symbol": {
              "value": "\u00b0",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/degree"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/common/quantity-kind/_aerodromeMeanWindDirection",
            "label": "Wind Direction"
          },
          "measurementType": {
            "method": "mean",
            "period": "-PT10M/PT0M"
          }
        },
        "Wind Speed": {
          "type": "Parameter",
          "description": "Wind Speed",
          "unit": {
            "label": "mph",
            "symbol": {
              "value": "mph",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/mph"
            }
          },
          "observedProperty": {
            "id": " http://codes.wmo.int/common/quantity-kind/aerodromeMeanWindSpeed",
            "label": "Wind Speed"
          },
          "measurementType": {
            "method": "mean",
            "period": "-PT10M/PT0M"
          }
        },
        "Wind Gust": {
          "type": "Parameter",
          "description": "Wind Gust",
          "unit": {
            "label": "mph",
            "symbol": {
              "value": "mph",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/mph"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/common/quantity-kind/_aerodromeMaximumWindGustSpeed",
            "label": "Wind Gust"
          },
          "measurementType": {
            "method": "maximum",
            "period": "-PT10M/PT0M"
          }
        },
        "Visibility": {
          "type": "Parameter",
          "description": "Visibility",
          "unit": {
            "label": "m",
            "symbol": {
              "value": "m",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/m"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/common/quantity-kind/_horizontalVisibility",
            "label": "Visibility"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Air Temperature": {
          "type": "Parameter",
          "description": "",
          "unit": {
            "label": "degC",
            "symbol": {
              "value": "\u00b0C",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/degC"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/common/quantity-kind/_airTemperature",
            "label": "Air Temperature"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Dew point": {
          "type": "Parameter",
          "description": "",
          "unit": {
            "label": "degC",
            "symbol": {
              "value": "\u00b0C",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/degC"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/common/quantity-kind/_dewPointTemperature",
            "label": "Dew point"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Runway Visibility": {
          "type": "Parameter",
          "description": "Runway Visibile Range",
          "unit": {
            "label": "m",
            "symbol": {
              "value": "m",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/m"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/common/quantity-kind/_runwayVisualRangeRvr",
            "label": "Runway Visibility"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Weather": {
          "type": "Parameter",
          "description": "Aerodrome recent weather",
          "unit": {
            "label": "weather",
            "symbol": {
              "value": "",
              "type": "http://codes.wmo.int/49-2/AerodromeRecentWeather"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/49-2/AerodromeRecentWeather",
            "label": "Weather"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Sky condition": {
          "type": "Parameter",
          "description": "Sky condition",
          "unit": {
            "label": "sky",
            "symbol": {
              "value": "",
              "type": "http://{server}"
            }
          },
          "observedProperty": {
            "id": "",
            "label": "Sky condition"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Mean Sea Level Pressure": {
          "type": "Parameter",
          "description": "",
          "unit": {
            "label": "hPa",
            "symbol": {
              "value": "hPa",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/hPa"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/bufr4/b/10/_051",
            "label": "Mean Sea Level Pressure"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        },
        "Station Level Pressure": {
          "type": "Parameter",
          "description": "",
          "unit": {
            "label": "hPa",
            "symbol": {
              "value": "hPa",
              "type": "http://labs.metoffice.gov.uk/edr/metadata/units/hPa"
            }
          },
          "observedProperty": {
            "id": "http://codes.wmo.int/bufr4/b/10/_004",
            "label": "Station Level Pressure"
          },
          "measurementType": {
            "method": "instantaneous",
            "period": "PT0M"
          }
        }
      }
    }
  ]
}
```

The **Collection** resource provides detailed information about the
collection identified in a request. Some of the information returned
includes the supported geographic extent, data queries, coordinate
reference systems, output formats, and parameter names.

Below is an extract from the response to the request
<http://labs.metoffice.gov.uk/edr/collections/metar_demo?f=json>

```json
{
  "id": "metar_demo",
  "title": "Metar observations EDR demonstrator",
  "description": "API to access 24 hours of Global Metar Observation data (not for operational use)",
  "keywords": [
    "Metar observation",
    "ICAO identifier",
    "Wind Direction",
    "Wind Speed",
    "Wind Gust",
    "Visibility",
    "Air Temperature",
    "Dew point",
    "Runway Visibility",
    "Weather",
    "Sky condition",
    "Mean Sea Level Pressure",
    "Station Level Pressure",
    "description",
    "restrictions",
    "collection",
    "position",
    "radius",
    "area",
    "location"
  ],
  "links": [
    {
      "href": "http://labs.metoffice.gov.uk/collections/metar_demo",
      "hreflang": "en",
      "rel": "self",
      "type": "application/json"
    },
    {
      "href": "http://labs.metoffice.gov.uk/collections/metar_demo?f=html",
      "hreflang": "en",
      "rel": "alternate",
      "type": "text/html"
    },
    {
      "href": "http://labs.metoffice.gov.uk/collections/metar_demo?f=xml",
      "hreflang": "en",
      "rel": "alternate",
      "type": "application/xml"
    },
    {
      "href": "https://www.aviationweather.gov/metar/help",
      "hreflang": "en",
      "rel": "service-doc",
      "type": "text/html",
      "title": ""
    },
    {
      "href": "https://www.weather.gov/disclaimer",
      "hreflang": "en",
      "rel": "restrictions",
      "type": "text/html",
      "title": ""
    },
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/position",
      "hreflang": "en",
      "rel": "data"
    },
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/radius",
      "hreflang": "en",
      "rel": "data"
    },
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/area",
      "hreflang": "en",
      "rel": "data"
    },
    {
      "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/locations",
      "hreflang": "en",
      "rel": "data"
    }
  ],
  "extent": {
    "spatial": {
      "bbox": [
        -180.0,
        -89.9,
        180.0,
        89.9
      ],
      "crs": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
    },
    "temporal": {
      "interval": [
        "R36/2021-10-03T03:00Z/PT1H"
      ],
      "trs": "TIMECRS[\"DateTime\",TDATUM[\"Gregorian Calendar\"],CS[TemporalDateTime,1],AXIS[\"Time (T)\",future]"
    }
  },
  "data_queries": {
    "position": {
      "link": {
        "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/position",
        "hreflang": "en",
        "rel": "data",
        "variables": {
          "title": "Position query",
          "query_type": "position",
          "output_formats": [
            "CoverageJSON",
            "GeoJSON",
            "IWXXM"
          ],
          "default_output_format": "GeoJSON",
          "crs_details": [
            {
              "crs": "CRS84",
              "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
            }
          ]
        }
      }
    },
    "radius": {
      "link": {
        "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/radius",
        "hreflang": "en",
        "rel": "data",
        "variables": {
          "title": "Radius query",
          "description": "Radius query",
          "query_type": "radius",
          "output_formats": [
            "CoverageJSON",
            "GeoJSON",
            "IWXXM"
          ],
          "default_output_format": "GeoJSON",
          "within_units": [
            "km",
            "miles"
          ],
          "crs_details": [
            {
              "crs": "CRS84",
              "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
            }
          ]
        }
      }
    },
    "area": {
      "link": {
        "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/area",
        "hreflang": "en",
        "rel": "data",
        "variables": {
          "title": "Area query",
          "query_type": "area",
          "output_formats": [
            "CoverageJSON",
            "GeoJSON",
            "IWXXM"
          ],
          "default_output_format": "CoverageJSON",
          "crs_details": [
            {
              "crs": "CRS84",
              "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
            }
          ]
        }
      }
    },
    "locations": {
      "link": {
        "href": "http://labs.metoffice.gov.uk/edr/collections/metar_demo/locations",
        "hreflang": "en",
        "rel": "data",
        "variables": {
          "title": "Location query",
          "description": "Location query",
          "query_type": "locations",
          "output_formats": [
            "CoverageJSON",
            "GeoJSON",
            "CSV"
          ],
          "default_output_format": "GeoJSON",
          "crs_details": [
            {
              "crs": "CRS84",
              "wkt": "GEOGCS[\"WGS 84\",DATUM[\"WGS_1984\",SPHEROID[\"WGS 84\",6378137,298.257223563,AUTHORITY[\"EPSG\",\"7030\"]],AUTHORITY[\"EPSG\",\"6326\"]],PRIMEM[\"Greenwich\",0,AUTHORITY[\"EPSG\",\"8901\"]],UNIT[\"degree\",0.01745329251994328,AUTHORITY[\"EPSG\",\"9122\"]],AUTHORITY[\"EPSG\",\"4326\"]]"
            }
          ]
        }
      }
    }
  },
  "crs": [
    "CRS84"
  ],
  "output_formats": [
    "CoverageJSON",
    "GeoJSON",
    "IWXXM"
  ],
  "parameter_names": {
    "Metar observation": {
      "type": "Parameter",
      "description": "Source Metar observation",
      "unit": {
        "label": "",
        "symbol": {
          "value": "",
          "type": "http://codes.wmo.int/wmdr/DataFormat/FM-15-metar"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/wmdr/DataFormat/FM-15-metar",
        "label": "Metar observation"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "ICAO identifier": {
      "type": "Parameter",
      "description": "ICAO identifier",
      "unit": {
        "label": "",
        "symbol": {
          "value": "",
          "type": "https://en.wikipedia.org/wiki/ICAO_airport_code"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/bufr4/b/01/_063",
        "label": "ICAO identifier"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Wind Direction": {
      "type": "Parameter",
      "description": "Wind Direction",
      "unit": {
        "label": "degree true",
        "symbol": {
          "value": "\u00b0",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/degree"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/common/quantity-kind/_aerodromeMeanWindDirection",
        "label": "Wind Direction"
      },
      "measurementType": {
        "method": "mean",
        "period": "-PT10M/PT0M"
      }
    },
    "Wind Speed": {
      "type": "Parameter",
      "description": "Wind Speed",
      "unit": {
        "label": "mph",
        "symbol": {
          "value": "mph",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/mph"
        }
      },
      "observedProperty": {
        "id": " http://codes.wmo.int/common/quantity-kind/aerodromeMeanWindSpeed",
        "label": "Wind Speed"
      },
      "measurementType": {
        "method": "mean",
        "period": "-PT10M/PT0M"
      }
    },
    "Wind Gust": {
      "type": "Parameter",
      "description": "Wind Gust",
      "unit": {
        "label": "mph",
        "symbol": {
          "value": "mph",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/mph"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/common/quantity-kind/_aerodromeMaximumWindGustSpeed",
        "label": "Wind Gust"
      },
      "measurementType": {
        "method": "maximum",
        "period": "-PT10M/PT0M"
      }
    },
    "Visibility": {
      "type": "Parameter",
      "description": "Visibility",
      "unit": {
        "label": "m",
        "symbol": {
          "value": "m",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/m"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/common/quantity-kind/_horizontalVisibility",
        "label": "Visibility"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Air Temperature": {
      "type": "Parameter",
      "description": "",
      "unit": {
        "label": "degC",
        "symbol": {
          "value": "\u00b0C",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/degC"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/common/quantity-kind/_airTemperature",
        "label": "Air Temperature"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Dew point": {
      "type": "Parameter",
      "description": "",
      "unit": {
        "label": "degC",
        "symbol": {
          "value": "\u00b0C",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/degC"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/common/quantity-kind/_dewPointTemperature",
        "label": "Dew point"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Runway Visibility": {
      "type": "Parameter",
      "description": "Runway Visibile Range",
      "unit": {
        "label": "m",
        "symbol": {
          "value": "m",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/m"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/common/quantity-kind/_runwayVisualRangeRvr",
        "label": "Runway Visibility"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Weather": {
      "type": "Parameter",
      "description": "Aerodrome recent weather",
      "unit": {
        "label": "weather",
        "symbol": {
          "value": "",
          "type": "http://codes.wmo.int/49-2/AerodromeRecentWeather"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/49-2/AerodromeRecentWeather",
        "label": "Weather"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Sky condition": {
      "type": "Parameter",
      "description": "Sky condition",
      "unit": {
        "label": "sky",
        "symbol": {
          "value": "",
          "type": "http://{server}"
        }
      },
      "observedProperty": {
        "id": "",
        "label": "Sky condition"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Mean Sea Level Pressure": {
      "type": "Parameter",
      "description": "",
      "unit": {
        "label": "hPa",
        "symbol": {
          "value": "hPa",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/hPa"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/bufr4/b/10/_051",
        "label": "Mean Sea Level Pressure"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    },
    "Station Level Pressure": {
      "type": "Parameter",
      "description": "",
      "unit": {
        "label": "hPa",
        "symbol": {
          "value": "hPa",
          "type": "http://labs.metoffice.gov.uk/edr/metadata/units/hPa"
        }
      },
      "observedProperty": {
        "id": "http://codes.wmo.int/bufr4/b/10/_004",
        "label": "Station Level Pressure"
      },
      "measurementType": {
        "method": "instantaneous",
        "period": "PT0M"
      }
    }
  }
}
```

### Query Resources

Query resources are spatio-temporal queries which support operation of
the API for the access and use of the spatio-temporal data resources.

Query resources share several common parameters, which makes it easier
for developers to implement the queries.

Where the query applies to a collection, the pattern is as follows:

```/collections/{collectionId}/{queryType}```

The parameter ```queryType``` can be one of the following:

-   position
-   area
-   cube
-   trajectory
-   corridor
-   radius
-   instances
-   locations
-   items

Where the query applies to an instance, the pattern is as follows:

```/collections/{collectionId}/instances/{instanceId}/{queryType}```


#### Area Query Resources of OGC API - EDR

An area is a region specified with a geographic envelope that may have
vertical dimension. An illustration, created using NASA WorldWind, is
shown below.

![image](../assets/images/environmental-data-retrieval-query-area.png){width="80.0%"}

The ```area``` query resource returns data for the defined area.
The resource offers a convenience mechanism for querying the API by
area, using a Well Known Text (WKT) POLYGON geometry.

The path to the resource is shown below:

```/collections/{collectionId}/area```

The paths accepts the following parameters:

-   coords
-   z
-   parameter-name
-   datetime
-   crs
-   f

An example request is shown below.

```http://example.org/edr/collections/gfs-pressure_at_height/area?coords=POLYGON((-0.898132%2051.179362,-0.909119%2051.815488,0.552063%2051.818884,0.560303%2051.191414,-0.898132%2051.179362))&parameter-name=Pressure_height_above_ground&datetime=2022-01-19T06:00Z/2022-01-19T12:00Z&z=80/80&crs=CRS84&f=CoverageJSON```

#### Corridor Query Resources of OGC API - EDR

A corridor is a two parameter set of points around a trajectory. An
illustration, created using NASA WorldWind, is shown below.

![image](../assets/images/environmental-data-retrieval-query-corridor.png){width="80.0%"}

The ```corridor``` query resource returns data for the defined
corridor. The resource offers a convenience mechanism for querying the
API by corridor, using a Well Known Text (WKT) LINESTRING geometry, or
alternatively subclasses LINESTRINGZ, LINESTRINGM, LINESTRINGZM.

The path to the resource is shown below:

```/collections/{collectionId}/corridor```

The paths accepts the following parameters:

-   coords
-   corridor-width
-   corridor-height
-   width-units
-   height-units
-   z
-   parameter-name
-   datetime
-   crs
-   f
  
#### Cube Query Resources of OGC API - EDR

A cube is a rectangular area, with a vertical extent. An illustration,
created using NASA WorldWind, is shown below.

![image](../assets/images/environmental-data-retrieval-query-cube.png){width="80.0%"}

The ```cube``` query resource returns data for a defined cube.
The resource offers a convenience mechanism for querying the API using a
bounding box (BBOX) defining a cube.

The path to the resource is shown below:

```/collections/{collectionId}/cube```

The paths accepts the following parameters:

-   bbox
-   z
-   parameter-name
-   datetime
-   crs
-   f

#### Instances Query Resources of OGC API - EDR

The ```instances``` query resource retrieves metadata about
instances of a collection. The resource enables support for multiple
instances or versions of the same underlying data source to be accessed
by the API.

The path to the resource is shown below:

```/collections/{collectionID}/instances/{instanceID}/{queryType}```

#### Items (Features) Query Resources of OGC API - EDR

The ```items``` query resource offers an OGC API - Features
endpoint that may be used to catalog pre-existing EDR sampling features.

Example use cases of this resource include:

-   existence of a monitoring location
-   cached query
-   cataloguing of anomalies in a data

The path to the resource is shown below:

```/collections/{collectionId}/items```

An example request is below.

```http://example.org/edr/collections/mocov-daily_global/items```

#### Locations Query Resources of OGC API - EDR

The ```locations``` query resource returns a list of location
identifiers and relevant metadata for the collection.

The location identifier can be anything as long as it is unique for the
required position (e.g. a GeoHash).

The path to the resource is shown below:

```/collections/{collectionId}/locations```

An example request is below.

```http://example.org/edr/collections/obs_demo/locations```

#### Position Query Resources of OGC API - EDR

A position is a data type that describes a point or geometry potentially
occupied by an object or person. An illustration, created using NASA
WorldWind, is shown below.

![image](../assets/images/environmental-data-retrieval-query-position.png){width="80.0%"}

The ```position``` query resource returns data for the requested
position. The resource offers a convenience mechanism for querying the
API using a Well Known Text (WKT) POINT geometry defining a position.

The path to the resource is shown below:

```/collections/{collectionId}/position```

The paths accepts the following parameters:

-   coords
-   z
-   parameter-name
-   datetime
-   crs
-   f

An example request is shown below.

```http://example.org/edr/collections/obs_demo/position?coords=POINT(0.00577%2051.562608)&parameter-name=Wind%20Direction&datetime=2022-01-19T10:00Z/2022-01-19T12:00Z&crs=CRS84&f=GeoJSON```

#### Radius Query Resources of OGC API - EDR

A radius is a region specified with a geographic position and radial
distance. An illustration, created using NASA WorldWind, is shown below.

![image](../assets/images/environmental-data-retrieval-query-radius.png){width="80.0%"}

The ```radius``` query resource returns data for a defined
radius. The resource offers a convenience mechanism for querying the API
by radius.

The path to the resource is shown below:

```/collections/{collectionId}/radius```

The paths accepts the following parameters:

-   coords
-   within
-   width-units
-   z
-   parameter-name
-   datetime
-   crs
-   f

An example request is shown below.

```http://example.org/edr/collections/obs_demo/radius?coords=POINT(-0.095882%2051.512983)&within=50&within-units=km&parameter-name=Wind%20Direction&datetime=2022-01-19T04:00Z/2022-01-19T06:00Z&crs=CRS84&f=GeoJSON```

#### Trajectory Query Resources of OGC API - EDR

A trajectory is a path of a moving point described by a one parameter
set of points. An illustration, created using NASA WorldWind, is shown
below.

![image](../assets/images/environmental-data-retrieval-query-trajectory.png){width="80.0%"}

The ```trajectory``` query resource returns data for the defined
trajectory. The resource offers a convenience mechanism for querying the
API by trajectory, using a Well Known Text (WKT) LINESTRING geometry, or
alternatively the specializations LINESTRINGZ, LINESTRINGM,
LINESTRINGZM.

The path to the resource is shown below:

```/collections/{collectionId}/trajectory```

The paths accepts the following parameters:

-   coords
-   z
-   parameter-name
-   datetime
-   crs
-   f

An example request is shown below.

```http://example.org/edr/collections/gfs-pressure_at_height/trajectory?coords=LINESTRING(-3.56
53.695,-3.546 53.696,-3.532
53.697)&parameter-name=Height&crs=CRS84&f=CoverageJSON```

## Summary

 OGC API - Environmental Data Retrieval provides a family of lightweight interfaces to access Environmental Data resources. Each resource addressed by an EDR API maps to a defined query pattern. In this deep dive, we provided an overview of the standard and described each of these query patterns in detail.
