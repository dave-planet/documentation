## Getting Started

This guide shows how you to create a private application with layers and widgets. A private application requires users to login into the application using their CARTO credentials.

<video height="400" autoplay="" loop="" muted=""> <source src="/img/react/getting-started.mp4" type="video/mp4"> Your browser does not support the video tag. </video>

### Creating an application

CARTO for React applications are created using [Create React App](https://create-react-app.dev/) with one of the CARTO for React templates. The basic prerequisite for using Create React App is to have [Node.js](https://nodejs.org) with a package manager ([npm](https://www.npmjs.com/get-npm) or [yarn](https://yarnpkg.com/)) previously installed. In this guide we are going to use yarn.

We are going to create a new application in the `my-app` folder using the `@carto/base-3` template:

```bash
yarn create react-app my-app --template @carto/base-3
```

### Understanding the folder structure

These are the main folders:

* **src/components/common**: common components as Header, Footer, Menus, etc

* **src/components/layers**: deck.gl layers that are available to the Map component.

* **src/components/views**: pages which match with routes.

* **src/data**: sources and models.

* **src/store**: slice configuration.

* **src/utils**: general utils.

* **public**: the public folder contains the HTML file so you can tweak it, for example, to set the page title.

And these are the main files:

* **routes.js**: the file where views and routes are matched.

* **views/Main.js**: the general component that defines the layout of the application.

* **store/initialStateSlice.js**: the file that defines the configuration of CARTO as default values for the slices. Set your CARTO account, token / api key, basemap, OAuth app configuration, etc...

* **store/appSlice.js**: general slice of the app to include/extend with custom app functionality.

{{% bannerNote type="note" title="Other templates" %}}
You can also create new applications using any of the available templates, including a template for creating a CARTO 3 app with TypeScript, a basic template for CARTO 2 apps, and sample app templates for CARTO 2 and CARTO 3. Please refer to the [Templates](/react/overview) section in the Overview.
{{%/ bannerNote %}}

### Connecting your CARTO account

### Get an Application ID

To connect a private application you first need to create an Application and get a `Client ID`:

1. You need to go to the Developers section in the Workspace

2. Create a new APP with the URL `https://127.0.0.1:3000`

3. Copy the `Client ID` and introduce it at `src/store/initialStateSlice.js`.

### apiBaseUrl

Go to the Developers section in the Workspace and copy the `apiBaseUrl`.

Edit `src/store/initialStateSlice.js` to add it:

```javascript
    ...
    credentials: {
      apiVersion: API_VERSIONS.V3,
      apiBaseUrl: 'https://gcp-us-east1.api.carto.com',
    },
    ...
  },
```

### Creating a view

We're going to create a view called `Stores` that will be accesible in the `/stores` path. When this view is loaded, the layer will be displayed.

The easiest way to create a new view in the application is to use the [code generator](../code-generator). You need to execute the following command in the `my-app` folder:

```shell
yarn hygen view new
```

and select these options:

```shell
$ hygen view new
✔ Name: · Stores
✔ Route path: · stores
✔ Do you want a link in the menu? (y/N) · true
```

Now you're ready to start the local development server using the following command:

```bash
yarn
yarn start
```

You should see the map component with a `Hello World` text on the left sidebar and a link to the new view in the top navigation bar.

{{% bannerNote type="note" title="Browser certificate warning" %}}
The application uses HTTPS by default but your browser will complain because it cannot found a valid certificate. It is safe to ignore this warning when developing but you should have a valid certificate when you deploy the application to your web server. 
{{%/ bannerNote %}}

### Creating a source

A source is a key piece in a CARTO for React application. Both layers and widgets depend on sources. A source exports a plain object with a certain structure that will be understood by the CARTO for React library to feed layers or widgets using the CARTO SQL and/or Maps APIs.
   
To create a source, the easiest way is again to use the [code generator](../code-generator):

```shell
yarn hygen source new
```

When you create a source in CARTO 3, you need to provide the connection name you want to use. CARTO provides a default `carto_dw`, but you probably want to [connect](https://gcp-us-east1.app.carto.com/connections/create) your own data warehouse to access your data.

We are going to create a source pointing to the public BigQuery dataset `cartobq.public_account.retail_stores` using the `carto_dw` connection. 

```shell
$ hygen source new
✔ Name: · Stores
✔ Enter a valid connection name · carto_dw
✔ Choose type · table
✔ Type a query · cartobq.public_account.retail_stores
```

### Creating a layer

Once we have defined the source, we can add now the layer to the map. 

```shell
yarn hygen layer new
```

We select the following options:

```shell
~ yarn hygen layer new
✔ Name: · Stores
✔ Choose a source · storesSource
✔ Do you want to attach to some view (y/N) · true
✔ Choose a view · Stores (views/Stores.js)
```

If you reload the page, you will see the new layer in the map.

### Adding widgets

Finally we are ready to add some widgets to the view. We will add a Formula and a Category Widget.

The first task you need to perform is to add the following imports at the top of the `src/components/views/Stores.js` file:

```javascript
import { Divider } from '@material-ui/core';
import { AggregationTypes } from '@carto/react-core';
import { FormulaWidget, CategoryWidget } from '@carto/react-widgets';
import { currencyFormatter } from 'utils/formatter';
```

Then, in the same file, you need to replace the `Hello World` text with:

```javascript
<div>
  <FormulaWidget
    id='totalRevenue'
    title='Total revenue'
    dataSource={storesSource.id}
    column='revenue'
    operation={AggregationTypes.SUM}
    formatter={currencyFormatter}
  />

  <Divider />

  <CategoryWidget
    id='revenueByStoreType'
    title='Revenue by store type'
    dataSource={storesSource.id}
    column='storetype'
    operationColumn='revenue'
    operation={AggregationTypes.SUM}
    formatter={currencyFormatter}
  />
</div>
```

### Understanding how the pieces work together

There are two main elements in the store: the source and the viewport. When we change any of these elements, the following actions are triggered:

- The layer is filtered when the source changes.

- The widget is re-rendered when the source or viewport changes.

- Any time we change the map extent (pan or zoom), the viewport changes and all the widgets are refreshed.

- Any time a widget applies a filter (for example selecting a widget category), the filter is dispatched to the store. When we add a filter, we are changing the source, so all the components depending on the source are updated: the widgets are re-rendered and the layers are filtered. The map applies the filters using the [`DataFilterExtension`](https://deck.gl/docs/api-reference/extensions/data-filter-extension) from deck.gl.


### Where to go next 

You already have your first CARTO for React application with layers and widgets, now you can jump to the Layers guide to learn more about working with layers and customizing styling properties:

{{<link href="../layers">}}
  Layers
{{</link>}}
