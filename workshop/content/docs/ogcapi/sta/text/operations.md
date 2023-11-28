# SensorThings - Operations

The entities offered by a SensorThings API service can be accessed by
appending a resource path to the service root URI. An example of a URL
that retrieves observations is shown below.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations>

An extract of the response is presented below. Notice how the instances
of the requested entity are presented in a JSON array.

``` javascript
{"@iot.count":1594349,
    "@iot.nextLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$top=100&$skip=100","value":
        [
            {"@iot.id":1595550,"@iot.selfLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595550)","phenomenonTime":"2017-02-16T21:55:12.841Z","result":"7","resultTime":null,"Datastream@iot.navigationLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595550)/Datastream","FeatureOfInterest@iot.navigationLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595550)/FeatureOfInterest"
                },
            {"@iot.id":1595551,"@iot.selfLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595551)","phenomenonTime":"2017-02-16T21:55:12.841Z","result":"4","resultTime":null,"Datastream@iot.navigationLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595551)/Datastream","FeatureOfInterest@iot.navigationLink":"http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595551)/FeatureOfInterest"
                },
                ...
        ]
}
```

Other entities can also be retrieved through resource paths of a similar
pattern. The following table lists the resource paths of each entity
type.

<table>
  <caption>Entity Sets Offered</caption>
  <tr>
    <th>Entity Set</th>
    <th>Resource Path</th>
  </tr>
  <tr>
    <td>Things</td>
    <td>/Things</td>
  </tr>
  <tr>
    <td>Locations</td>
    <td>/Locations</td>
  </tr>
  <tr>
    <td>Historical locations</td>
    <td>/HistoricalLocations</td>
  </tr>
  <tr>
    <td>Datastreams</td>
    <td>/Datastreams</td>
  </tr>
  <tr>
    <td>Sensors</td>
    <td>/Sensors</td>
  </tr>
  <tr>
    <td>Observed properties</td>
    <td>/ObservedProperties</td>
  </tr>
  <tr>
    <td>Observations</td>
    <td>/Observations</td>
  </tr>
  <tr>
    <td>Features of interest</td>
    <td>/FeaturesOfInterest</td>
  </tr>
</table>

In addition to accessing an entity, the property of an entity can also
be accessed in a similar way by appending the name of the property to
the resource path. The following is an example of a request that
retrieves a property named ```result``` from a specific observation.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations(1595550)/result>

Examples of resource paths of properties are shown in the following
table.

<table>
  <caption>Property Resource Path Examples</caption>
  <tr>
    <th>Property</th>
    <th>Resource Path</th>
  </tr>
  <tr>
    <td>Result of an observation with an ID of 1595550</td>
    <td>/Observations(1595550)/result</td>
  </tr>
  <tr>
    <td>The name of a feature of interest</td>
    <td>/Sensor(4)/metadata</td>
  </tr>
  <tr>
    <td>Coordinates of the feature observed by observation 1595550</td>
    <td>/Observations(1595550)/FeatureOfInterest/feature</td>
  </tr>
</table>

## Retrieval Options {#sta_retrieval}

### $filter

The ```$filter``` system option allows clients to filter a collection of
entities that are addressed by a request URL.

For example, the following request returns all Observations whose result
is less than 15.00.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$filter=result%20lt%2015.00>

### $count

The ```$count``` query option specifies whether the total count of items
within a collection matching the request should be returned along with
the result.

For example, the following request returns the total number of
Observations in the collection, as well as the results. Changing the
value of the ```$count``` option to false causes the count to be omitted from
the response.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$count=true>

### $orderby

The ```$orderby``` query option specifies the order in which items are
returned from the service.

For example, the following request all Observations arranged in
ascending order of the result property

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$orderby=result>

### $skip

The ```$skip``` query option specifies the number for the items of the
queried collection that should be excluded from the result.

For example, the following request all Observations starting with the
twenty-first Observation entity.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$skip=20>

### $top

The ```$top``` query option specifies the limit on the number of items
returned from a collection of entities.

For example, the following request returns only the first six entities
in the Observations collection.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$top=6>

### $expand

The ```$expand``` query option enables the client to specify the set of
properties to be included in a response by indicating that the related
entities are to be represented inline.

For example, the following request returns the complete entity set of
Things and their associated Datastreams.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Things?$expand=Datastreams>

### $select

The ```$select``` query option enables the client to specify the set of
properties to be included in a response by instructing the service to
return only the properties explicitly requested.

For example, the following request returns each Observation entity with
only the result and phenomenonTime properties listed.

<http://toronto-bike-snapshot.sensorup.com/v1.0/Observations?$select=result,phenomenonTime>

## References

-   [SensorUp SensorThings API](https://www.sensorup.com/)
