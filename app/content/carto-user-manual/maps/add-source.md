## Add source

When you open a map, the *Layers* tab will appear on the left side panel. There you can add data as layers to the map by clicking on "Add source from", where you can access the contents from your existing data warehouse connections. If you haven’t added a data layer to the map yet, you will see the following page:

![Add source to your map](/img/cloud-native-workspace/maps/map_add_source_to_your_map.png)

### ADD SOURCE FROM A CONNECTION

From the *Layers* tab, go to the *Sources* panel and click on *Add source from...*. A new dialog screen will open allowing you to select a table or a tileset from on of your connections. Insert the *Fully Qualified Table* or the *Tileset Name* and click *Add source*.

![Add source select a connection](/img/cloud-native-workspace/maps/map_add_source_selected_connection.png)

![Add source select a table](/img/cloud-native-workspace/maps/map_add_source_table.png)

Once the process is finished, the table or tileset is included in the Builder map as a new layer. The map displays the basemap and the new layer on top. You can add additional layers, or start applying styling and analysis features.
	
![Map created](/img/cloud-native-workspace/maps/map_created.png)

### ADD SOURCE FROM A CUSTOM QUERY

Go to *Sources* and click *Add source from...*. A new dialog screen will open allowing you to create your own query or run a SQL analysis to data on your connection. Select an option and click *Add source*.

![Add source custom query](/img/cloud-native-workspace/maps/map_add_source_custom_query.png)

![Add source analysis query](/img/cloud-native-workspace/maps/map_add_source_analysis_query.png)

Once the process is finished, the SQL console appears in the Builder interface You can type your query by inserting the *Fully Qualified Table* or the *Tileset Name* when calling an object and then click *Run*. 

![Map sql console](/img/cloud-native-workspace/maps/map_sql_console.png)

In this example we are going to use a table accessible via a BigQuery connection. The BigQuery table is included in the Builder map tool as a new layer. You can add additional layers, or apply styling and analysis features.
	
![Map add query](/img/cloud-native-workspace/maps/map_add_query.png)

### ADD SOURCE FROM A LOCAL FILE

Go to *Sources* and click *Add source from...*. A new dialog will open allowing you to upload a CSV, Json, GeoJSON, or a saved map Json file. You can browse your files, or drag & drop them into the dotted area of the dialog screen.

![Add source local file](/img/cloud-native-workspace/maps/map_add_source_file.png)

Once the data has been imported, the dataset is included in the Builder map tool as a new layer. You can then add additional layers, or apply styling and analysis features.
	
![Map local file](/img/cloud-native-workspace/maps/map_paris.png)

In all cases, you can keep adding multiple data to your map from your different data sources available.