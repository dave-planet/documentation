## Upgrade Guide

This guide includes information about changes between CARTO for React v1.0 and v1.1. 

In this documentation site we have already updated the documentation for version 1.1.0-beta but, currently, the latest stable version is 1.0.2 for the templates and 1.0.1 for the library. 

CARTO for React v1.1 includes support for deck.gl 8.5 that provides data visualization capabilities for the new [CARTO 3 platform](#compatibility-with-platform-versions). Read more about the capabilities in this new deck.gl version [here](/deck-gl).

You can start testing CARTO for React v1.1 beta right now but we don't recommend its use for production applications yet. We will release the final stable version when CARTO 3 is launched.

### Library changes

If you update an application that is using v1.0 of the CARTO for React library to v1.1, there are some minor changes that might affect your existing code (we have already updated our documentation with these changes):

- [useCartoLayerProps](react/library-reference/api/#usecartolayerprops) now uses object destructuring instead of multiple arguments
- [executeSQL](/react/library-reference/api/#executesql) now uses object destructuring instead of multiple arguments
- `SourceTypes` constants have been removed from the `@carto/react-api` package
- The `type` property in data sources now accepts a different set of values. You need to use `MAP_TYPES.QUERY` if you were using `'sql'` or `MAP_TYPES.TILESET` if you were using `'bigquery'`. The `MAP_TYPES` constants are defined in the `@deck.gl/carto` package.

### Template changes

In this new version 1.1, we have also renamed our existing templates and added a new template for creating applications with the CARTO 3 platform:

- `base-2` is the new name for the existing CARTO 2 skeleton template, previously the default `@carto` template

   ```shell
   $ npx create-react-app my-app --template @carto/base-2
   ```

- `base-3` is the name for the new CARTO 3 template

   ```shell
   $ npx create-react-app my-app --template @carto/base-3
   ```

- `sample-app-2` is the new name for the existing sample app template for CARTO 2, previously named `sample-app`

   ```shell
   $ npx create-react-app my-app --template @carto/sample-app-2
   ```

### Compatibility with platform versions

CARTO for React v1.1 is the first version compatible with the CARTO 3 platform. CARTO 3 is a fully cloud native platform that is currently in beta and provides direct connectivity to cloud data warehouses without the need for importing data first into CARTO. If you want to request access, please fill in [this form](https://carto.com/carto3/).
