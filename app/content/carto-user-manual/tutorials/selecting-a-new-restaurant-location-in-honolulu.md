---
title: "Selecting a new restaurant location in Honolulu"
description: "We find the best new location for a specific target demographics using spatial indexes and advanced statistical functions."
image: "/img/tutorials/pizza-hut-location-in-honolulu.png"
type: tutorials
date: "2022-05-02"
# categories:
#     - hard
#     - h3
#     - statistics
#     - retail
---

## Selecting a new restaurant location in Honolulu

**Context**

Identifying an optimal location for a new store is not always an easy task, and we often do not have enough data at our disposal to build a solid model to predict potential revenues across an entire territory. In these cases, managers rely on different business criteria in order to make a sound decision for their expansion strategy. For example, they rely on defining their target market and segmenting population groups accordingly in order to locate the store closer to where the target market lives (e.g. areas with a great presence of youngsters).

In this tutorial, we are going to use CARTO's Analytics Toolbox for BigQuery to explore good locations to open a new restaurant in Honolulu, Hawaii. For that, we will perform two different spatial analyses based on spatial indices (H3): [Commercial Hotspots](/analytics-toolbox-bigquery/sql-reference/retail/#commercial_hotspots) and [Local Outlier Factor](/analytics-toolbox-bigquery/sql-reference/statistics/#lof).

In-depth content and more technical information regarding the exercise found at [Opening a new Pizza Hut location in Honolulu](/analytics-toolbox-bigquery/examples/opening-a-new-pizza-hut-location-in-honolulu)

**Steps to reproduce**

1. Go to the new CARTO platform access page: https://app.carto.com 

   ![Log in Email and password](/img/cloud-native-workspace/get-started/login.png)

2. Create a new CARTO organization. Check this [guide](../../overview/getting-started/) to get started.

3. The first time that you access the Workspace, you will see a Welcome banner with links providing quick access to different actions to get you started with CARTO, like creating your first connection or your first map. 

    <!-- ![Welcome banner Homepage first landing](/img/cloud-native-workspace/get-started/homepage_first_landing.png) -->

    ![Welcome banner Homepage first new landing](/img/cloud-native-workspace/get-started/homepage_first_new_landing.png)

4. From the Navigation Menu in the left panel, select Maps. On the top-right corner, select "New map". This should take you to a new instance of a Builder map:   

    ![Map new map instance](/img/cloud-native-workspace/tutorials/tutorial13_map_new_map_instance.png)

5. We will define the overall Area of study by running an SQL query. Select the "Add source from..." at the bottom left of the page. Select the tab named "Custom Query (SQL)", and click on the "CARTO Data Warehouse" connection: 

   ![Map select new source custom query](/img/cloud-native-workspace/tutorials/tutorial13_map_custom_query.png)

6. We will write a custom SQL query, therefore select the "Type your own query" option and click on "Add source" on the bottom right. This should open the SQL Editor:

   ![Map new map sql editor](/img/cloud-native-workspace/tutorials/tutorial13_map_new_sql_editor.png)

7. First we define the area of study by creating a buffer of 5km around Honolulu downtown. Run the query below:

    ```sql
    SELECT ST_BUFFER(ST_GEOGPOINT(-157.852587, 21.304390), 5000);
    ```
    Rename the layer to "Area of Study", and style the buffer according to the config seen below

   ![Map define buffer](/img/cloud-native-workspace/tutorials/tutorial13_map_area_of_study_buffer.png)

