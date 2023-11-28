Position Query Resources of OGC API - EDR ================

A position is a data type that describes a point or geometry potentially
occupied by an object or person. An illustration, created using NASA
WorldWind, is shown below.

![image](../img/position.png){width="80.0%"}

The [position]{.title-ref} query resource returns data for the requested
position. The resource offers a convenience mechanism for querying the
API using a Well Known Text (WKT) POINT geometry defining a position.

The path to the resource is shown below:

[/collections/{collectionId}/position]{.title-ref}

The paths accepts the following parameters:

-   coords
-   z
-   parameter-name
-   datetime
-   crs
-   f

An example request is shown below.

[http://example.org/edr/collections/obs_demo/position?coords=POINT(0.00577%2051.562608)&parameter-name=Wind%20Direction&datetime=2022-01-19T10:00Z/2022-01-19T12:00Z&crs=CRS84&f=GeoJSON]{.title-ref}
