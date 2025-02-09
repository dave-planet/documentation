---
aliases:
    - /analytics-toolbox-bq/release-notes/
---
## Release notes

### August 26, 2022

#### Module tiler

Add
- Add `generate_feature_id` parameter in `CREATE_SIMPLE_TILESET`.

### August 19, 2022

#### Module retail

Changed
- Index parameter admits any type in PREDICT_REVENUE_AVERAGE.
- Index from revenue_model_data is not casted in PREDICT_REVENUE_AVERAGE to reduce query data processing.

### August 16, 2022

#### Module tiler

Fixed
- Fixed bug when parsing zoom columns in geography tilers.

### August 11, 2022

#### Module tiler

Changed
- Unify `extra_metadata` into `metadata` in tiler metadata.

### August 9, 2022

#### Module h3

Fixed
- Apply make_valid in H3_BOUNDARY.

### August 8, 2022

#### Module tiler

Fixed
- Fixed bug in metadata `CREATE_SPATIAL_INDEX_TILESET`.

### August 5, 2022

#### Module retail

Changed
- Check fixed model options in BUILD_REVENUE_MODEL procedure.

### August 3, 2022

#### Module retail

Feature
- Add BUILD_CANNIBALIZATION_DATA procedure.
- Add CANNIBALIZATION_OVERLAP procedure.

### July 26, 2022

#### Module lds

Feature
- Add GEOCODE_TABLE procedure.
- Add LDS_QUOTA_INFO procedure.
- Add GEOCODE_REVERSE_TABLE procedure.
- Add CREATE_ISOLINES procedure.

### July 21, 2022

#### Module statistics

Changes
- Feature HH, LL, LH, HL detection in LOCAL_MORANS_I functions.

### July 20, 2022

#### Module tiler

Fixed
- Fixed bug when passing multiline input to `CREATE_SPATIAL_INDEX_TILESET`.

### July 8, 2022

#### Module data

Add
- Add quadbin support to module.

#### Module retail

Feature
- Add quadbin support

#### Module tiler

Add
- Support of quadgrid as alias in `CREATE_POINT_AGGREGATION_TILESET`.

#### Module tiler

Changed
- Use core functions to convert H3 from int to string.

### July 7, 2022

#### Module h3

Fixed
- Correctly handle large polygons in H3_POLYFILL.
- Fixed wrong uppercase for quadbin and h3 tile ids

#### Module statistics

Feature
- Add SMOOTHING_MRF_QUADBIN procedure.
- Add LOCAL_MORANS_I_QUADBIN function.
- Add MORANS_I_QUADBIN function.
- Add GETIS_ORD_QUADBIN function.
- Quadbin support in GWR_GRID function.

#### Module tiler

Fixed
- Fixed tablename quoting in BigQuery tiler

### July 6, 2022

#### Module retail

Fixed
- Fix quadkey support in FIND_WHITESPACE_AREAS

### June 29, 2022

#### Module retail

Fixed
- Fixing bugs when not providing store variables to BUILD_REVENUE_MODEL_DATA

### June 23, 2022

#### Module quadbin

Feature
- Add QUADBIN_BBOX function.
- Add QUADBIN_BOUNDARY function.
- Add QUADBIN_CENTER function.
- Add QUADBIN_FROMGEOGPOINT function.
- Add QUADBIN_FROMLONGLAT function.
- Add QUADBIN_FROMZXY function.
- Add QUADBIN_ISVALID function.
- Add QUADBIN_KRING function.
- Add QUADBIN_KRING_DISTANCES function.
- Add QUADBIN_POLYFILL function.
- Add QUADBIN_RESOLUTION function.
- Add QUADBIN_SIBLING function.
- Add QUADBIN_TOCHILDREN function.
- Add QUADBIN_TOPARENT function.
- Add QUADBIN_TOZXY function.

### June 21, 2022

#### Module data

Fixed
- Fix BQ inplace enrichment with uppercase column names.

#### Module tiler

Changed
- Support H3 integer in `CREATE_SPATIAL_INDEX_TILESET`.

### June 13, 2022

#### Module data

Fixed
- Fix order of `__KRING_DECAY` parameters.

### June 10, 2022

#### Module tiler

Fixed
- Fix global stats in `CREATE_SPATIAL_INDEX_TILESET`.

Changed
- Check input resolution limits in `CREATE_SPATIAL_INDEX_TILESET`.

### June 9, 2022

#### Module data

