---
aliases:
    - /analytics-toolbox-sf/overview/tilesets/
---

## Tilesets

The tiler is a module of the Analytics Toolbox for Snowflake that allows to process and visualize very large spatial datasets (millions or even billions of rows) stored in Snowflake.

### How it works

The tiler procedures will process your data and create a complete tileset out of it. All the map tiles for the specified zoom range will be stored in a Snowflake table in GeoJSON format. Each individual tile is a row in this table, with the tile coordinates and the corresponding geometry data stored in different columns:

| Row | z | x | y | data |
|-----|---|---|---|-----------------|
| 1   | 16 | 45340 | 24576 | {"geometry":{"coordinates":[-138.50516208988,... |
| 2   | 16 | 45292 | 24576 | {"geometry":{"coordinates":[-164.87444768784,... |

Visualizing and publishing your tilesets is straight-forward using [Builder](/carto-user-manual/maps/add-source/#add-source-from-a-connection), the map making tool integrated into the CARTO Workspace.

The integration of tilesets with custom web map applications is also possible with CARTO Maps API, which will connect to Snowflake using your connection's credentials to fetch and serve the tiles.


### Tileset types and procedures

The tiler module enables the creation of three types of tilesets: *simple*, *aggregation* and *spatial index* tilesets. _Simple_ tilesets encode all the input features as is, while _aggregation_ tilesets encode aggregations over the input features. Therefore, you should use _simple_ tilesets for visualizing a dataset of world rivers, but use an _aggregation_ tileset to visualize a heatmap of the trees distribution in New York City. On the other hand, _spatial index_ tilesets allow the creation of tilesets aggregating data from an input table that uses H3 or Quadbin spatial indexes as geographic support systems.  

We provide the following set of procedures to create tilesets:

1. `carto.CREATE_SIMPLE_TILESET`
    * This procedure creates a _simple_ tileset. You should use it if you have a dataset with any geography type (point, line, or polygon) and you want to visualize it at an appropriate zoom level.
    * The geographies will be represented exactly as stored in BigQuery, which means that if they are too small to be visible at a certain zoom level they won't be included in the tiles at that zoom level.
    * The values associated with each feature are the same as the ones available in the source dataset.

2. `carto.CREATE_POINT_AGGREGATION_TILESET`
    * Use this procedure if you have a point dataset (or anything that can be converted to points, such as polygon centroids) and you want to see it aggregated.
    * The points will be aggregated into cells. Each feature or cell represents all the points that fall under it, so the associated properties available for visualization are generated by aggregating the values in the source dataset.

3. `carto.CREATE_SPATIAL_INDEX_TILESET`
    * Use this procedure if you have a dataset based on spatial indexes, and you want to build a tileset aggregating data in the same spatial index (H3 and QUADBIN are currently supported).
    * Aggregated data will be computed for all levels between `resolution_min` and `resolution_max`.
    * For each resolution level, all tiles for the area covered by the source table are added, with data aggregated at level `resolution + aggregation resolution`. 


### Benefits

The tiler is:

* **Convenient** -- It can be run directly as SQL commands in Snowflake. The data never leaves Snowflake so you won't have to worry about security and additional ETLs.
* **Fast** -- It benefits from the massive scalability capabilities of Snowflake and can process hundreds of millions of rows in a few minutes.
* **Scalable** -- This solution works well for 1M points or 100B points.
* **Cost-effective** -- Since Snowflake separates storage from computing, the actual cost of hosting these tilesets is very low. Additionally, since the tiling process runs on-demand, you'll only pay for that processing and you won't need to have a warehouse available 24/7.
