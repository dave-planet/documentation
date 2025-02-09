---
aliases:
    - /analytics-toolbox-bq/sql-reference/transformations/
---
## transformations

<div class="badges"><div class="core"></div></div>

This module contains functions that compute geometric constructions, or alter geometry size or shape.

### ST_BUFFER

{{% bannerNote type="code" %}}
carto.ST_BUFFER(geog, radius, units, steps)
{{%/ bannerNote %}}

**Description**

Calculates a Geography buffer for input features for a given radius. Units supported are miles, kilometers, and degrees.

* `geog`: `GEOGRAPHY` input to be buffered.
* `radius`: `FLOAT64` distance to draw the buffer (negative values are allowed).
* `units`: `STRING`|`NULL` units of length, the supported options are: miles, kilometers, and degrees. If `NULL`the default value `kilometers` is used.
* `steps`: `INT64`|`NULL` number of steps. If `NULL` the default value `8` is used.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_BUFFER(ST_GEOGPOINT(-74.00, 40.7128), 1, "kilometers", 10);
-- POLYGON((-73.9881354374691 40.7127993926494 ... 
```

### ST_CENTERMEAN

{{% bannerNote type="code" %}}
carto.ST_CENTERMEAN(geog)
{{%/ bannerNote %}}

**Description**

Takes a Feature or FeatureCollection and returns the mean center.

* `geog`: `GEOGRAPHY` feature to be centered.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_CENTERMEAN(ST_GEOGFROMTEXT("POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"));
-- POINT(25.3890912155939 29.7916831655627)
```

### ST_CENTERMEDIAN

{{% bannerNote type="code" %}}
carto.ST_CENTERMEDIAN(geog)
{{%/ bannerNote %}}

**Description**

Takes a FeatureCollection of points and calculates the median center, algorithimically. The median center is understood as the point that requires the least total travel from all other points.

* `geog`: `GEOGRAPHY` feature to be centered.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_CENTERMEDIAN(ST_GEOGFROMTEXT("POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"));
-- POINT(25.3783930513609 29.8376035441371)
```

### ST_CENTEROFMASS

{{% bannerNote type="code" %}}
carto.ST_CENTEROFMASS(geog)
{{%/ bannerNote %}}

**Description**

Takes any Feature or a FeatureCollection and returns its center of mass using this formula: Centroid of Polygon.

* `geog`: `GEOGRAPHY` feature to be centered.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_CENTEROFMASS(ST_GEOGFROMTEXT("POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"));
-- POINT(25.1730977433239 27.2789529273059) 
```

### ST_CONCAVEHULL

{{% bannerNote type="code" %}}
carto.ST_CONCAVEHULL(geog, maxEdge, units)
{{%/ bannerNote %}}

**Description**

Takes a set of points and returns a concave hull Polygon or MultiPolygon. In case of a single or a couple of points are passed as input, the function will return that point or a segment respectively.

* `geog`: `ARRAY<GEOGRAPHY>` input points.
* `maxEdge`: `FLOAT64`|`NULL` the length (in 'units') of an edge necessary for part of the hull to become concave. If `NULL`the default value `infinity` is used.
* `units`: `STRING`|`NULL` units of length, the supported options are: miles, kilometers, degrees or radians. If `NULL`the default value `kilometers` is used.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_CONCAVEHULL([ST_GEOGPOINT(-75.833, 39.284),ST_GEOGPOINT(-75.6, 39.984),ST_GEOGPOINT(-75.221, 39.125),ST_GEOGPOINT(-75.521, 39.325)], 100, 'kilometers');
-- POLYGON((-75.68 39.24425, -75.527 39.2045 ...
```
``` sql
SELECT `carto-os`.carto.ST_CONCAVEHULL([ST_GEOGPOINT(-75.833, 39.284)], 100, 'kilometers');
-- POINT(-75.833 39.284)
```

### ST_DESTINATION

{{% bannerNote type="code" %}}
carto.ST_DESTINATION(startPoint, distance, bearing, units)
{{%/ bannerNote %}}

**Description**

Takes a Point and calculates the location of a destination point given a distance in degrees, radians, miles, or kilometers; and bearing in degrees. This uses the Haversine formula to account for global curvature.

* `origin`: `GEOGRAPHY` starting point.
* `distance`: `FLOAT64` distance from the origin point.
* `bearing`: `FLOAT64` ranging from -180 to 180.
* `units`: `STRING`|`NULL` units of length, the supported options are: miles, kilometers, degrees or radians. If `NULL`the default value `kilometers` is used.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_DESTINATION(ST_GEOGPOINT(-3.70325,40.4167), 10, 45, "miles");
-- POINT(-3.56862505487045 40.5189626777536)
```

### ST_GREATCIRCLE

{{% bannerNote type="code" %}}
carto.ST_GREATCIRCLE(startPoint, endPoint, npoints)
{{%/ bannerNote %}}

**Description**

Calculate great circles routes as LineString or MultiLineString. If the start and end points span the antimeridian, the resulting feature will be split into a MultiLineString.

* `startPoint`: `GEOGRAPHY` source point feature.
* `endPoint`: `GEOGRAPHY` destination point feature.
* `npoints`: `INT64`|`NULL` number of points. If `NULL` the default value `100` is used.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_GREATCIRCLE(ST_GEOGPOINT(-3.70325,40.4167), ST_GEOGPOINT(-73.9385,40.6643), 20);
-- LINESTRING(-3.70325 40.4167 ... 
```

### ST_LINE_INTERPOLATE_POINT

{{% bannerNote type="code" %}}
carto.ST_LINE_INTERPOLATE_POINT(geog, distance, units)
{{%/ bannerNote %}}

**Description**

Takes a LineString and returns a Point at a specified distance along the line.

* `geog`: `GEOGRAPHY` input line.
* `distance`: `FLOAT64` distance along the line.
* `units`: `STRING`|`NULL` units of length, the supported options are: miles, kilometers, degrees and radians. If `NULL`the default value `kilometers` is used.

**Return type**

`GEOGRAPHY`

{{% customSelector %}}
**Example**
{{%/ customSelector %}}

``` sql
SELECT `carto-os`.carto.ST_LINE_INTERPOLATE_POINT(ST_GEOGFROMTEXT("LINESTRING (-76.091308 18.427501,-76.695556 18.729501,-76.552734 19.40443,-74.61914 19.134789,-73.652343 20.07657,-73.157958 20.210656)"), 250, 'miles');
-- POINT(-74.297592068938 19.4498107103156) 
```

{{% euFlagFunding %}}