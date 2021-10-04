## Browsing the Spatial Data Catalog

CARTO's Spatial Data Catalog allows users to explore thousands of spatial datasets available via the Data Observatory, in order to find the best data for their use-case

The Spatial Data Catalog is built on top of a smart metadata system that has registered all characteristics defining a data product in an homogenous manner (i.e., provider, coverage, schema, variable description, sample data, etc.). This system enables us to provide a unified experience for users to explore and understand the details of very different types of spatial data.

The Spatial Data Catalog is available from our [public website](http://www.carto.com/data) and also from within your Workspace once you [log into](http://app.carto.com/) your account and navigate to the "Data Observatory" section from the left-side menu. 

![Spatial Data Catalog](/img/cloud-native-workspace/data-observatory/do_spatial_data_catalog.png)

There are a set of high-level metadata attributes that allow the user to filter different datasets when browsing the Spatial Data Catalog:
- Countries -- The geographical coverage of the datasets.
- Categories -- The type of data product (e.g., demographic, human mobility, road traffic, environmental, etc.)
- Licenses -- Identifies whether the dataset access is governed by a public or premium license.
- Sources -- The premium data provider or public data source of the datasets.
- Placetypes -- The type of spatial aggregation used in the dataset (e.g. admin region, postal codes, road segments, grids, etc.).

![Spatial Data Catalog metadata](/img/cloud-native-workspace/data-observatory/do-dataset-metadata.png)

<!-- <div style="text-align:center">
<img src="/img/data-observatory/data-observatory-dataset-metadata1.png" alt="Dataset metadata" style="width:85%; text-align:center">
</div> -->

Then, once a dataset from the list is selected the following additional metadata attributes are available:

- Summary description of the dataset.
- List of key variables.
- A sample table with 10 rows of data.
- Full detailed dataset schema with variable names and descriptions.
- Map preview.

From the Summary, there is also information on the right hand side about the following:

- License
- Country
- Source
- Placetype
- Temporal aggregation.
- Update frequency.
- Associated Geography. If applicable, these are the digital boundaries (geometries) associated with this dataset, this is, its spatial aggregation. Note that some Geographies can also require their own premium license.

![Data Observatory summary sample](/img/cloud-native-workspace/data-observatory/do-summary-sample.png)

![Data Observatory data sample](/img/cloud-native-workspace/data-observatory/do-data-sample.png)

![Data Observatory map sample](/img/cloud-native-workspace/data-observatory/do-map-sample.png)

You can have access to a sample of the data by clicking on *Access free sample*:

![Data Observatory access free sample](/img/cloud-native-workspace/data-observatory/do-public-access-free-sample.png)

A new dialog will open so you can accept the terms of use of the data (e.g. evaluation purposes only). Click on *Connect sample* to connect to the data sample. 

![Data Observatory connect your sample](/img/cloud-native-workspace/data-observatory/do-connect-your-sample.png)

When you connect your data sample, you will be redirected to the Data Explorer section, from where you can explore your current connections as well as your Data Observatory subscriptions and sample data.

![Data Observatory sample dataset](/img/cloud-native-workspace/data-observatory/do-sample-dataset.png)