---
title: OGC API - Tiles
---

# OGC API - Tiles

!!! abstract Audience
    Students that are familiar with web services and APIs, and want to have
    an overview of OGC API - Tiles standard.

!!! abstract "Learning Objectives"
    At the completion of the module students will be able to:

    -   Explain what the OGC API - Tiles standard is
    -   Describe what can be done with OGC API - Tiles implementations
    -   Understand the main resources offered by OGC API - Tiles implementations
    -   Understand how to retrieve a description of the capabilities of an OGC API - Tiles implementation
    -   Understand how to issue requests to an implementation of OGC API - Features
    -   Be able to find an OGC API - Tiles endpoint and use it through a client

# An Introduction to OGC API - Tiles

## Introduction

The OGC API --- Tiles standard defines building blocks for creating Web
APIs that support the retrieval of geospatial information as tiles.
Different forms of geospatial information are supported, such as tiles
of vector features ("vector tiles"), coverages, maps (or imagery) and
other types of geospatial information. Although it can be used
independently, the OGC API --- Tiles building blocks can be combined
with other OGC API Standards and draft specifications for additional
capabilities or increasing interoperability for specific types of data.
The OGC API --- Tiles standard references the OGC Two Dimensional Tile
Matrix Set (TMS) and Tileset Metadata standard, which defines logical
models and encodings for specifying tile matrix sets and describing tile
sets. A tile matrix set is a tiling scheme that enables an application
to partition and index space based on a set of regular grids defined for
multiple scales in a Coordinate Reference System (CRS).

!!! note
    This tutorial module is not intended to be a replacement to the actual
    **OGC API - Tiles - Part 1: Core** standard. The tutorial intentionally
    focuses on a subset of capabilities in order to get the student started
    with using the standard. Please refer to the **OGC API - Tiles - Part 1:
    Core** standard for additional detail.


## Background

>  History

  The OGC API - Tiles standard is a successor to the OGC's Web Map
  Tile Service (WMTS) standard, focusing on simple reusable REST API
  building blocks which can be described using the OpenAPI
  specification. Whereas WMTS focused on map tiles, the OGC API -
  Tiles standard has been designed to support any form of tiled data.

>  Versions

  **OGC API - Tiles - Part 1: Core** version 1.0.0 is the current latest version

>  Test Suite

  Test suites are available for:

  -   [OGC API - Tiles](https://github.com/opengeospatial/ets-ogcapi-tiles10)

>  Implementations

  Implementations can be found on the Compliance Database here <http://www.opengeospatial.org/resource/products/byspec>

### Usage

There are at least two ways to approach an implementation of the OGC
API - Tiles Standard.

-   Read the landing page, look for links, follow them and discover new
    links until the desired resource is found
-   Read a Web API definition document that specifies a list of paths
    and path templates to resources.

Once you have discovered the relevant resources, then retrieve the list
of available tiling schemes from the resource
```.../{datasetRoot}/tileMatrixSets]``` to identify the tiling
scheme of interest. Retrieve the details of the specific tiling scheme
with ```.../{datasetRoot}/tileMatrixSets/{tileMatrixSetId}```.

Once you have identified a tiling scheme of interest, you can retrieve
tile set metadata for that tiling scheme through
```[{datasetRoot}/tiles/{tileMatrixSetId}]``` and also retrieve
individual tiles with
```[{datasetRoot}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}```

### Relation to other OGC Standards

Although the OGC API --- Tiles Standard is designed as a building block
that can be leveraged by (or with) other OGC API Standards adding
precisions about specific types of data available as tiles (e.g., OGC
API --- Features standard, and OGC API --- Maps and OGC API ---
Coverages candidate standards), the conformance classes defined in this
Standard are still concrete enough to make it possible to support
distributing and requesting various types of tiled data, including
coverages, vector features and maps, by relying strictly on the content
herein and in the OGC Two Dimensional Tile Matrix Set and Tile Set
Metadata 2.0 standard.

# Overview of Resources

**OGC API - Tiles - Part 1: Core** defines the resources listed in the
following table.


<table>
  <tr>
    <th>Resource</th>
    <th>Path</th>
  </tr>
  <tr>
    <td>Landing page</td>
    <td>/</td>
  </tr>
  <tr>
    <td>Conformance declaration</td>
    <td>/conformance</td>
  <tr>
  </tr>
    <td>API definition</td>
    <td>/api</td>
  </tr>
  <tr>
    <td>Tiling Schemes</td>
    <td>/tileMatrixSets</td>
  </tr>
  <tr>
    <td>Tiling Scheme (tile matrix set)</td>
    <td>/tileMatrixSets/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Dataset tileset</td>
    <td>/tiles</td>
  </tr>
  <tr>
    <td>Dataset tileset metadata</td>
    <td>/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Dataset tileset metadata</td>
    <td>/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Dataset feature tile</td>
    <td>/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
  <tr>
    <td>Map tileset list</td>
    <td>/map/tiles</td>
  </tr>
  <tr>
    <td>Map tileset metadata</td>
    <td>/map/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Map tile</td>
    <td>/map/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
  <tr>
    <td>Collections</td>
    <td>/collections </td>
  </tr>
  <tr>
    <td>Collection</td>
    <td>/collections/{collectionId}</td>
  </tr>
  <tr>
    <td>Feature tileset list</td>
    <td>/collections/{collectionId}/tiles</td>
  </tr>
  <tr>
    <td>Feature tileset metadata</td>
    <td>/collections/{collectionId}/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Feature tileset list</td>
    <td>/collections/{collectionId}/tiles</td>
  </tr>
  <tr>
    <td>Feature tile</td>
    <td>/collections/{collectionId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>

  <tr>
    <td>Map tileset list</td>
    <td>/collections/{collectionId}/map/tiles</td>
  </tr>
  <tr>
    <td>Map tileset metadata</td>
    <td>/collections/{collectionId}/map/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Map tile</td>
    <td>/collections/{collectionId}/map/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
  <tr>
    <td>Coverage tileset list</td>
    <td>/collections/{collectionId}/coverage/tiles</td>
  </tr>
  <tr>
    <td>Coverage tileset metadata</td>
    <td>/collections/{collectionId}/coverage/tiles/{tileMatrixSetId}</td>
  </tr>
  <tr>
    <td>Coverage tile</td>
    <td>/collections/{collectionId}/coverage/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}</td>
  </tr>
</table>

# Example

This [demonstration server](https://demo.ldproxy.net/zoomstack/)
publishes tiled feature data through an interface that conforms to OGC
API - Tiles.

An example request that can be used to retrieve data, referenced to
WebMercatorQuad, from the OS Zoomstack collection is
<https://demo.ldproxy.net/zoomstack/tiles/WebMercatorQuad/0/0/0?f=mvt>

In this case the data is encoded in Mapbox Vector Tiles (MVT) format.

Once downloaded, a client application can then display or process the
data.

![image](../../assets/images/mvt_example.png){width="40.0%"}

# Resources

This section provides basic information about the types of resources
that OGC API - Tiles offers.