Fixed
- Report missing subscription geographies in DATAOBS_ENRICH_ procedures.

### June 6, 2022

#### Module data

Fixed
- Fix stability issues in GRIDIFY_ENRICH procedure.

### June 3, 2022

#### Module retail

Feature
- Add store features and competitors stores features into BUILD_REVENUE_MODEL_DATA procedure.

Fixed
- Fixing bugs calling other routines

### June 2, 2022

#### Module tiler

Feature
- Add spatial index tileset generator `CREATE_SPATIAL_INDEX_TILESET`.

### May 16, 2022

#### Module tiler

- Bug fixing when the geometry early collapse

### April 27, 2022

#### Module data

Feature
- Add GRIDIFY_ENRICH procedure.

#### Module retail

Feature
- Add FIND_TWIN_AREAS procedure.

### April 22, 2022

#### Module data

Feature
- Allow using tables as input, not just queries.
- Add in place enrichment.
- Allow using tables as input.
- Accept NULL as output.

### April 20, 2022

#### Module retail

Fixed
- Fix BUILD_REVENUE_MODEL_DATA k-ring buffer computation.

### March 21, 2022

#### Module transformations

Changed
- ST_CONCAVEHULL now allows arrays with one/two points as input.

#### Module retail

Feature
- Add COMMERCIAL_HOTSPOTS procedure.

#### Module statistics

Feature
- Add SMOOTHING_MRF_H3 procedure.
- Add SMOOTHING_MRF_QUADKEY procedure.

### February 16, 2022

#### Module statistics

Feature
- Add VARIOGRAM function.
- Add ORDINARY_KRIGING function.
- Add ORDINARY_KRIGING_TABLE procedure.

### February 15, 2022

#### Module h3

Feature
- Add H3_CENTER function.
- Add H3_RESOLUTION function.

#### Module retail

Feature
- Add FIND_WHITESPACE_AREAS procedure.

### February 3, 2022

#### Module retail

Feature
- Remove features importance tables from BUILD_REVENUE_MODEL procedure.

### February 1, 2022

#### Module statistics

Feature
- Add LOCAL_MORANS_I_H3 function.
- Add LOCAL_MORANS_I_QUADKEY function.

Changed
- Improve MORANS_I_H3 and MORANS_I_QUADKEY implementation.

### January 10, 2022

#### Module statistics

Fixed
- Replace STDDEV by STDDEV_POP in GETIS_ORD_H3 and GETIS_ORD_QUADKEY.

### December 22, 2021

#### Module retail

Feature
- Add BUILD_REVENUE_MODEL_DATA procedure.
- Add BUILD_REVENUE_MODEL procedure.
- Add PREDICT_REVENUE_AVERAGE procedure.

### December 16, 2021

#### Module accessors

Changed
- Deployment schema "carto" instead of "accessors".

Removed
- Remove VERSION function.

#### Module constructors

Changed
- Deployment schema "carto" instead of "constructors".

Removed
- Remove VERSION function.

#### Module geohash

Changed
- Deployment schema "carto" instead of "geohash".

Removed
- Remove VERSION function.

#### Module h3

Changed
- Deployment schema "carto" instead of "h3".
- Rename ST_ASH3 function to H3_FROMGEOGPOINT.
- Rename LONGLAT_ASH3 function to H3_FROMLONGLAT.
- Rename ST_ASH3_POLYFILL function to H3_POLYFILL.
- Rename ST_BOUNDARY function to H3_BOUNDARY.
- Rename ISVALID function to H3_ISVALID.
- Rename COMPACT function to H3_COMPACT.
- Rename UNCOMPACT function to H3_UNCOMPACT.
- Rename TOPARENT function to H3_TOPARENT.
- Rename TOCHILDREN function to H3_TOCHILDREN.
- Rename ISPENTAGON function to H3_ISPENTAGON.
- Rename DISTANCE function to H3_DISTANCE.
- Rename KRING function to H3_KRING.
- Rename KRING_DISTANCES function to H3_KRING_DISTANCES.
- Rename HEXRING function to H3_HEXRING.

Removed
- Remove VERSION function.

#### Module measurements

Changed
- Deployment schema "carto" instead of "measurements".

#Removed
- Remove ST_ANGLE, already present in Bigquery.
- Remove VERSION function.

#### Module placekey

