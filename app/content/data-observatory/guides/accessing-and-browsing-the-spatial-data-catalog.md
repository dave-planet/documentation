## Accessing and browsing the Spatial Data Catalog

CARTO's Spatial Data Catalog allows users to explore the specifications of thousands of spatial datasets available via the Data Observatory, in order to find the best data based on their requirements.

The Spatial Data Catalog is built on top of a smart metadata system that has all characteristics defining a dataset registered in an homogenous manner (i.e. provider, coverage, schema, variable description, sample data, etc.). This provides a unified experience that allows users to explore and understand the details of very different types of spatial data.

The Spatial Data Catalog is available from our [public website](http://www.carto.com/data) and also from within the CARTO Workspace once you [log into](http://www.carto.com/login) your account and navigate to the _Data Observatory_ section.

![Spatial Data Catalog](/img/data-observatory/spatial-data-catalog.png)

There are a set of high-level metadata attributes that allow the user to filter different datasets when browsing the Spatial Data Catalog:
- Countries -- The geographical coverage of the datasets.
- Categories -- The type of data product (e.g. demographic, human mobility, road traffic, environmental, etc.).
- Licenses -- Identifies whether the dataset access is ruled by a public or premium license.
- Sources -- The premium data provider or public data source of the datasets.
- Placetypes -- The type of spatial aggregation used in the dataset (e.g. admin region, postal codes, road segments, grids, etc.).

<div style="text-align:center">
<img src="/img/data-observatory/data-observatory-dataset-metadata1.png" alt="Dataset metadata" style="width:75%; text-align:center">
</div>

Then, once a dataset from the list is selected the following additional metadata attributes are available:
- Summary description of the dataset.
- List of key variables.
- Temporal aggregation.
- Update frequency.
- Associated Geography. If applies, these are the digital boundaries (geometries) associated with this dataset, this is, its spatial aggregation. Note that some Geographies can also require their own premium license.
- Sample table with 10 rows of data.

![Data Observatory data sample](/img/data-observatory/do-data-sample.png)

- Full detailed dataset schema with variable names and descriptions.

- Map preview.

![Data Observatory map preview](/img/data-observatory/do-map-sample.png)