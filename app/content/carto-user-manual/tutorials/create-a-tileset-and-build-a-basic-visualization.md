---
title: "Create a tileset and build a basic visualization"
description: "Understanding the urban areas has important implications in a wide range of geospatial analysis, for example, to inform decision-makers in sectors such as urban planning. In this example we are creating a tileset in which each building in Madrid is represented by a polygon and each of them is assigned a graduated color from the lowest to the highest value of the gross floor area. This visualisation allows us to represent at a glance how the surface area in Madrid is distributed." 
image: "/img/tutorials/tileset.png"
type: tutorials
date: "2021-05-12"
# categories:
#     - easy
#     - tileset
---
## Create a tileset and build a basic visualization

**Context**

Understanding the urban areas has important implications in a wide range of geospatial analysis, for example, to inform decision-makers in sectors such as urban planning.

<!-- This dataset is provided by Inspire, and it requires a tileset to be visualized entirely due to their size. -->

In this example we are creating a tileset in which each building in Madrid is represented by a polygon and each of them is assigned a graduated color from the lowest to the highest value of the gross floor area. This visualisation allows us to represent at a glance how the surface area in Madrid is distributed.

**Steps To Reproduce**

1. Go to the <a href="http://app.carto.com/signup" target="_blank">CARTO signup</a> page.
   - Click on *Log in*.
   - Enter your email address and password. You can also log in with your existing Google account by clicking *Continue with Google*.
   - Once you have entered your credentials: click *Continue*.

   ![Log in Email and password](/img/cloud-native-workspace/get-started/login.png)

2. From the Navigation Menu in the left panel, select Data Explorer. 

   ![Menu features data explorer](/img/cloud-native-workspace/tutorials/tutorial1_the_menu_features_data_explorer.png)

3. Select the [CARTO Data Warehouse](../../connections/carto-data-warehouse) connection and click on *demo data > demo_tables* from the collapsible tree. 

   ![Data Explorer content carto data warehouse](/img/cloud-native-workspace/tutorials/tutorial1_content_carto_dw.png)

4. Selected "inspire_buildings_madrid" and explore the preview of the map and the details of the table.

   ![Data Explorer map prewiew](/img/cloud-native-workspace/tutorials/tutorial6_de_map_preview.png)

   ![Data Explorer data prewiew](/img/cloud-native-workspace/tutorials/tutorial6_de_data_preview.png)

5. This table, due to its size and current constraints in Builder, can be added to Builder by using the [dynamic tile generation](../../maps/performance-considerations/#medium-size-datasets) or [creating a tileset](../../data-explorer/creating-a-tileset-from-your-data).

   Therefore, in order to build a visualization with this table, we are going to create a tileset by clicking on the *Create > Create a tileset* button on the top. This will open the table as a layer on a CARTO Builder map.

   ![Data Explorer create tileset](/img/cloud-native-workspace/tutorials/tutorial6_de_create_tileset_button.png)

6. Now from this interface will allow you to set the location and name of the output tileset in a directory within the `CARTO Data Warehouse` where the user has write permissions. In the case of the `CARTO Data Warehouse` connection for this user account the directory is `carto-dw-ac-t4cgd7ox.data`. Once you have completed this configuration, click on *Save here*.

   ![Data Explorer create tileset settings](/img/cloud-native-workspace/tutorials/tutorial6_de_create_tileset_destination.png)

7. In the next screen, you need to select the tileset zoom levels and choose the geometry column. Once you have completed this configuration, click on *Continue*.

   ![Data Explorer create tileset settings](/img/cloud-native-workspace/tutorials/tutorial6_de_create_tileset_the_settings.png)

8. From the next screen, you can select the attributes of your table that will be included in the tileset. After completing this step, click on *Continue*. 

   ![Data Explorer create tileset attributes](/img/cloud-native-workspace/tutorials/tutorial6_de_create_tileset_the_attributes.png)

9. The last screen will show you a summary of the configuration of the tileset for your confirmation. Click on *Create* to confirm.

   ![Data Explorer create tileset confirmation](/img/cloud-native-workspace/tutorials/tutorial6_de_create_tileset_the_confirmation.png)

10. Tilesets take a while to process. Once the process is completed you will see the message in the “Processing jobs” tab on the top right corner of the screen (blue tab).

   ![Data Explorer tileset processing running](/img/cloud-native-workspace/tutorials/tutorial6_de_tileset_processing_running.png)

11. Once the job has completed we can access the tileset in the Data Explorer and create a map visualization with all that data. 

    ![Data Explorer tileset processing successfully](/img/cloud-native-workspace/tutorials/tutorial6_de_tileset_processing_successfully.png)

12. Click on *Create map* and this source will be added as a layer in Builder.

    ![Data Explorer create map from the new tileset](/img/cloud-native-workspace/tutorials/tutorial6_de_create_map_from_the_new_tileset.png)

    ![Map created from the new tileset](/img/cloud-native-workspace/tutorials/tutorial6_de_map_created_from_tileset.png)

12. Now let's style this layer as we want to build a cool visualization.

    ![Map fill based on](/img/cloud-native-workspace/tutorials/tutorial6_map_fill_color_based_on.png)

13. Finally we can change our basemap. Go to Basemaps tab and select “Dark matter” from Google Maps.

    ![Map basemap google maps](/img/cloud-native-workspace/tutorials/tutorial6_map_basemap_dark_google_maps.png)

13. We can also make the map public and share it online with our colleagues. For more details, see [Publishing and sharing maps](../../maps/publishing-and-sharing-maps).

    ![Map public map](/img/cloud-native-workspace/tutorials/tutorial6_map_public_map_options.png)

14. Finally, we can visualize the result.

    <iframe width="800px" height="400px" src="https://gcp-us-east1.app.carto.com/map/8c4b5450-de0d-41ed-8485-4b6a2b0e6614"></iframe>