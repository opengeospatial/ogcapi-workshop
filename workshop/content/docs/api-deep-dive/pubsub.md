---
title: OGC API - Publish-Subscribe Workflow
---

# OGC API - Publish-Subscribe Workflow

!!! abstract "Audience"
    Students that are familiar with web services and APIs, and want to have
    an overview of the OGC API - Publish-Subscribe Workflow standard

!!! abstract "Learning Objectives"
    At the completion of the module students will be able to:

    - Explain what the OGC API - Publish-Subscribe Workflow standard is
    - Describe what can be done with Publish-Subscribe workflows in OGC API implementations
    - Understand the requirements classes offered by the standard (Discovery, message payloads)
    - Understand how to retrieve a description of the Publish-Subscribe capabilities of an OGC API implementation
    - Understand how channels and topics are derived from OGC API resource paths
    - Understand how notification message payloads are encoded (CloudEvents, GeoJSON)
    - Be able to find an OGC API endpoint that offers Publish-Subscribe capabilities and consume its notifications

## Introduction

[OGC API - Publish-Subscribe Workflow - Part 1: Core](https://docs.ogc.org/DRAFTS/25-030.html) is a
standard that defines building blocks that can be assembled to implement
Publish-Subscribe workflows (discovery, topic structure, encoding) as part
of the OGC API suite of Standards. Implementations of OGC API Standards
typically rely on clients *polling* the server for updates to collections
(new features, records, items, coverages, maps, etc.). Depending on a
collection's temporal resolution or frequency of updates, an
event-driven / Publish-Subscribe (Pub/Sub) architecture provides a
timely, efficient and low-latency approach for the delivery of data
updates or notifications of updates: instead of the client repeatedly
asking "has anything changed?", the server pushes a notification to
subscribers whenever something does change.

The standard defines a **discovery capability** that contains a topic
structure in support of binding to notifications for data access and
retrieval, and it defines **baseline message payloads** which can contain
summary descriptive information about a given notification of new data
events (new granule, new model run, and so on).

!!! note
    This tutorial module is not intended to be a replacement to the actual
    **OGC API - Publish-Subscribe Workflow - Part 1: Core** standard. The
    tutorial intentionally focuses on a subset of capabilities in order to
    get the student started with using the standard. Please refer to the
    [**OGC API - Publish-Subscribe Workflow - Part 1: Core** standard](https://docs.ogc.org/DRAFTS/25-030.html)
    for additional detail.

### Background

> History

  The standard builds on the OGC Publish-Subscribe Interface Standard
  (OGC 13-131r1), the recommendations put forward in the OGC Pub/Sub
  White Paper (OGC 20-081) produced as part of OGC Testbed 12, and the
  discussion paper for Publish-Subscribe workflow in OGC APIs
  (OGC 23-013). It generalizes and extends the approach previously
  specified in the **OGC API - Environmental Data Retrieval - Part 2:
  Publish-Subscribe Workflow** standard, which is superseded by this
  cross-cutting standard.

> Versions

  As of writing, **OGC API - Publish-Subscribe Workflow - Part 1: Core**
  (document 25-030) is a *Draft* standard available at
  <https://docs.ogc.org/DRAFTS/25-030.html>. This document is distributed
  for review and comment and is subject to change without notice, and may
  not be referred to as an OGC Standard.

> Use cases

  Numerous use cases exist for event-driven architectures and
  Publish-Subscribe workflows in OGC APIs:

  * **OGC API - Common:** a data publisher making their data available as
    a collection via an OGC API wishes to advertise a new dataset
    publication (a new collection).
  * **OGC API - Features:** a client wishes to subscribe to data granule
    inserts, updates or deletes from a feature collection.
  * **OGC API - Records:** a client wishes to subscribe to metadata
    updates from a given metadata repository. Instead of traditional
    polling (for the last 24 hours of updates, for example), real-time
    notifications are sent whenever a metadata record is added, updated
    or deleted.
  * **OGC API - Processes:** a client that has initiated a long-running
    process subscribes to a Pub/Sub broker to receive job status updates
    in real-time instead of polling for them.
  * **OGC API - Environmental Data Retrieval:** a numerical weather
    prediction (NWP) system produces a weather forecast as part of a
    model run. A Pub/Sub workflow can be applied where notifications are
    sent as individual weather elements (data granules) become available,
    or once the model run generation is complete.

  As an event-driven design pattern, Pub/Sub eliminates the need for
  continuous polling while, for example, a model run is in progress.

#### Usage

The standard provides building blocks to add an event-driven,
notification-based interface to an OGC API implementation. The key
property of this design is *reusability*: the OGC API service endpoint
specified by a URL path of resources and sub-resources can be used in
parallel as the **channel description** when the data publisher wishes to
provide Pub/Sub capability for resources normally available via an OGC
API implementation. For example:

* **/collections**: notifies subscribers whenever there is a change to
  the `/collections` resource (for example, the addition of a new
  collection). The message payload would be collection metadata, or a
  message referencing the collection metadata.
* **/collections/{collectionId}**: notifies subscribers whenever there is
  an update to a single collection resource (for example, spatial or
  temporal extents, new items, etc.). The message payload would be
  defined by either the resource model of the given collection (items,
  etc.), or a notification message of metadata referencing the collection
  with the relevant change.

Using the OGC API service endpoints of the URL path of resources and
sub-resources as channels provides the key benefit that developers
implementing OGC API Standards do not need to learn a different,
additional approach or resource path for Pub/Sub (same content,
additional interface).

In addition, for brokers providing notification metadata (as opposed to
actual data or record payloads), an implementation of OGC API Building
Blocks can, in parallel, provide GeoJSON based notification messages via
(for example) an OGC API - Features or OGC API - Records endpoint.
Providing message payloads via an OGC API provides the additional
benefit of querying for messages over time in case of a lost connection.

The workflow consists of three parts:

* **Data producers:** messages are published to a broker, applied to a
  given channel (for example `collections/mycollection`).
* **Broker provisioning:** the broker sends published messages to
  subscribers. An implementation MAY use the message queueing protocol of
  its choice and/or based on application requirements (for example
  MQTT, AMQP or WebSockets, which are all referenced by the standard).
* **Subscribers and data consumers:** messages are received by users
  subscribed to one or more channels (explicitly, or using wildcards or
  filtering).

#### Relation to other OGC Standards

* **OGC API - Common:** the landing page and link mechanisms defined in
  OGC API - Common are reused to expose Publish-Subscribe capabilities;
  in particular, links to AsyncAPI documents and to Pub/Sub brokers are
  expressed through the Common link object.
* **OGC API - Environmental Data Retrieval - Part 2: Publish-Subscribe
  Workflow:** the earlier, EDR-specific Pub/Sub standard that this
  standard generalizes into the broader OGC API suite.
* **OGC API - Features / OGC API - Records:** notification messages can
  themselves be published as GeoJSON items, allowing Pub/Sub message
  payloads to be queried with standard OGC API requests.
* **AsyncAPI:** the standard for describing event-driven APIs; the
  event-driven equivalent of what OpenAPI provides for OGC API
  Standards. OGC API implementations advertise their Pub/Sub capabilities
  through AsyncAPI documents.

### Overview of Capabilities

**OGC API - Publish-Subscribe Workflow - Part 1: Core** defines the
requirements classes and conformance classes listed in the following
table.

<table>
  <tr>
    <th>Requirements Class</th>
    <th>Conformance Class</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Discovery</td>
    <td>conf/discovery</td>
    <td>Links from OGC API (and OpenAPI) to AsyncAPI documents and Pub/Sub resources, so that clients can discover channels to subscribe to.</td>
  </tr>
  <tr>
    <td>Message Payloads - CloudEvents (JSON)</td>
    <td>conf/message-payload-cloudevents-json</td>
    <td>Requirements for message payloads encoded as CloudEvents in the JSON format.</td>
  </tr>
  <tr>
    <td>Message Payloads - GeoJSON</td>
    <td>conf/message-payload-geojson</td>
    <td>Requirements for notification message payloads encoded as GeoJSON (RFC 7946).</td>
  </tr>
</table>

A software implementation SHALL implement any one of the conformance
classes; the conformance classes are combined to describe the Pub/Sub
capabilities of a given implementation.

## Capabilities in Detail

This section provides basic information about the capabilities that
OGC API - Publish-Subscribe Workflow offers.

### Discovery

Event-driven workflows provide Publish-Subscribe based capabilities as
part of information systems and architectures. The Publish-Subscribe model
provides efficiencies in delivering data "as it happens", thereby
preventing potential clients from continuously polling to check on the
availability of new data or resources. The result is less network traffic
and more timely responses for event-based models such as urgent,
temporally unpredictable data (examples include, but are not limited to:
traffic conditions, weather or hazard warnings, and real-time sensor
data).

Discovery is achieved through a set of cross-referencing links:

* an OGC API **landing page** links to an **AsyncAPI document**
  describing the Pub/Sub capabilities (protocols, channels, message
  payloads),
* the AsyncAPI document links back to the equivalent **OGC API
  endpoint/resource**,
* **OpenAPI** definitions of the API can link to the AsyncAPI equivalent,
* OGC API resources link directly to the **Pub/Sub broker** and channel.

#### Links from OGC API to AsyncAPI

A landing page SHALL provide a link reference to the description of its
Publish-Subscribe capabilities using a link relation of
```service-desc```, and the description SHALL be provided using AsyncAPI
to describe the supported protocols, channels, and message payload
descriptions.

```json
{ "rel": "service-desc", "type": "application/asyncapi+json", "title": "AsyncAPI document", "href": "https://example.org/asyncapi?f=json" }
```

A landing page MAY also provide a link for human consumption using the
```service-doc``` link relation (for example an HTML representation).

To link to a specific channel of a collection, the `href` of the link
object references the AsyncAPI document (in JSON or YAML) with a URI
fragment that addresses the relevant channel object:

```json
{ "rel": "items", "title": "Data notifications", "href": "https://example.org/asyncapi.json#/channels/notify-collections" }
```

This allows a client to navigate to the relevant channel object in the
AsyncAPI document, bind to the channel/topic and have *a priori* access
to the schema of the message payload as needed.

#### Links from AsyncAPI to OGC API

For the reverse direction, an `x-ogc-link` object is made available as
part of a channel definition so that an AsyncAPI document can refer back
to the OGC API equivalent of the given resource:

```yaml
notify-collections:
  address: collections
  x-ogc-link:
    type: application/json
    rel: data
    href: https://api.example.org/collections
  messages:
    collection_msg:
      description: collection updated notification
      payload: $ref: '#/components/schemas/collection_msg'
```

#### Links from OpenAPI to AsyncAPI

Given OGC APIs utilize OpenAPI to describe the (request/response) API, an
`x-ogc-linkTemplate` object can be used to refer to the Pub/Sub
equivalent for the given resource. An `x-ogc-linkTemplate` object
structures a `uriTemplate` property that references the AsyncAPI document
(in JSON or YAML) with a URI template, which is useful when the channel
address includes an expression:

```json
{
  "/collections/discovery-metadata/items": {
    "get": {
      "description": "Discovery metadata records",
      "operationId": "getDiscoveryMetadataItems"
    },
    "x-ogc-linkTemplate": {
      "uriTemplate": "https://example.org/asyncapi.json#/channels/{collectionId}"
    }
  }
}
```

#### Links from OGC API to Pub/Sub resources

OGC API link objects can also point directly at the Pub/Sub capability
itself. Communicating an event-driven workflow from a link object is made
via the **```hub``` link relation**. This link relation communicates that
the link represents a Publish-Subscribe workflow, defined by the Pub/Sub
protocol in the `href` property as well as a `channel` property that
provides the relevant addressable topic that a client can subscribe to
after connecting to the Pub/Sub endpoint. The value and syntax of the
`channel` property is bound to the Pub/Sub protocol identified in the
`href` property.

```json
{ "rel": "hub", "title": "Data notifications", "href": "mqtt://example.org:8883", "channel": "collections/surface-weather-observations" }
```

A collection resource MAY provide a link reference to a Publish-Subscribe
server from an OGC API implementation endpoint when Publish-Subscribe
capabilities exist related to the collection service endpoint, and the
`channel` property allows for granular subscription.

#### Client side filtering

In some cases, users may wish to filter message payloads (when not
possible via a channel or topic structure) to process only payloads
matching given criteria. AsyncAPI natively supports this use case by
describing a channel's message payload using JSON Schema, thereby
allowing *a priori* knowledge of the payload when developing client
applications:

```yaml
notify-collections:
  address: collections
  messages:
    collection_msg:
      description: collection updated notification
      payload: $ref: '#/components/schemas/collection_msg'
components:
  schemas:
    collection_msg:
      type: object
      properties:
        id:
          type: string
          description: identifier
        title:
          type: string
          description: title of collection
      required:
        - id
```

By inspecting the message payload definition in the AsyncAPI channel, a
client SHOULD use it to determine the model of the resulting message
payload and can, for example:

* perform JSON Schema validation of each received message,
* evaluate each message based on a property (for example, searching the
  `title` property above for a certain string pattern or regular
  expression).

### Message Payloads - CloudEvents (JSON)

A key component of Pub/Sub workflows is the message payload. Once a
client subscribes to one or more channels from a given Pub/Sub server,
notification messages are sent using a given representation or encoding.
Notification messages can be issued using any encoding that is deemed
suitable by a given publisher, but the standard defines requirements for
two widely used, machine-readable encodings.

[CloudEvents](https://github.com/cloudevents/spec) is a specification
for describing event data in common formats to provide interoperability
across services, platforms and systems. When a CloudEvents (JSON) message
payload is used, the encoding SHALL be compliant to the JSON Event Format
for the CloudEvents Specification (v1.0.2), and the CloudEvents `type`
property SHALL start with the pattern `org.ogc.api.`. It is recommended
that the type include the resource type pertaining to the message
(e.g. `collection`, `collection.item`, `collection.map`, `process`,
`job`, etc.) and, for transactions of resources, the operation pertaining
to a given resource (e.g. `create`, `replace`, `update`, `delete`, etc.).

An example CloudEvents message payload for a created item with the
feature provided inline is:

```json
{
  "id": "6e1c7f9f-dd6c-48d9-bbc4-aef0625f1fb8",
  "specversion": "1.0",
  "type": "org.ogc.api.collection.item.create",
  "source": "https://example.org/api/collections/obs",
  "subject": "https://example.org/api/collections/obs/items/964",
  "time": "2025-08-27T12:36:33Z",
  "datacontenttype": "application/json",
  "data": {
    "type": "Feature",
    "id": "964",
    "geometry": {
      "type": "Point",
      "coordinates": [ -122, 49 ]
    },
    "properties": {
      "stn_id": 604,
      "datetime": "2000-10-30T18:24:39Z",
      "value": 99.9
    },
    "links": [
      {
        "rel": "collection",
        "type": "application/json",
        "title": "Observations",
        "href": "https://example.org/api/collections/obs"
      }
    ]
  }
}
```

Alternatively, the notification can reference the new resource by URI
rather than embedding it:

```json
{
  "id": "6e1c7f9f-dd6c-48d9-bbc4-aef0625f1fb8",
  "specversion": "1.0",
  "type": "org.ogc.api.collection.item.create",
  "source": "https://example.org/api/collections/obs",
  "subject": "https://example.org/api/collections/obs/items/964",
  "time": "2025-08-27T12:36:33Z",
  "datacontenttype": "application/json",
  "data": {
    "type": "application/geo+json",
    "rel": "item",
    "href": "https://example.org/api/collections/obs/items/964"
  }
}
```

Using notifications that reference the resource (rather than embedding
it) allows users to use a subscription to small metadata records, which
are more transportable, and which inform the user of changes prior to
requesting the possibly large source data, especially when bandwidth is
at a premium.

### Message Payloads - GeoJSON

[GeoJSON](https://www.rfc-editor.org/info/rfc7946) (IETF RFC 7946) can
be used for geospatial notification data to improve interoperability.
When a GeoJSON message payload is used, the following properties are
required:

* **`id`**: a globally unique identifier for the message, generated by
  the originator of the message. It remains the same throughout the
  lifetime of the message and is valuable for "replay" feed services,
  where a Pub/Sub client may have gone offline for a period of time.
  Note that multiple messages may communicate updates on the same
  resource, in which case the message payload can provide the resource
  identifier in another property. UUIDs (RFC 4122) are recommended.
* **`properties.pubtime`**: the date/time when the message was
  posted/published, in RFC 3339 format in the UTC timezone (`Z`). The
  publication date/time is critical for subscribers to prevent message
  loss and for providing awareness of how far behind the publisher they
  may be.
* **`properties.operation`**: indicates the stage of the lifecycle of the
  resource described in the notification, that is, whether a resource has
  been created, updated or deleted. The allowed values are `create`,
  `update` and `delete`; if not specified, the default value is
  `create`.

An example GeoJSON message payload is:

```json
{
  "id": "31e9d66a-cd83-4174-9429-b932f1abe1be",
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [ -122, 49 ]
  },
  "properties": {
    "id": "964",
    "pubtime": "2022-03-20T04:50:18.314854383Z",
    "operation": "create",
    "title": "New observation 964 in the 'obs' collection",
    "href": "https://example.org/api/collections/obs/items/964"
  }
}
```

!!! note
    The rest of this tutorial has focused on the core building blocks of
    the standard; the [standard](https://docs.ogc.org/DRAFTS/25-030.html)
    itself includes Annexes with conformance test suites and more
    complete message payload examples.

### Media Types

The standard indicates the media types that are to be used for the
encodings of the resources defined in it.

<table>
  <tr>
    <th>Resource type</th>
    <th>Link relation</th>
    <th>Media type</th>
  </tr>
  <tr>
    <td>AsyncAPI document (JSON)</td>
    <td>service-desc</td>
    <td>application/asyncapi+json</td>
  </tr>
  <tr>
    <td>AsyncAPI document (YAML)</td>
    <td>service-desc</td>
    <td>application/asyncapi+yaml</td>
  </tr>
  <tr>
    <td>AsyncAPI document (HTML)</td>
    <td>service-doc</td>
    <td>text/html</td>
  </tr>
  <tr>
    <td>CloudEvents message payload (JSON)</td>
    <td>N/A</td>
    <td>application/cloudevents+json</td>
  </tr>
  <tr>
    <td>CloudEvents batch message payload (JSON)</td>
    <td>N/A</td>
    <td>application/cloudevents-batch+json</td>
  </tr>
  <tr>
    <td>GeoJSON message payload (JSON)</td>
    <td>N/A</td>
    <td>application/geo+json</td>
  </tr>
</table>

## Summary

OGC API - Publish-Subscribe Workflow provides functionality for adding
event-driven, notification-based capabilities to OGC API implementations.
This deep dive provided an overview of the standard and the various
capabilities that are supported: discovering Pub/Sub channels through
AsyncAPI documents and `hub` links, deriving channel/topic structures
from OGC API resource paths, and encoding notification message payloads
as CloudEvents or GeoJSON.