Changed
- Deployment schema "carto" instead of "placekey".
- Rename H3_ASPLACEKEY function to PLACEKEY_FROMH3.
- Rename PLACEKEY_ASH3 function to PLACEKEY_TOH3.
- Rename ISVALID function to PLACEKEY_ISVALID.

Removed
- Remove VERSION function.

#### Module processing

Changed
- Deployment schema "carto" instead of "processing".

Removed
- Remove VERSION function.

#### Module s2

Changed
- Deployment schema "carto" instead of "s2".
- Rename ID_FROMHILBERTQUADKEY function to S2_FROMHILBERTQUADKEY.
- Rename HILBERTQUADKEY_FROMID function to S2_TOHILBERTQUADKEY.
- Rename LONGLAT_ASID function to S2_FROMLONGLAT.
- Rename ST_ASID function to S2_FROMGEOGPOINT.
- Rename ID_FROMTOKEN function to S2_FROMTOKEN.
- Rename TOKEN_FROMID function to S2_TOTOKEN.
- Rename ID_FROMUINT64REPR function to S2_FROMUINT64REPR.
- Rename UINT64REPR_FROMID function to S2_TOUINT64REPR.
- Rename ST_BOUNDARY function to S2_BOUNDARY.

Removed
- Remove VERSION function.

#### Module transformations

Changed
- Deployment schema "carto" instead of "transformations".

Remove
- Remove VERSION function.

#### Module clustering

Changed
- Deployment schema "carto" instead of "clustering".

Removed
- Remove VERSION function.

#### Module data

Changed
- Deployment schema "carto" instead of "data".

Removed
- Remove VERSION function.

#### Module random

Changed
- Deployment schema "carto" instead of "random".

Removed
- Remove VERSION function.

#### Module routing

Changed
- Deployment schema "carto" instead of "routing".

Removed
- Remove VERSION function.

#### Module statistics

Changed
- Deployment schema "carto" instead of "statistics".

Removed
- Remove VERSION function.

#### Module tiler

Changed
- Deployment schema "carto" instead of "tiler".

Removed
- Remove VERSION function.

### December 13, 2021

#### Module tiler

Changed
- Add support for legacy project names that contain dots or other special characters.

### December 10, 2021

#### Module statistics

Feature
- Add KNN function.
- Add GFUN function.
- Add LOF function.
- Add LOF_TABLE procedure.

### November 30, 2021

#### Module tiler

Fixed
- Escape single-quoted properties in the `CREATE_TILESET` metadata when obtaining the geometry type.

### November 25, 2021

#### Module statistics

Feature
- Add GWR_GRID function.

### November 16, 2021

#### Module tiler

Fixed
- Use `zoom_min_column` as `zoom_min` and `zoom_max_column` as `zoom_max` when provided.

Changed
- Optimize simplification method instead of the native BigQuery.

### November 5, 2021

#### Module data

Changes
- Fields named `dimension`, `total`, `intersection` and `input_area` are now
  `__carto_dimension`, `__carto_total` and `__carto_intersection` and `__carto_input_area`.
  Also the column `_carto_enrichment_` is now `__carto_enrichment`.
  This affects all the _raw_ enrichment procedures: `ENRICH_POINTS_RAW`, `ENRICH_POLYGONS_RAW`, `ENRICH_GRID_RAW`, `DATAOBS_ENRICH_POINTS_RAW`, `DATAOBS_ENRICH_POLYGONS_RAW`, `DATAOBS_ENRICH_GRID_RAW`.

Fixed
- User provided queries can now have columns named `dimension`, `total`, `intersection`, `input_area`, `_nonglobal`, which could have collided previously with internal columns. All internal columns are now prefixed with `__carto_`. This affects all the enrichment procedures: `ENRICH_POINTS`, `ENRICH_POLYGONS`, `ENRICH_GRID`, `DATAOBS_ENRICH_POINTS`, `DATAOBS_ENRICH_POLYGONS`, `DATAOBS_ENRICH_GRID`, `ENRICH_POINTS_RAW`, `ENRICH_POLYGONS_RAW`, `ENRICH_GRID_RAW`, `DATAOBS_ENRICH_POINTS_RAW`, `DATAOBS_ENRICH_POLYGONS_RAW`, `DATAOBS_ENRICH_GRID_RAW`.

### November 2, 2021

#### Module data

Changes
- Add `associated_geography_slug` column to `DATAOBS_SUBSCRIPTIONS`.
- Some column names have changed in `DATAOBS_SUBSCRIPTIONS`:
  + `table` is now `dataset_table`
  + `associated_geography` is now `associated_geography_table`
