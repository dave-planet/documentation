## Release notes

### December 3, 2021

#### Module accessors v1.1.0

Changed
- Deployment schema "carto" instead of "accessors".
- Rename ST_ENVELOPE function to ST_ENVELOPE_ARR.

Removed
- Remove VERSION function.

#### Module constructors v1.1.0

Changed
- Deployment schema "carto" instead of "constructors".

Removed
- Remove VERSION function.

#### Module h3 v1.1.0

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

#### Module measurements v1.1.0

Changed
- Deployment schema "carto" instead of "measurements".

#Removed
- Remove ST_ANGLE, already present in Snowflake.
- Remove ST_AZIMUTH, already present in Snowflake.
- Remove VERSION function.

#### Module placekey v1.1.0

Changed
- Deployment schema "carto" instead of "placekey".
- Rename H3_ASPLACEKEY function to PLACEKEY_FROMH3.
- Rename PLACEKEY_ASH3 function to PLACEKEY_TOH3.
- Rename ISVALID function to PLACEKEY_ISVALID.

Removed
- Remove VERSION function.

#### Module processing v1.1.0

Changed
- Deployment schema "carto" instead of "processing".

Removed
- Remove VERSION function.

#### Module quadkey v1.1.0

Changed
- Deployment schema "carto" instead of "quadkey".
- Rename ZXY_FROMQUADINT function to QUADINT_TOZXY.
- Rename LONGLAT_ASQUADINT function to QUADINT_FROMLONGLAT.
- Rename QUADKEY_FROMQUADINT function to QUADINT_TOQUADKEY.
- Rename TOPARENT function to QUADINT_TOPARENT.
- Rename TOCHILDREN function to QUADINT_TOCHILDREN.
- Rename SIBLING function to QUADINT_SIBLING.
- Rename KRING function to QUADINT_KRING.
- Rename KRING_DISTANCES function to QUADINT_KRING_DISTANCES.
- Rename BBOX function to QUADINT_BBOX.
- Rename ST_ASQUADINT function to QUADINT_FROMGEOGPOINT.
- Rename ST_ASQUADINT_POLYFILL function to QUADINT_POLYFILL.
- Rename ST_BOUNDARY function to QUADINT_BOUNDARY.

Removed
- Remove VERSION function.

#### Module s2 v1.1.0

Changed
- Deployment schema "carto" instead of "s2".
- Rename ID_FROMHILBERTQUADKEY function to S2_FROMHILBERTQUADKEY.
- Rename HILBERTQUADKEY_FROMID function to S2_TOHILBERTQUADKEY.
- Rename LONGLAT_ASID function to S2_FROMLONGLAT.
- Rename ST_ASID function to S2_FROMGEOGPOINT.
- Rename ST_BOUNDARY function to S2_BOUNDARY.

Removed
- Remove VERSION function.

#### Module transformations v1.1.0

Changed
- Deployment schema "carto" instead of "transformations".

Remove
- Remove VERSION function.

#### Module clustering v1.1.0

Changed
- Deployment schema "carto" instead of "clustering".

Removed
- Remove VERSION function.

#### Module data v1.0.0-beta.4

Changed
- Deployment schema "carto" instead of "data".

Removed
- Remove VERSION function.

#### Module random v1.1.0

Changed
- Deployment schema "carto" instead of "random".

Removed
- Remove VERSION function.

### November 24, 2021

#### Module data v1.0.0-beta.3

Feature
- Add DATAOBS_ENRICH_POINTS procedure.
- Add DATAOBS_ENRICH_POINTS_RAW procedure.
- Add DATAOBS_ENRICH_POLYGON procedure.
- Add DATAOBS_ENRICH_POLYGON_RAW procedure.
- Add DATAOBS_ENRICH_GRID procedure.
- Add DATAOBS_ENRICH_GRID_RAW procedure.

### November 5, 2021

#### Module data v1.0.0-beta.2

Changes
- Fields named `dimension`, `total`, `intersection` and `input_area` are now
  `__carto_dimension`, `__carto_total` and `__carto_intersection` and `__carto_input_area`.
  Also the column `_carto_enrichment_` is now `__carto_enrichment`.
  This affects all the _raw_ enrichment procedures: `ENRICH_POINTS_RAW`, `ENRICH_POLYGONS_RAW`, `ENRICH_GRID_RAW`.

Fixed
- User provided queries can now have columns named `dimension`, `total`, `intersection`, `input_area`, `_nonglobal`, which could have collided previously with internal columns. All internal columns are now prefixed with `__carto_`. This affects all the enrichment procedures: `ENRICH_POINTS`, `ENRICH_POLYGONS`, `ENRICH_GRID`, `ENRICH_POINTS_RAW`, `ENRICH_POLYGONS_RAW`, `ENRICH_GRID_RAW`.

