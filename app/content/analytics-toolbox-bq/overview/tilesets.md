## Tilesets

CARTO BigQuery Tiler is a module of the Analytics Toolbox for BigQuery that allows to process and visualize very large spatial datasets stored in BigQuery.

If you have small datasets in BigQuery (few megabytes), there are solutions such as [BigQuery Geo Viz](https://cloud.google.com/bigquery/docs/gis-visualize) to visualize them; but if you have millions or even billions of rows, you will need a system to load them progressively on a map. CARTO BigQuery Tiler allows you to do that without having to move your data out of BigQuery. 

### How it works

The Tiler will process your data and create a complete tileset out of it. All the map tiles for the specified zoom range will be stored in a BigQuery table in [MVT format](https://docs.mapbox.com/vector-tiles/specification/). Each individual tile is a row in this table, with the tile coordinates and the encoded MVT stored in different columns:

| Row | z | x | y | carto_partition | data |
|-----|---|---|---|-----------------|------|
| 1   | 16 | 45340 | 24576 | 3605 | H4sIAAAAAAAA/5Py52JPdt3eyCLEwM (...) |
| 2   | 16 | 45292 | 24576 | 3605 | H4sIAAAAAAAA/5Py52JjLM0pEZLgWL (...) |

Visualizing and publishing your tilesets is straight-forward using [Builder](/carto-user-manual/maps/introduction/), the map making tool integrated into the CARTO Workspace. Learn how to create, visualize and share your first tileset by following the [Tilesets guides](../../guides/creating-and-visualizing-tilesets).

The integration of tilesets with custom web map applications is also possible with CARTO Maps API, which will connect to BigQuery using your connection's Service Account credentials to fetch and serve the tiles in a standard format, so they can be used with any web-mapping library or desktop GIS application.



### Tileset types and procedures

CARTO BigQuery Tiler enables the creation of two types of tilesets through [stored procedures](https://cloud.google.com/bigquery/docs/reference/standard-sql/scripting): *simple* and *aggregation* tilesets. _Simple_ tilesets encode all the input features as is, while _aggregation_ tilesets encode aggregations over the input features. Therefore, you should use _simple_ tilesets for visualizing a dataset of world rivers, but use an _aggregation_ tileset to visualize a heatmap of the trees distribution in New York City. 

We provide the following set of procedures to create tilesets:

1. `tiler.CREATE_TILESET`
    * This procedure creates a _simple_ tileset. You should use it if you have a dataset with any geography type (point, line, or polygon) and you want to visualize it at an appropriate zoom level.
    * The geographies will be represented exactly as stored in BigQuery, which means that if they are too small to be visible at a certain zoom level they won't be included in the tiles at that zoom level.
    * The values associated with each feature are the same as the ones available in the source dataset.

2. `tiler.CREATE_SIMPLE_TILESET`
    * This procedure is the older version of `tiler.CREATE_TILESET` and you can achieve exactly the same results with either of these procedures. However, `tiler.CREATE_TILESET` is capable of finding the right configuration for your input data, whereas this procedure requires you to set them yourself. 
    * Please use this procedure _only_ if you need a really specific configuration for your tileset or need to tweak a particular option that it's not available in `tiler.CREATE_TILESET`.

3. `tiler.CREATE_POINT_AGGREGATION_TILESET`
    * Use this procedure if you have a point dataset (or anything that can be converted to points, such as polygon centroids) and you want to see it aggregated.
    * The points will be aggregated into cells. Each feature or cell represents all the points that fall under it, so the associated properties available for visualization are generated by aggregating the values in the source dataset.
    * Values of individual points are available using `single_point_properties` which will only be included when a cell includes only one point. Remember that you could also get similar values with the aggregated properties using functions like `ANY_VALUE` or `FIRST_VALUE`.

Take a look at the examples for creating [simple](../../examples/creating-simple-tilesets/) and [aggregation](../../examples/creating-aggregation-tilesets/) tilesets and the complete [reference](../../sql-reference/tiler) if you need help with the SQL query specifics. You can also create simple tilesets through the Data Explorer integrated in the CARTO Workspace, please visit [this page](/analytics-toolbox-bq/guides/creating-and-visualizing-tilesets/#from-the-carto-workspace) to learn more.

### Benefits

CARTO BigQuery Tilers is:

* **Convenient** -- It can be run directly as SQL commands in BigQuery. The data never leaves BigQuery so you won't have to worry about security and additional ETLs.
* **Fast** -- CARTO BigQuery Tiler benefits from the massive scalability capabilities of BigQuery and can process hundreds of millions of rows in a few minutes.
* **Scalable** -- This solution works well for 1M points or 100B points.
* **Cost-effective** -- Since BigQuery separates storage from computing, the actual cost of hosting these tilesets is very low. Additionally, since the tiling process runs on-demand, you'll only pay for that processing and you won't need to have a cluster available 24/7. Finally, we have optimized how we serve the tiles, thanks to our partitioning algorithms.