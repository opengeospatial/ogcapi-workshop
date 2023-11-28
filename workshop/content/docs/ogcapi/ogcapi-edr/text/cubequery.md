Cube Query Resources of OGC API - EDR ================

A cube is a rectangular area, with a vertical extent. An illustration,
created using NASA WorldWind, is shown below.

![image](../img/cube.png){width="80.0%"}

The [cube]{.title-ref} query resource returns data for a defined cube.
The resource offers a convenience mechanism for querying the API using a
bounding box (BBOX) defining a cube.

The path to the resource is shown below:

[/collections/{collectionId}/cube]{.title-ref}

The paths accepts the following parameters:

-   bbox
-   z
-   parameter-name
-   datetime
-   crs
-   f