### November 4, 2021

#### Module data v1.0.0-beta.1

Feature
- Create data module.
- Add VERSION function.
- Add ENRICH_POINTS procedure.
- Add ENRICH_POINTS_RAW procedure.
- Add ENRICH_POLYGON procedure.
- Add ENRICH_POLYGON_RAW procedure.
- Add ENRICH_GRID procedure.
- Add ENRICH_GRID_RAW procedure.

### September 22, 2021

#### Module h3 v1.0.3

Feature
- Add KRING_DISTANCES function.

Changed
- Review HEXRING, KRING functions.

#### Module quadkey v1.0.3

Feature
- Add KRING_DISTANCES function.

Changed
- Review KRING function.

### September 14, 2021

#### Module s2 v1.0.1

Changes
- Compute ST_BOUNDARY from WKT.

### September 9, 2021

#### Module quadkey v1.0.2

Changed
- Performance improvement in ST_ASQUADINT_POLYFILL.

### August 24, 2021

#### Module h3 v1.0.2

Fixed
- Support GEOMETRYCOLLECTION from ST_ASH3_POLYFILL.

### August 11, 2021

#### Module quadkey v1.0.1

Fixed
- Support GEOMETRYCOLLECTION from ST_ASQUADINT_POLYFILL.

### June 2, 2021

#### Module h3 v1.0.1

Changed
- Reduce bundle size for every function.

### May 26, 2021

#### Module processing v1.0.0

Feature
- Create processing module.
- Add ST_VORONOIPOLYGONS function.
- Add ST_VORONOILINES function.
- Add ST_DELAUNAYPOLYGONS function.
- Add ST_DELAUNAYLINES function.
- Add ST_POLYGONIZE function.
- Add VERSION function.

### May 24, 2021

#### Module clustering v1.0.0

Feature
- Create clustering module.
- Add VERSION function.
- Add ST_CLUSTERKMEANS function.

#### Module random v1.0.0

Feature
- Create random module.
- Add ST_GENERATEPOINTS function.
- Add VERSION function.

### May 21, 2021

#### Module accessors v1.0.0

Feature
- Create accessors module.
- Add ST_ENVELOPE function.
- Add VERSION function.

### May 20, 2021

#### Module constructors v1.0.0

Feature
- Create constructors module.
- Add ST_BEZIERSPLINE function.
- Add ST_MAKEELLIPSE function.
- Add ST_MAKEENVELOPE function.
- Add ST_TILEENVELOPE function.
- Add VERSION function.

#### Module measurements v1.0.0

Feature
- Create measurements module.
- Add ST_ANGLE function.
- Add ST_AZIMUTH function.
- Add ST_MINKOWSKIDISTANCE function.
- Add VERSION function.

#### Module transformations v1.0.0

Feature
- Create transformations module.
- Add ST_CENTERMEAN function.
- Add ST_CENTERMEDIAN function.
- Add ST_CENTEROFMASS function.
- Add ST_CONCAVEHULL function.
- Add ST_DESTINATION function.
- Add ST_GREATCIRCLE function.
- Add ST_LINE_INTERPOLATE_POINT function.
- Add VERSION function.

### April 16, 2021

#### Module placekey v1.0.0

Feature
- Create placekey module.
- Add H3_ASPLACEKEY function.
- Add PLACEKEY_ASH3 function.
- Add ISVALID function.
- Add VERSION function.

### April 12, 2021

#### Module s2 v1.0.0

Feature
- Create s2 module.
- Add ID_FROMHILBERTQUADKEY function.
- Add HILBERTQUADKEY_FROMID function.
- Add LONGLAT_ASID function.
- Add ST_ASID function.
- Add ST_BOUNDARY function.
- Add VERSION function.

### April 10, 2021

#### Module random v1.1.1

Changed
- ST_GENERATEPOINTS now uses a spherically uniform distribution. Previously used to by uniform on projection.

### April 7, 2021

#### Module h3 v1.0.0

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

### March 31, 2021

#### Module quadkey v1.0.0

Feature
- Create quadkey module.
- Add QUADINT_FROMZXY function.
- Add ZXY_FROMQUADINT function.
- Add LONGLAT_ASQUADINT function.
- Add QUADINT_FROMQUADKEY function.
- Add QUADKEY_FROMQUADINT function.
- Add TOPARENT function.
- Add TOCHILDREN function.
- Add SIBLING function.
- Add KRING function.
- Add BBOX function.
- Add ST_ASQUADINT function.
- Add ST_ASQUADINT_POLYFILL function.
- Add ST_BOUNDARY function.
- Add VERSION function.