8. We then extract our current store assets and display on the map. In this example, we will extract Pizza Hut stores from a sample dataset including points of interest in Honolulu (subset of [OpenStreetMaps's Planet Nodes dataset](https://carto.com/spatial-data-catalog/browser/dataset/osm_nodes_74461e34/)). Add a new custom query, as we did in the buffer example, and introduce the query below:

   ```sql
    DECLARE honolulu_buffer GEOGRAPHY;
    -- We use the ST_BUFFER to define a 5 km buffer centered in Honolulu
    SET honolulu_buffer = ST_BUFFER(ST_GEOGPOINT(-157.852587, 21.304390), 5000);
 
    SELECT
    tag.value AS brand, geometry,
    FROM
    `cartobq.docs.honolulu_planet_nodes` d,
    UNNEST(all_tags) as tag
    WHERE ST_CONTAINS(honolulu_buffer, geometry)
    AND ((tag.value in ("Pizza Hut") AND tag.key = 'brand'))
    ```

    Rename the layer to "Own stores", and style the buffer according to the config seen below

   ![Map import own stores](/img/cloud-native-workspace/tutorials/tutorial13_map_import_own_stores.png)

9.  Next we will subdivide the area of study into H3 grid cells of resolution 10 using the query below:

    ```sql
    DECLARE honolulu_buffer GEOGRAPHY;
    -- We use the ST_BUFFER to define a 5 km buffer centered in Honolulu
    SET honolulu_buffer = ST_BUFFER(ST_GEOGPOINT(-157.852587, 21.304390), 5000);
 
    CREATE TABLE `cartobq.docs.honolulu_pizza_aos` AS (
        SELECT h3id
        FROM UNNEST(`carto-un`.carto.H3_POLYFILL(honolulu_buffer, 10)) h3id
    )
    ```
    We have already created the table for you, named `cartobq.docs.honolulu_pizza_aos`. You only need to add a new custom query, and run the query below:

    ```sql
    SELECT * FROM cartobq.docs.honolulu_pizza_aos
    ````

    Rename the layer "Polyfill area of study" and reorder the layer to place as the bottom layer.

    ![Map polyfill area of study](/img/cloud-native-workspace/tutorials/tutorial13_map_polyfill_area_of_study.png)

    Hide the layer we have just created by clicking on the "eye" icon next to the 3 dots of each layer.

10. We will then enrich the H3 grid with population variables, with the aim of looking for areas with a high density of males and females between 15 and 34 years old. For more detailed analysis of how we do that you can refer to [here](/analytics-toolbox-bigquery/examples/opening-a-new-pizza-hut-location-in-honolulu), under the heading "Enrich area of study".

    We have already created the table for you, named `cartobq.docs.honolulu_pizza_aos_enriched`. You only need to add a new custom query, and run the query below:

    ```sql
    SELECT * FROM cartobq.docs.honolulu_pizza_aos_enriched
    ```

    Rename the layer "Demographics enrichment" and reorder the layer to place as the bottom layer. Hover over a hexagon to see that there is data on population of age groups.

    Hide the layer we have just created by clicking on the "eye" icon next to the 3 dots of each layer.

    ![Map area of study demographics enrichment](/img/cloud-native-workspace/tutorials/tutorial13_map_area_of_study_demographics_enrichment.png)

11. Next, we aggregate all the population results (demographics per hexagon) and store into a single column.

    ```sql
    DECLARE features ARRAY<STRING>;
    DECLARE query STRING;
 
    -- We get the names of all columns in the enriched table except for ('h3id')
    SET features =
    (
        SELECT ARRAY_AGG(column_name)
        FROM `cartobq.docs`.INFORMATION_SCHEMA.COLUMNS
        WHERE table_name = 'honolulu_pizza_aos_enriched' AND NOT column_name IN ('h3id')
    );
 
    SET query =
    """ CREATE TABLE `cartobq.docs.honolulu_pizza_aos_enriched_sum` AS (SELECT h3id, """
    || ARRAY_TO_STRING(features, " + ")  ||
    """ AS sum_pop FROM `cartobq.docs.honolulu_pizza_aos_enriched`)""";
 
    -- We execute such query
    EXECUTE IMMEDIATE query;
    ```

    We have already created the table for you, named `cartobq.docs.honolulu_pizza_aos_enriched_sum`. You only need to add a new custom query, and run the query below:

    ```sql
    SELECT * FROM cartobq.docs.honolulu_pizza_aos_enriched_sum
    ```

    Rename the layer "Aggregated population" and reorder the layer to place as the bottom layer. Hover over a hexagon to see that there is now only one population value per hexagon (all the males and females 15 to 34).

    ![Map area of studyaggregated population](/img/cloud-native-workspace/tutorials/tutorial13_map_area_of_study_aggregated_population.png)

    Hide the layer we have just created by clicking on the "eye" icon next to the 3 dots of each layer.

12. In addition to target population, we also want to consider the distance to the closest own store, in order to avoid cannibalization. To do this we calculate the distance of each hexagon to each store, and keep the minimum.

    ```sql
    DECLARE honolulu_buffer GEOGRAPHY;
    SET honolulu_buffer = ST_BUFFER(ST_GEOGPOINT(-157.852587, 21.304390), 5000);
 
    CREATE TABLE `cartobq.docs.honolulu_pizza_aos_enriched_sum_wdist` AS
    (
    WITH t1 AS (
        SELECT `carto-un`.carto.H3_FROMGEOGPOINT(geometry, 10) as h3id,
        FROM `cartobq.docs.honolulu_planet_nodes` d,
        UNNEST(all_tags) as tag
        WHERE ST_CONTAINS(honolulu_buffer, geometry)
        AND ((tag.value in ("Pizza Hut") AND tag.key = 'brand'))
    ),
 
    t2 AS (
        SELECT * FROM `cartobq.docs.honolulu_pizza_aos_enriched_sum`
    )
 
    SELECT t2.h3id, ANY_VALUE(t2.sum_pop) AS sum_pop, MIN(`carto-un`.carto.H3_DISTANCE(t2.h3id, t1.h3id)) AS dist
    FROM t1
    CROSS JOIN t2
    WHERE sum_pop IS NOT NULL
    GROUP BY t2.h3id
    );
    ```

    We have already created the table for you, named `cartobq.docs.honolulu_pizza_aos_enriched_sum_wdist`. You only need to add a new custom query, and run the query below:

    ```sql
    SELECT * FROM cartobq.docs.honolulu_pizza_aos_enriched_sum_wdist
    ```

    Rename the layer "Demographics and distance to closest store" and reorder the layer to place below "Own stores" and "Area of study". Hover over a hexagon to see that there is now one population value and distance value per hexagon (population between 15 and 34, and distance to closest own store).

    Style the hexagons according to the config seen below, applying a gradient palette to represent with darker colour the areas with the lowest population. 

    ![Map area of study demographics distance to store](/img/cloud-native-workspace/tutorials/tutorial13_map_area_of_study_demographics_distance.png)

13. Next we will use the [COMMERCIAL_HOTSPOTS](/analytics-toolbox-bigquery/sql-reference/retail/#commercial_hotspots) method to identify locations with large populations aged 15-34 and far from existing own restaurants. This functionality identifies areas with values that are significantly higher than the average.

    ```sql
        CALL `carto-un`.carto.COMMERCIAL_HOTSPOTS(
            'cartobq.docs.honolulu_pizza_aos_enriched_sum_wdist',
            NULL,
            'h3id',
            'h3',
            ['sum_pop','dist'],
            [0.7, 0.3],
            2,
            0.01
        )
    ```
    We have already created the table for you, named `cartobq.docs.honolulu_pizza_hotspots`. You only need to add a new custom query, and run the query below:

    ```sql
    SELECT ST_UNION_AGG(`carto-un`.carto.H3_BOUNDARY(index)) FROM `cartobq.docs.honolulu_pizza_hotspots`
    ```
    Rename the layer "Proposed locations" and reorder the layer to place below "Own stores" and "Area of study". 

    Style the boundary according to the config seen below.

    ![Map proposed locations](/img/cloud-native-workspace/tutorials/tutorial13_map_proposed_locations.png)

14. Finally, we are going to extract competitors from the `cartobq.docs.honolulu_planet_nodes` table and compute the local outlier factor (using the [LOF](/analytics-toolbox-bigquery/sql-reference/statistics/#lof) function) to identify those that are very close to one another and those far from the others.

    ```sql
    DECLARE honolulu_buffer GEOGRAPHY;
    SET honolulu_buffer = ST_BUFFER(ST_GEOGPOINT(-157.852587, 21.304390), 5000);
 
    -- We get all amenities tagged as restaurants or fast_food POIS in Honolulu
    WITH fast_food AS (
        SELECT CAST(id AS STRING) AS id , tag.value, geometry as geom
        FROM `cartobq.docs.honolulu_planet_nodes` d,
        UNNEST(all_tags) as tag
        WHERE ST_CONTAINS(honolulu_buffer, geometry)
        AND ((tag.value in ('fast_food', 'restaurant') AND tag.key = 'amenity'))
    ),
 
    -- We calculate the Local Outlier Factor in order to identify restaurants without competition.
    lof_output as (
        SELECT `carto-un`.carto.LOF(ARRAY_AGG(STRUCT(id,geom)), 5) as lof FROM fast_food
    )
    SELECT lof.* FROM lof_output, UNNEST(lof_output.lof) AS lof
    ```
    We have already created the table for you, named `cartobq.docs.honolulu_competitors_lof`. You only need to add a new custom query, and run the query below:

    ```sql
    SELECT * FROM `cartobq.docs.honolulu_competitors_lof`
    ```
    Rename the layer "Competitor LOF analysis" and reorder the layer to place below "Own stores". 

    Style the boundary according to the config seen below.

    ![Map competitor lof analysis](/img/cloud-native-workspace/tutorials/tutorial13_map_competitor_lof_analysis.png)

15. Change the name of the map to "Selecting a new restaurant location using Commercial Hotspots analysis"

16. Finally we can make the map public and share the link to anybody in the organization. For that you should go to “Share” on the top right corner and set the map as Public. For more details, see [Publishing and sharing maps](../../maps/publishing-and-sharing-maps).

    ![Map public map](/img/cloud-native-workspace/tutorials/tutorial13_map_public_sharelink.png)

30. Finally, we can visualize the result.

    <iframe width="800px" height="800px" src="https://gcp-us-east1.app.carto.com/map/bf3846cc-aa71-42f2-88da-fe98233072d1"></iframe>