- Some column names have changed in `DATAOBS_SUBSCRIPTION_VARIABLES`:
  + `geography_slug` is now `associated_geography_slug`.
- Some column names have changed in `DATAOBS_SAMPLES`:
  + `table` is now `dataset_sample_table`.
- In `DATAOBS_SUBSCRIPTION_VARIABLES`, the column `associated_geography_slug` is now NULL for geography datasets.

Fixed
- The output of `DATAOBS_SUBSCRIPTIONS` and `DATAOBS_SUBSCRIPTION_VARIABLES` now omits items that are not Data Observatory products.

### October 15, 2021

#### Module data

Fixed
- Enrichment results could mix input rows and values, specially for large inputs due
  to multiple evaluation of nondeterministic ROW_NUMBERS expression.

Changes
- New API, with consistent naming of procedures `

### September 23, 2021

#### Module s2

Changed
- Rename functions ID_FROMUINT64REPR, UINT64REPR_FROMID to follow convention.

#### Module statistics

Feature
- Create statistics module.
- Add GETIS_ORD_H3 function.
- Add GETIS_ORD_QUADKEY function.
- Add MORANS_I_H3 function.
- Add MORANS_I_QUADKEY function.
- Add VERSION function.

### September 22, 2021

#### Module h3

Changed
- Review HEXRING, KRING functions.
- Change KRING_INDEXED to KRING_DISTANCES.

### September 17, 2021

#### Module tiler

Fixed
- Fix support for DATE in `CREATE_TILESET`.
- Fix naming of internal variables to avoid name collisions.

Feature
- Add `fraction_dropped_per_zoom` in tileset metadata.

### September 16, 2021

#### Module data

Changes
- Support `sub_` (table) subscriptions in:
  - DATAOBS_ENRICH_POINTS
  - DATAOBS_ENRICH_POINTS_WITH_MEASURES
  - DATAOBS_ENRICH_POLYGONS_WITH_AGGREGATION
  - DATAOBS_ENRICH_POLYGONS_WITH_MEASURES
  - DATAOBS_ENRICH_GRID

### September 14, 2021

#### Module s2

Fixed
- Avoid keeping planar shape in spherical coordinates in ST_BOUNDARY.

### September 3, 2021

#### Module data

Changes
- Search for tables in DATAOBS_SAMPLES, DATAOBS_SUBSCRIPTIONS, DATAOBS_SUBSCRIPTIONS_VARIABLES.

### August 31, 2021

#### Module data

Changed
- DATAOBS_ENRICH_* procedures are now optimized to reduce the amount of data processed by taking advantage of clusterization by geography in the Data Observatory.
- The `input_id_column` parameter has been removed from the following procedures:
  - DATAOBS_ENRICH_POINTS
  - DATAOBS_ENRICH_POINTS_WITH_MEASURES
  - DATAOBS_ENRICH_POLYGONS_WITH_AGGREGATION
  - DATAOBS_ENRICH_POLYGONS_WITH_MEASURES
  - ENRICH_POINTS
  - ENRICH_POINTS_WITH_MEASURES
  - ENRICH_POLYGONS_WITH_AGGREGATION
  - ENRICH_POLYGONS_WITH_MEASURES

### August 26, 2021

#### Module data

Changed
- ENRICH_GRID and DATAOBS_ENRICH_GRID procedures take `input_query` and `input_index_column` parameters instead of the `indices` array.
- DATAOBS_ENRICH_* procedures now report missing subscriptions in a more user-friendly way.

#### Module routing

Changed
- Pass network to JS UDF natively
- Support custom speed over LineStrings for GENERATE_NETWORK function.
- Support custom speed over LineStrings for FIND_SHORTEST_PATH function.
- Support custom speed over LineStrings for DISTANCE_MAP function.

### August 25, 2021

#### Module tiler

Fixed
- Fix support for TIMESTAMP,DATETIME in CREATE_TILESET and CREATE_SIMPLE_TILESET.
- Reduce parallelization to skip the recent error: "Not enough resources for query planning - too many subqueries or query is too complex"

### August 24, 2021

#### Module h3

Fixed
- Support GEOMETRYCOLLECTION from ST_ASH3_POLYFILL.

### August 6, 2021

#### Module data

Feature
- Add DATAOBS_ENRICH_GRID procedure.
- Add ENRICH_GRID procedure.

### August 4, 2021

#### Module h3

Feature
- Add KRING_INDEXED function.

### July 30, 2021

#### Module geohash

Feature
- Create geohash module.
- Add VERSION function.
- Add ST_BOUNDARY function.

#### Module tiler

Changed
- Checking if the output table exists before running the tiler.

### July 13, 2021

#### Module data

Changed
- DATAOBS_ENRICH_* procedures take single `source` parameter with default `carto-customers` project.

### July 9, 2021

#### Module data

Feature
- Add DATAOBS_SAMPLES procedure.

Changed
- DATAOBS_SUBSCRIPTIONS and DATAOBS_SUBSCRIPTION_VARIABLES take single `source` parameter with default `carto-customers` project. Views with `sub_` prefix are supported.

#### Module routing

Feature
- Create routing module.
- Add GENERATE_NETWORK function.
- Add GENERATE_NETWORK_TABLE procedure.
- Add FIND_SHORTEST_PATH function.
- Add FIND_SHORTEST_PATH_FROM_NETWORK function.
- Add FIND_SHORTEST_PATH_FROM_NETWORK_TABLE procedure.
- Add DISTANCE_MAP function.
- Add DISTANCE_MAP_FROM_NETWORK function.
- Add DISTANCE_MAP_FROM_NETWORK_TABLE procedure.
- Add VERSION function.

### July 8, 2021

#### Module data

Fixed
- Fix DATAOBS_SUBSCRIPTIONS and DATAOBS_SUBSCRIPTION_VARIABLES not working with subscriptions in which the
  provider id contained underscores.

### July 1, 2021

#### Module tiler

Feature
- Add new automatic tileset generator `CREATE_TILESET`.

### June 23, 2021

#### Module data

Feature
- Add DATAOBS_SUBSCRIPTIONS procedure.
- Add DATAOBS_SUBSCRIPTION_VARIABLES procedure.

Changed
- Change spatial catalog structure using two tables.
- Improve enrichment procedures:
  - Use public geographies instead of subscription views
  - Remove unnecessary variables from ENRICH_POLYGONS_WITH_MEASURES
  - Make input_id_column always mandatory
  - Add input_area consistently

### June 2, 2021

#### Module data

Feature
- Create data module.
- Add VERSION function.
- Add DATAOBS_ENRICH_POINTS procedure.
- Add DATAOBS_ENRICH_POINTS_WITH_MEASURES procedure.
- Add DATAOBS_ENRICH_POLYGONS_WITH_AGGREGATION procedure.
- Add DATAOBS_ENRICH_POLYGONS_WITH_MEASURES procedure.
- Add ENRICH_POINTS procedure.
- Add ENRICH_POINTS_WITH_MEASURES procedure.
- Add ENRICH_POLYGONS_WITH_AGGREGATION procedure.
- Add ENRICH_POLYGONS_WITH_MEASURES procedure.

### June 1, 2021

#### Module s2

Feature
- Add TOKEN_FROMID function.
- Add ID_FROMTOKEN function.
- Add ID_FROM_UINT64REPR function.
- Add UINT64REPR_FROM_ID function.

### May 19, 2021

#### Module tiler

Changed
- Use semantic versioning.
- Add `features_count` and `geometry` labels to the tilesets.

### May 6, 2021

#### Module clustering

Changed
- Change ST_CLUSTERKMEANS returning cluster and geom

### May 4, 2021

#### Module accessors

Feature
- Create accessors module.
- Add ST_ENVELOPE function.
- Add VERSION function.

#### Module processing

Feature
- Create processing module.
- Add ST_VORONOIPOLYGONS function.
- Add ST_VORONOILINES function.
- Add ST_DELAUNAYPOLYGONS function.
- Add ST_DELAUNAYLINES function.
- Add ST_POLYGONIZE function.
- Add VERSION function.

#### Module transformations

Feature
- Add ST_CONCAVEHULL function.

### April 30, 2021

#### Module clustering

Feature
- Create clustering module.
- Add ST_CLUSTERKMEANS function.
- Add VERSION function.

### April 29, 2021

#### Module constructors

Feature
- Add ST_BEZIERSPLINE function.
- Add ST_MAKEELLIPSE function.

#### Module measurements

Feature
- Create measurements module.
- Add ST_ANGLE function.
- Add ST_AZIMUTH function.
- Add ST_MINKOWSKIDISTANCE function.

#### Module transformations

Feature
- Rename module to transformations.
- Add ST_CENTERMEAN function.
- Add ST_CENTERMEDIAN function.
- Add ST_CENTEROFMASS function.
- Add ST_DESTINATION function.
- Add ST_GREATCIRCLE function.
- Add ST_LINE_INTERPOLATE_POINT function.

#### Module tiler

Removed
- Remove quota & project checking.

### April 28, 2021

#### Module constructors

Feature
- Create constructors module.
- Add ST_MAKEENVELOPE function.
- Add ST_TILEENVELOPE function.
- Add VERSION function.

### April 16, 2021

#### Module transformations

Feature
- Create transformation module.
- Add ST_BUFFER function.
- Add VERSION function.

### April 10, 2021

#### Module random

Changed
- ST_GENERATEPOINTS now uses a spherically uniform distribution. Previously used to by uniform on projection.

### April 9, 2021

#### Module h3

Changed
- Use hexadecimal as default type instead of int for h3 indexes.

Fixed
- Fix ST_BOUNDARY generating error when not able to parse geometry.

#### Module placekey

Changed
- Placekey conversions works with hexadecimal h3 indexes instead of int.

#### Module random

Feature
- Create random module.
- Add ST_GENERATEPOINTS function.
- Add VERSION function.

### March 31, 2021

#### Module h3

Feature
- Create h3 module.
- Add ST_ASH3 function.
- Add LONGLAT_ASH3 function.
- Add ST_ASH3_POLYFILL function.
- Add ST_BOUNDARY function.
- Add ISVALID function.
- Add COMPACT function.
- Add UNCOMPACT function.
- Add TOPARENT function.
- Add TOCHILDREN function.
- Add ISPENTAGON function.
- Add DISTANCE function.
- Add KRING function.
- Add HEXRING function.
- Add VERSION function.

#### Module placekey

Feature
- Create placekey module.
- Add H3_ASPLACEKEY function.
- Add PLACEKEY_ASH3 function.
- Add ISVALID function.
- Add VERSION function.

#### Module s2

Feature
- Create s2 module.
- Add ID_FROMHILBERTQUADKEY function.
- Add HILBERTQUADKEY_FROMID function.
- Add LONGLAT_ASID function.
- Add ST_ASID function.
- Add ST_BOUNDARY function.
- Add VERSION function.

#### Module tiler

Feature
- Add QUOTA procedure in order to display the monthly quota and quota available.
- Implement support for layer name.
- Add a max limit to the `max_tile_size_kb` property. Adds a new option (`skip_validation`) to circunvent this limit, which also allows going over the max partition limit.
- Add a limit to the max amount of **expected** tiles at the highest zoom level for Simple Tilesets. It can be disabled via the `skip_validation` option of modified (for tests using `max_tiles_at_maxzoom`).
- Add new `drop_fraction_as_needed` strategy initial implementation. Also adds **internal** `debug` and `fraction_drop_per_zoom_level` options to help debugging.
- Add new `metadada` input parameter to set the properties `name`, `description`, `legends` and also `extra_metadata`.
- Add `zoom_min_column` and `zoom_max_column` to control the zoom level at which particular features are visible.

Changed
- Change the default and max partition limit to 3999.
- Make aggregation tilesets to use the quadkey module UDF LONGLAT_ASQUADINTLIST_RESOLUTION in order to generate quadkey aggregations.

Removed
- Removed `zoom_step` option.

Fixed
- Fix bug that left empty the generator options in the metadata cell.
- Fix CREATE_SIMPLE_TILESET failing with single column tables.
- Fix collision with `frequency` column name.

### February 10, 2021

#### Module tiler

Feature
- Add tileset type to metadata and BigQuery labels.
- Add the prefix "aggregation_" to aggregation options: type, resolution and placement.

Changed
- Moved to the Advanced Spatial Extension.
- Change "max_tile_size_strategy" default to "throw_error", matching the other defaults and improve the exception error message in CreatePointAggregationTileset.
- Rename adapting to BigQuery conventions, using UPPER CASE and separating words with underscore "_".
- Set up limits for the procedures based on a limits table in the config project. The users can only execute the tiler from the "billing_project" and they have a maximum amount of processed bytes per month.

Removed
- Remove compression levels 10-12 to reduce library size.
- Remove ST prefix from functions not using geographies.
- Remove unused functions like st_tileenvelope or st_tileenvelope_bbox.



{{% euFlagFunding %}}