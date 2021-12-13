## clustering

<div class="badges"><div class="advanced"></div></div>

This module contains functions that perform clustering on geographies.

### ST_CLUSTERKMEANS

{{% bannerNote type="code" %}}
carto.ST_CLUSTERKMEANS(geog [, numberOfClusters])
{{%/ bannerNote %}}

**Description**

Takes a set of points as input and partitions them into clusters using the k-means algorithm. Returns an array of tuples with the cluster index for each of the input features and the input geometry.

* `geog`: `GEOMETRY` points to be clustered.
* `numberOfClusters` (optional): `INT` number of clusters that will be generated. It defaults to `Math.sqrt(<NUMBER OF POINTS>/2)`.

**Return type**

`SUPER`: containing objects with `cluster` as the cluster id and `geom` as the geometry in GeoJSON format.

**Examples**

```sql
SELECT carto.ST_CLUSTERKMEANS(ST_GEOMFROMTEXT('MULTIPOINT ((0 0), (0 1), (5 0), (1 0))'));
-- {"cluster":0,"geom":{"type":"Point","coordinates":[0.0,0.0]}}
-- {"cluster":0,"geom":{"type":"Point","coordinates":[0.0,1.0]}}
-- {"cluster":0,"geom":{"type":"Point","coordinates":[5.0,0.0]}}
-- {"cluster":0,"geom":{"type":"Point","coordinates":[1.0,0.0]}}
```

```sql
SELECT carto.ST_CLUSTERKMEANS(ST_GEOMFROMTEXT('MULTIPOINT ((0 0), (0 1), (5 0), (1 0))'), 2);
-- {"cluster":0,"geom":{"type":"Point","coordinates":[0.0,0.0]}}
-- {"cluster":0,"geom":{"type":"Point","coordinates":[0.0,1.0]}}
-- {"cluster":1,"geom":{"type":"Point","coordinates":[5.0,0.0]}}
-- {"cluster":0,"geom":{"type":"Point","coordinates":[1.0,0.0]}}
```