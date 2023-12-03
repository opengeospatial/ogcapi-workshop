---
title: OGC API - Tiles
---

# OGC API - Tiles

!!! abstract Audience
    Students that are familiar with web services and APIs, and want to have
    an overview of OGC API - Tiles standard

!!! abstract "Learning Objectives"
    At the completion of the module students will be able to:

    -   Explain what the OGC API - Tiles standard is
    -   Describe what can be done with OGC API - Tiles implementations
    -   Understand the main resources offered by OGC API - Tiles implementations
    -   Understand how to retrieve a description of the capabilities of an OGC API - Tiles implementation
    -   Understand how to issue requests to an implementation of OGC API - Features
    -   Be able to find an OGC API - Tiles endpoint and use it through a client

## Introduction

The OGC API - Tiles standard defines building blocks for creating Web
APIs that support the retrieval of geospatial information as tiles.
Different forms of geospatial information are supported, such as tiles
of vector features ("vector tiles"), coverages, maps (or imagery) and
other types of geospatial information. Although it can be used
independently, the OGC API - Tiles building blocks can be combined
with other OGC API Standards and draft specifications for additional
capabilities or increasing interoperability for specific types of data.
The OGC API - Tiles standard references the [OGC Two Dimensional Tile
Matrix Set (TMS) and Tileset Metadata standard](https://docs.ogc.org/is/17-083r4/17-083r4.html), which defines logical
models and encodings for specifying tile matrix sets and describing tile
sets. 

!!! note
    This tutorial module is not intended to be a replacement to the actual
    **OGC API - Tiles - Part 1: Core** standard. The tutorial intentionally
    focuses on a subset of capabilities in order to get the student started
    with using the standard. Please refer to the **OGC API - Tiles - Part 1:
    Core** standard for additional detail.

The concepts of ```Tiling Scheme```, ```Tile Matrix``` and ```Tile Matrix Set``` are at the core of this standard:

- **Tiling Scheme:** schema used to partitioning the space into individual tiles, potentially featuring multiple levels of detail. A tiling scheme is usually defined on top of a CRS, althought it can use other spatial reference systems.
- **Tile Matrix:** set of tiles that implement a given tiling scheme, for a given scale.
  ![image](../assets/images/tm.png){width="80.0%"}
- **Tile Matrix Set:** set of tile matrices, used to represent the data at different scales. A Tile Matrix has a unique alphanumeric identifier in the Tile Matrix Set. Some tile-based implementations prefer to use the zoom level number. 
  ![image](../assets/images/tms.png){width="80.0%"}

!!! note

    - A tile matrix can be implemented as a set of image files (e.g., PNG or JPEG) in a file folder, each file representing a single tile.
    - In some standards the Tile Matrix Set concept is called an *image pyramid*. 
    
<iframe
  src="https://emotional.byteroad.net/collections/hex350_grid_cardio_1920/tiles"
  style="width:100%; height:800px;"
></iframe>


### Background

>  History

  The OGC API - Tiles standard is a successor to the OGC's Web Map
  Tile Service (WMTS) standard, focusing on simple reusable REST API
  building blocks which can be described using the OpenAPI
  specification. Whereas WMTS focused on map tiles, the OGC API -
  Tiles standard has been designed to support any form of tiled data.

> Versions

  **OGC API - Tiles - Part 1: Core** version 1.0.0 is the current latest version

> Test suite

  Test suites are available for:

  -   [OGC API - Tiles](https://github.com/opengeospatial/ets-ogcapi-tiles10)

> Implementations

  Implementations can be found on the [implementations page](https://github.com/opengeospatial/ogcapi-tiles/blob/master/implementations.adoc).

#### Usage

There are at least two ways to approach an implementation of the OGC
API - Tiles Standard.

-   Read the landing page, look for links, follow them and discover new
    links until the desired resource is found
-   Read a Web API definition document that specifies a list of paths
    and path templates to resources.

Once you have discovered the relevant resources, then retrieve the list
of available tiling schemes from the resource
```/tileMatrixSets``` to identify the tiling
scheme of interest. Retrieve the details of the specific tiling scheme
with ```/tileMatrixSets/{tileMatrixSetId}```.

Once you have identified a tiling scheme of interest, you can retrieve
tile set metadata for that tiling scheme through
```/tiles/{tileMatrixSetId}``` and also retrieve
individual tiles with
```/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}```

#### Relation to other OGC Standards

Although the OGC API - Tiles Standard is designed as a building block
that can be leveraged by (or with) other OGC API Standards adding
precisions about specific types of data available as tiles (e.g., OGC
API - Features standard, and OGC API - Maps and OGC API -
Coverages candidate standards), the conformance classes defined in this
Standard are still concrete enough to make it possible to support
distributing and requesting various types of tiled data, including
coverages, vector features and maps, by relying strictly on the content
herein and in the OGC Two Dimensional Tile Matrix Set and Tile Set
Metadata 2.0 standard.

### Overview of Resources

**OGC API - Tiles - Part 1: Core** defines the resources listed in the
following table.


<table>
  <tr>
    <th>Resource</th>
    <th>Method</th>
    <th>Path</th>
  </tr>
  <tr>
    <td>Landing page</td>
    <td>GET</td>
    <td>/</td>
  </tr>
  <tr>
    <td>Conformance declaration</td>
    <td>GET</td>
    <td>/conformance</td>
  <tr>
  </tr>
    <td>API definition</td>
    <td>GET</td>
    <td>/api</td>
  </tr>
  <tr>
    <td>Tiling Schemes</td>
    <td>GET</td>
    <td>/tileMatrixSets</td>
  </tr>
  <tr>
    <td>Tiling Scheme (tile matrix set)</td>
    <td>GET</td>
    <td>/tileMatrixSets/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Dataset tileset</td>
    <td>GET</td>
    <td>/tiles</td>
  </tr>
  <tr>
    <td>Dataset tileset metadata</td>
    <td>GET</td>
    <td>/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Dataset tileset metadata</td>
    <td>GET</td>
    <td>/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Dataset feature tile</td>
    <td>GET</td>
    <td>/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
  <tr>
    <td>Map tileset list</td>
    <td>GET</td>
    <td>/map/tiles</td>
  </tr>
  <tr>
    <td>Map tileset metadata</td>
    <td>GET</td>
    <td>/map/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Map tile</td>
    <td>GET</td>
    <td>/map/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
  <tr>
    <td>Collections</td>
    <td>GET</td>
    <td>/collections</td>
  </tr>
  <tr>
    <td>Collection</td>
    <td>GET</td>
    <td>/collections/{collectionId}</td>
  </tr>
  <tr>
    <td>Feature tileset list</td>
    <td>GET</td>
    <td>/collections/{collectionId}/tiles</td>
  </tr>
  <tr>
    <td>Feature tileset metadata</td>
    <td>GET</td>
    <td>/collections/{collectionId}/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Feature tileset list</td>
    <td>GET</td>
    <td>/collections/{collectionId}/tiles</td>
  </tr>
  <tr>
    <td>Feature tile</td>
    <td>GET</td>
    <td>/collections/{collectionId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>

  <tr>
    <td>Map tileset list</td>
    <td>GET</td>
    <td>/collections/{collectionId}/map/tiles</td>
  </tr>
  <tr>
    <td>Map tileset metadata</td>
    <td>GET</td>
    <td>/collections/{collectionId}/map/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Map tile</td>
    <td>GET</td>
    <td>/collections/{collectionId}/map/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
  <tr>
    <td>Coverage tileset list</td>
    <td>GET</td>
    <td>/collections/{collectionId}/coverage/tiles</td>
  </tr>
  <tr>
    <td>Coverage tileset metadata</td>
    <td>GET</td>
    <td>/collections/{collectionId}/coverage/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Coverage tile</td>
    <td>GET</td>
    <td>/collections/{collectionId}/coverage/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
</table>

### Example

This [demonstration server](https://demo.ldproxy.net/zoomstack/)
publishes tiled feature data through an interface that conforms to OGC
API - Tiles.

An example request that can be used to retrieve data, referenced to
WebMercatorQuad, from the OS Zoomstack collection is
<https://demo.ldproxy.net/zoomstack/tiles/WebMercatorQuad/0/0/0?f=mvt>

In this case the data is encoded in Mapbox Vector Tiles (MVT) format.

Once downloaded, a client application can then display or process the
data.

![image](../assets/images/mvt_example.png){width="40.0%"}

## Resources

### Landing page

Given OGC API - Tiles uses OGC API - Common as a building block, please see the [OGC API - Features](features.md#landing-page) deep dive
for a detailed explanation of an example implementation.

### Conformance declarations

Given OGC API - Tiles uses OGC API - Common as a building block, please see the [OGC API - Features](features.md#conformance-declarations) deep dive
for a detailed explanation of an example implementation.

### API Definition

Given OGC API - Tiles uses OGC API - Common as a building block, please see the [OGC API - Features](features.md#api-definition) deep dive
for a detailed explanation of an example implementation.

### Collections

Given OGC API - Maps uses OGC API - Common as a building block, please see the [OGC API - Features](features.md#collections) deep dive
for a detailed explanation of an example implementation.


## Summary
