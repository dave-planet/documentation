---
aliases:
    - /analytics-toolbox-sf/sql-reference/clustering/
---
## clustering

<div class="badges"><div class="advanced"></div></div>

This module contains functions that perform clustering on geographies.

### ST_CLUSTERKMEANS

{{% bannerNote type="code" %}}
carto.ST_CLUSTERKMEANS(geog [, numberOfClusters])
{{%/ bannerNote %}}

**Description**

Takes a set of points and partition them into clusters using the k-mean. It uses the k-means algorithm. Returns an array of tuples with the cluster index for each of the input features and the input geometry.

* `geojsons`: `ARRAY` points to be clustered.
* `numberOfClusters` (optional): `INT` numberOfClusters that will be generated. By default `numberOfClusters` is `Math.sqrt(<NUMBER OF POINTS>/2)`.

**Return type**

`ARRAY`: containing objects with `cluster`, as the cluster id, and `geom`, as the geometry geojson.

**Examples**

```sql
SELECT carto.ST_CLUSTERKMEANS(ARRAY_CONSTRUCT(ST_ASGEOJSON(ST_POINT(0, 0))::STRING, ST_ASGEOJSON(ST_POINT(0, 1))::STRING, ST_ASGEOJSON(ST_POINT(5, 0))::STRING, ST_ASGEOJSON(ST_POINT(1, 0))::STRING));
-- {"cluster": 0, "geom": "{\"coordinates\":[0,0],\"type\":\"Point\"}"}
-- {"cluster": 0, "geom": "{\"coordinates\":[0,1],\"type\":\"Point\"}"}
-- {"cluster": 0, "geom": "{\"coordinates\":[5,0],\"type\":\"Point\"}"}
-- {"cluster": 0, "geom": "{\"coordinates\":[1,0],\"type\":\"Point\"}"}
```

```sql
SELECT carto.ST_CLUSTERKMEANS(ARRAY_CONSTRUCT(ST_ASGEOJSON(ST_POINT(0, 0))::STRING, ST_ASGEOJSON(ST_POINT(0, 1))::STRING, ST_ASGEOJSON(ST_POINT(5, 0))::STRING, ST_ASGEOJSON(ST_POINT(1, 0))::STRING), 2);
-- {"cluster": 1, "geom": "{\"coordinates\":[0,0],\"type\":\"Point\"}"}
-- {"cluster": 1, "geom": "{\"coordinates\":[0,1],\"type\":\"Point\"}"}
-- {"cluster": 0, "geom": "{\"coordinates\":[5,0],\"type\":\"Point\"}"}
-- {"cluster": 1, "geom": "{\"coordinates\":[1,0],\"type\":\"Point\"}"}
```