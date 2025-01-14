---
title: "Computing US airport connections and route interpolations"
description: "In this example we will showcase how easily we can compute all the paths that interconnect the main four US airports using the Analytics Toolbox."
image: "/img/bq-analytics-toolbox/examples/us-airport-connections-route-interpolations.png"
type: examples
date: "2021-05-12"
categories:
    - transformations
aliases:
    - /analytics-toolbox-bq/examples/computing-us-airport-connections-and-route-interpolations/
---
## Computing US airport connections and route interpolations

### Generating connections

In this example we will showcase how easily we can compute all the paths that interconnect the main four US airports using the Analytics Toolbox.

```sql
WITH data AS(
    SELECT *
    FROM `carto-do-public-data`.natural_earth.geography_glo_airports_410 
	WHERE abbrev = 'JFK' OR abbrev = 'LAX'  OR abbrev = 'SEA'  OR abbrev = 'MIA'
)
SELECT `carto-un`.carto.ST_GREATCIRCLE(t1.geom, t2.geom, 25) AS geo
FROM data AS t1
CROSS JOIN data AS t2
WHERE t1.abbrev != t2.abbrev
```

This query first creates all the possible combinations between airports and then generates the paths between them using the `ST_GREATCIRCLE` function. The resulting paths contain 25 points, but you can set the number of points in order to make the lines smoother if needed.

The result is displayed in this visualization. Notice we are not using straight lines to interconnect the different airports, but great circles instead.

<iframe height=480px width=100% style='margin-bottom:20px' src="https://public.carto.com/builder/f54fe4b8-fee3-4e2d-a9d1-4f8a632eba71" title="US airports connections."></iframe> 


### Routes interpolation

Now let's put to the test how to perform line interpolations using the `ST_LINE_INTERPOLATE_POINT` function. In this example we will compute the airplane position after taking off from the different airports and travelling a certain distance.

```sql
WITH data AS(
    SELECT *
    FROM `carto-do-public-data`.natural_earth.geography_glo_airports_410 
	WHERE abbrev = 'JFK' OR abbrev = 'LAX'  OR abbrev = 'SEA'  OR abbrev = 'MIA'
)
SELECT CONCAT(t1.abbrev, " - ", t2.abbrev) as route, `carto-un`.carto.ST_LINE_INTERPOLATE_POINT(`carto-un`.carto.ST_GREATCIRCLE(t1.geom, t2.geom, 25), 500,'kilometers') AS geo
FROM data AS t1
CROSS JOIN data AS t2
WHERE t1.abbrev != t2.abbrev
```

This query uses the `ST_LINE_INTERPOLATE_POINT` function over each great circle in order to calculate the location of the plane after travelling 500 kilometers. In the following visualization you can see these locations as well as their origin and destination airports.

<iframe height=480px width=100% style='margin-bottom:20px' src="https://public.carto.com/builder/b5c490e8-81ec-4c6f-ad67-864509d734d6" title="US airports routes interpolation."></iframe>

{{% euFlagFunding %}}
