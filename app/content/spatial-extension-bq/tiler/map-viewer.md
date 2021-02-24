## Map Viewer

Map Viewer is a new tool for visualizing tilesets directly from the Dashboard. To open Map Viewer, just click on a tileset from 'Your Tilesets' tab in the 'Data' section of the Dashboard. 

Map Viewer provides some defaults to help you explore your data, but it's possible to customize the cartography using the [deck.gl styling language](../../../deck-gl/guides/style-language).

For this guide, we will use a tileset that contains every european river. It's available in the CARTO Data Observatory public data project in BigQuery. To visualize it, just type the `bqcartodemos` in the project selector and find the `tilesets` dataset.

![eurivers tileset](/img/bq-spatial-extension/tiler/guides-eurivers.png)

### Map Style

By clicking on the icon on the left bar, the Map Style panel will appear, showing a text editor with a predefined style.

As mentioned before, Map Viewer uses deck.gl's style language. For more detailed information about the language's capabilities, see the complete reference [here](../../../deck-gl/guides/style-language/#api-reference).

![Map Style](/img/bq-spatial-extension/tiler/guides-mapstyle.png)

#### Basemaps

Map Viewer offers different basemaps for your visualizations. Click on the icon in the top-left corner to show the basemap selector. 

*Positron*, *Dark Matter* and *Voyager* CARTO basemaps are optimized for data visualization and will make your data layer stand out. 

You can also use Google Maps as basemaps, selecting *Roads* or *Satellite*

![Map Style basemap selector](/img/bq-spatial-extension/tiler/guides-basemap-selector.png).

#### Basic styles

You can quickly change some of the properties, like `getFillColor` for changing the fill colors of points and polygons, or `getLineColor` for lines. The property expects a color defined as an `[r,g,b,[a]]` array. Simple visualization properties are detailed [here](../../../deck-gl/guides/style-language/#layers-basic-properties).

#### Color ramps

Basic styles might be a good option for the most basic maps, but creating more sophisticated, data-driven visualizations is also possible using [helper functions](../../../deck-gl/guides/style-language/#creating-advanced-visualizations) for three different types of visualization: 

* `colorBins` assigns different colors to different buckets in the data range. This is useful for a choropleth visualization where you need to define the breaks of the data and define a color palette.
* `colorCategories` assigns colors to specific values. This is useful for visualizing categorical data.
* `colorContinuous` assings a blend color based on a linear interpolation of values. This is useful for different types of visualizations. This is the one we are going to use for our example.

Replace the `getLineColor` property with the following block to style the rivers depending on their bearing. 

```javascript
  "getLineColor": {
    "@@function": "colorContinuous",
    "attr": "bearing",
    "domain": [
      0,
      60,
      120,
      180,
      240,
      300,
      360
    ],
    "colors": "Earth"
  }
```

Let's explain a bit how this function works:

* `"attr"`: Select a property from your tileset that contains the values that you want to use for the styling. In this case it's `bearing`, which contains the direction in degrees relative to the North in which each river flows. 
* `"domain"`: In this case, it contains the values that will be used for the interpolation. 
* `"colors"`: This value can be an array of `[r,g,b,[a]]` colors that will be mapped with the values in the domain. The intermediate colors will be assigned based on the linear interpolation of values.
Another option is just using a [CARTOcolors](https://carto.com/carto-colors) palette, by just indicating its name.

Take a look at the result. Can you appreciate how the hydrographic basins stand out, just by assigning different colors to each river's bearing?  

![Map Style ramp](/img/bq-spatial-extension/tiler/guides-ramp.png)


#### Open TileJSON

At the bottom of the _Map Style_ section you will find an _Open TileJSON_ button. It will open a new tab with a TileJSON request. The response contains a description of the tileset in TileJSON format, with metadata about: 
* The URL pattern to retrieve the tiles. 
* Zoom range, bounds and center of the features in the tileset.
* Information about the layers contained in the tileset.
* Tilestats with statistic information such as maximum, minimum, average, count and sum. It also includes a section called `quantiles` that contains the quantile breaks for the properties included, as well as the top 10 categories and their frequency. 

#### Copy XYZ URL

Also at the bottom of the _Map Style_ section there is a _Copy XYZ URL_ that copies directly in your clipboard the tiles URL following the XYZ convention:

{{% bannerNote type="code" %}}
https://maps-api-v2.us.carto.com/user/USERNAME/bigquery/tileset/{z}/{x}/{y}?source=project.dataset.tileset(...)&api_key=API_KEY
{{%/ bannerNote %}}

This is most useful for loading the tileset with any webmapping library or desktop application, like QGIS.

### Share

The _Share_ section allows publishing a tileset. By publishing, we grant **CARTO BigQuery Data Viewer** (`bigquery/dataViewer`) permissions to the associated tileset. Doing so, this map becomes public on the web and anybody with the URL will be able to see it.

By unpublishing the tileset, we will revoke the permission mentioned above and disable the sharing links. 

{{% bannerNote title="Note" %}}
It can take up to 5 minutes to remove the map from the CDN cache.
{{%/ bannerNote %}}

Once published, you will find different options to publish the map URL in social networks, as well as the HTML code to embed the map on a website. 
