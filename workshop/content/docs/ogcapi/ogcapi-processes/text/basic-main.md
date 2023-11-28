# An Introduction to OGC API - Processes

## Introduction

The OGC API --- Processes standard supports the wrapping of
computational tasks into executable processes that can be offered by a
server through a Web API and be invoked by a client application. The
standard specifies a processing interface to communicate over a RESTful
protocol using JavaScript Object Notation (JSON) encodings. The standard
leverages concepts from the OGC Web Processing Service (WPS) 2.0
Interface Standard but does not require implementation of a WPS. The
Core part of the standard is called **OGC API - Processes - Part 1:
Core**. The Core part of the standard supports the wrapping of
computational tasks into executable processes that can be offered by a
server through a Web API and be invoked by a client application either
synchronously or asynchronously. Examples of computational processes
that can be supported by implementations of this specification include
raster algebra, geometry buffering, constructive area geometry, routing,
imagery analysis and several others.

!!! note
    This tutorial module is not intended to be a replacement to the actual
    **OGC API - Processes - Part 1: Core** standard. The tutorial
    intentionally focuses on a subset of capabilities in order to get the
    student started with using the standard. Please refer to the **OGC API -
    Processes - Part 1: Core** standard for additional detail.

## Background

### History

Several of the concepts specified in OGC API - Processes originated in work specifying a RESTful interface for WPS 2.0. From February 2019 onwards, all work relating to a RESTful interface for the WPS2.0 was changed to focus on OGC API - Processes.

### Versions

**OGC API - Processes - Part 1: Core** version 1.0.0 is the current latest version

### Test Suite

**Draft** Test suites are available for:

-   [OGC API - Processes](https://github.com/opengeospatial/ets-ogcapi-processes10)

### Implementations

Implementations can be found here <https://github.com/opengeospatial/ogcapi-processes/blob/master/implementations.adoc>

### Usage

**OGC API - Processes - Part 1: Core** supports the wrapping of
computational tasks into executable processes that can be offered by a
server through a Web API and be invoked by a client application.
Government agencies, private organisations and academic institutes use
the OGC API - Processes standard to provide implementations of
geospatial algorithms that process data. The benefit of this is that the
processing of geospatial data, including data from sensors, can be
distributed thereby allowing for more capacity to process larger amounts
of data.

### Relation to other OGC Standards

-   OGC Web Processing Service Interface Standard (WPS): The WPS
    Standard provides a standard interface that simplifies the task of
    making simple or complex computational geospatial processing
    services accessible via web services. The OGC API --- Processes
    Standard is a newer and more modern way of programming and
    interacting with resources over the web while allowing better
    integration into existing software packages. The OGC
    API --- Processes Standard addresses all of the use cases that were
    addressed by the WPS Standard, while also leveraging the OpenAPI
    specification and a resource-oriented approach.

## Overview of Resources

**OGC API - Processes - Part 1: Core** defines the resources listed in
the following table.


<table>
  <tr>
    <th>Resource</th>
    <th>Path</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Landing page</td>
    <td>/</td>
    <td>This is the top-level resource, which serves as an entry point.</td>
  </tr>
  <tr>
    <td>Conformance declaration</td>
    <td>/conformance</td>
    <td>This resource presents information about the functionality that is implemented by the server.</td>
  </tr>
  <tr>
    <td>API definition</td>
    <td>/api</td>
    <td>This resource provides metadata about the API itself. Note use of /api on the server is optional and the API definition may be hosted on completely separate server.</td>
  </tr>
  <tr>
    <td>Process list</td>
    <td>/processes </td>
    <td>Process identifiers, links to process descriptions.</td>
  </tr>
  <tr>
    <td>Process description </td>
    <td>/processes/{processID}</td>
    <td>Retrieves a process description.</td>
  </tr>
  <tr>
    <td>Process execution</td>
    <td>/processes/{processID}/execution</td>
    <td>Creates and executes a job.</td>
  </tr>
  <tr>
    <td>Job status info</td>
    <td>/jobs/{jobID}</td>
    <td>Retrieves information about the status of a job./td>
  </tr>
  <tr>
    <td>Job results</td>
    <td>/jobs/{jobID}/results</td>
    <td>Retrieves the resul(s) of a job./td>
  </tr>
  <tr>
    <td>Job list</td>
    <td>/jobs</td>
    <td>Retrieves the list of jobs./td>
  </tr>
  <tr>
    <td>Job Deletion</td>
    <td>/jobs/{jobID} </td>
    <td>Cancels and deletes a job./td>
  </tr>
</table>

# Example

This ZOO-Project [demonstration
server](http://tb17.geolabs.fr:8090/ogc-api/index.html) from OGC
Testbed-17 implements a variety of processing algorithms through an
interface that conforms to OGC API - Processes.

The processes offered by the server can be browsed at
<http://tb17.geolabs.fr:8090/ogc-api/processes.html>
