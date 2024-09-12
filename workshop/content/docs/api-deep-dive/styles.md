---
title: OGC API - Styles
---

# OGC API - Styles

!!! abstract "Audience"
    Students that are familiar with web services and APIs, and want to have an overview of OGC API - Styles standard

!!! abstract "Learning Objectives"
    At the completion of the module students will be able to:

    - Explain what the OGC API - Styles standard is
    - Describe what can be done with OGC API - Styles implementations
    - Understand the main resources offered by OGC API - Styles implementations
    - Understand how to retrieve a description of the capabilities of an OGC API - Styles implementation
    - Understand how to issue requests to an implementation of OGC API - Styles
    - Be able to find an OGC API - Styles endpoint and use it through a client

## Introduction

[OGC API - Styles](https://ogcapi.ogc.org/styles) is a standard that describes an API that enables map servers, clients as well as visual style editors, to manage and fetch styles. The styles consist of symbolizing instructions that can be applied by a rendering engine on features and/or coverages. The API implements the conceptual model for style encodings and style metadata.

!!! note
    This tutorial module is not intended to be a replacement to the actual
    **OGC API - Styles - Part 1: Core** standard. The tutorial intentionally
    focuses on a subset of capabilities in order to get the student started
    with using the standard. Please refer to the [**OGC API - Styles - Part 1:
    Core** standard](https://docs.ogc.org/DRAFTS/20-009.html) for additional detail.

### Background

> History

The need for users and software to be able to control the visual portrayal of geospatial data was already present in the first generation of OGC Web Services. A profile of the [Web Map Service (WMS)](https://www.ogc.org/standard/wms/) Standard was published in 2007, for the definition of a [Styled Layer Descriptor (SLD)](https://www.ogc.org/standard/sld/); this profile defined an encoding that extends the WMS standard to allow user-defined symbolization and coloring of geographic feature and coverage data. 
The evolution of the new web APIs also brought new capabilities in terms of changing, sharing and rendering styles, which were explored in OGC Testbed-15 Open Portrayal Framework (OPF), in 2019. This work was documented in the [OGC Testbed-15: Styles API Engineering Report](https://docs.ogc.org/per/19-010r2.html). The following year, in 2020, the charter for the OGC API - Styles Standards Working Group was drafted.

> Versions

  **OGC API - Styles - Part 1: Core** is currently in draft.

> Test suite

  There are no test suites currently implemented; they will be made available once the specification is
  approved, and an executable test suite (ETS) is made availabe as per of OGC CITE.

> Implementations

  Implementations can be found on the [implementations page](https://github.com/opengeospatial/ogcapi-styles/blob/master/implementations.md).

#### Usage

The Styles API supports three main types of consumers:

* Visual style editors that create, update and delete styles for datasets shared by other OGC APIs that publish feature or coverage data. Feature data is either accessed directly or organized into spatial partitions (e.g.: vector tiles).
* OGC API - Maps implementations, that fetch styles and render spatial data (features or coverages) on the server.
* Map clients that fetch styles and render spatial data (features or coverages) on the client.

The draft Standard also defines a conceptual model for styles, style encodings and style metadata. The model defines three main concepts, which are mapped to resources and documents.

* **Style**: the main resource.
* **Stylesheets**: the representation of a style in an encoding like OGC SLD 1.0 or Mapbox Style. Each style is available in one or more stylesheets. Clients will use the stylesheet of a style that fits best based on the capabilities of available tools and their preferences. 
* **Style metadata**: general descriptive information about the style, structural information (e.g., layers and attributes), and so forth to allow users to discover and select existing styles for their data. For each style there is style metadata available.

!!! note

    *Draft* **OGC API - Styles - Part 1**: Core offers conformance classes for fetching styles and style metadata, managing and validating styles.

#### Relation to other standards

OGC API - styles is designed to be combined with other OGC API Standards, in order to produce styled geospatial data.
Feature or coverage data published through OGC APIs, can be styled on client side with styles produced by OGC API - Styles editors. This is the case of OGC API - Features, OGC API - Coverages or OGC API - Tiles (vector tiles).
OGC API - Maps has support for fetching styles and rendering geospatial data (features or coverages) on server side. 

The styles themselves can be represented using different encodings. As usual in OGC API, no encodings are prescribed, although the draft Standard offers conformance classes for [OGC SLD 1.0](http://portal.opengeospatial.org/files/?artifact_id=1188)/[1.1](http://portal.opengeospatial.org/files/?artifact_id=22364) and [Mapbox Styles](https://docs.mapbox.com/style-spec/guides/).

### Overview of Resources

**OGC API - Styles - Part 1: Core** defines the resources listed in
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
    <td>Fetch Styles</td>
    <td>GET</td>
    <td>/styles</td>
    <td>This resource lists the styles that are offered through the API.</td>
  </tr>
  <tr>
    <td>Create or validate Styles</td>
    <td>POST</td>
    <td>/styles</td>
    <td>This resource enables the creation of a new Style or the validation of an existing one.</td>
  </tr>
  <tr>
    <td>Fetch Style</td>
    <td>GET</td>
    <td>/styles/{styleId}</td>
    <td>This resource retrieves the style identified in the path.</td>
  </tr>
  <tr>
    <td>Create or validate Style</td>
    <td>PUT</td>
    <td>/styles/{styleId}</td>
    <td>This resource can be used to update, create or validate the style identified in the path.</td>
  </tr>
  <tr>
    <td>Delete Style</td>
    <td>DELETE</td>
    <td>/styles/{styleId}</td>
    <td>This resource can be used to delete the style identified in the path.</td>
  </tr>
  <tr>
    <td>Fetch Style metadata</td>
    <td>GET</td>
    <td>/styles/{styleId}/metadata</td>
    <td>This resource retrieves the metadata of the style identified in the path.</td>
  </tr>
  <tr>
    <td>Replace Style metadata</td>
    <td>PUT</td>
    <td>/styles/{styleId}</td>
    <td>This resource replaces the metadata of the style identified in the path.</td>
  </tr>
  <tr>
    <td>Patch Style metadata</td>
    <td>PATCH</td>
    <td>/styles/{styleId}</td>
    <td>This resource updates parts of the metadata of the style identified in the path.</td>
  </tr>
  <tr>
    <td>Fetch resources</td>
    <td>GET</td>
    <td>/resources</td>
    <td>This operation fetches the set of resources (e.g.: symbols and sprites) that have been created and that may be used by reference in stylesheets.</td>
  </tr>
  <tr>
    <td>Fetch symbol resource by id</td>
    <td>GET</td>
    <td>/resources/{resourceId}</td>
    <td>This operation fetches the resource with identifier resourceId. The set of available resources can be retrieved at /resources.</td>
  </tr>
  <tr>
    <td>Replace symbol resource or add new one</td>
    <td>PUT</td>
    <td>/resources/{resourceId}</td>
    <td>This operation replaces an existing resource with the id resourceId. If no such resource exists, a new resource with that id is added. This operation is only available to registered style authors.</td>
  </tr>
  <tr>
    <td>Delete symbol resource</td>
    <td>DELETE</td>
    <td>/resources/{resourceId}</td>
    <td>This operation deletes an existing resource with the id resourceId. If no such resource exists, an error is returned. This operation is only available to registered style authors.</td>
  </tr>
</table>

!!! note

    A *sprite* used in a Mapbox Style stylesheet consists of three resources: 

    * PNG bitmap image (resourceId ends in '.png').
    * JSON index file (resourceId of the same name, but ends in '.json' instead of '.png')
    * PNG bitmap image for high-resolution displays (the file ends in '.@2x.png').
    
    Each of the resources needs to be created (and eventually deleted) separately. 

