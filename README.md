# Gatsby Plugin GraphQL Preview

> **A Gatsby plugin to automatically make the source-graphql parts of your
> application available as a live updating preview.**

_This plugin is in a pretty early status. Use at your own risk._

Requires React 16.8 or newer. (it uses hooks 🤫)

This works by doing the following:

1. Grab the pages graphql query, isoloate the parts that belong to the remote
   graphql source and make it available to the page.
2. If on the client, the query paramter perview has a truthy value, wrap the
   page inside an apollo setup, that replaces the statically queried remote data
   with fresh data queried on the client.
3. Add a tiny UI to control how and when to re-query the data.

It only works conjunction with `gatsby-source-graphql`.

## Install

with yarn

```
yarn add gatsby-plugin-graphql-preview
```

<details>
<summary>with npm</summary>

```
npm install --save gatsby-plugin-graphql-preview
```

</details>

## How to use

Add the plugin to the plugins array in your `gatsby-config.js`.

It requires the same configuration options as gatsby-source-graphql. I'd suggest
extracting the configuration into a variable instead of copying it.

_`gatsby-source-graphql`s `createLink` is not yet supported. The `url` field is
required._

```javascript
// In your gatsby-config.js

const graphqlOptions = {
  typeName: 'SWAPI',
  fieldName: 'swapi',
  url: 'https://api.graphcms.com/simple/v1/swapi',
};

module.exports = {
  plugins: [
    {
      resolve: 'gatsby-source-graphql',
      options: graphqlOptions,
    },
    {
      resolve: 'gatsby-plugin-graphql-preview',
      options: graphqlOptions,
    },
  ],
};
```

Open a page that includes a query to your graphql-source and append `?preview=1`
to your pathname in the browser. It should include a small ui to configure in
which interval the endpoint should be polled.

## To do

- Configuration
  - Add option to configure the serach/query param (currently hardcoded)
  - Add option for custom PreviewUI component (currently hardcoded)
- Improve documentation and add examples
- Add tests
- Create cool example gif
