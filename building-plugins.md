# Building Plugins

Plugins should be built with `webpack` target `umd`.

The plugin should expose a default export that is a function that invokes `registerPlugin`.

TicketTaker will invoke the exported function after the page load event.

Here is the webpack config that we use internally to build our plugins:

```javascript
const fs = require('fs')
const path = require('path')
const WebpackManifestPlugin = require('webpack-manifest-plugin')

module.exports = {
  mode: process.env.NODE_ENV || 'development',
  entry: Object.fromEntries(
    fs
      .readdirSync(path.resolve(__dirname, 'src/client/plugins'))
      .map((p) => [p, `./src/client/plugins/${p}/index.ts`]),
  ),
  output: {
    path: path.resolve(__dirname, 'build/public/static/plugins'),
    filename: '[name].[hash].js',
    library: 'plugin-[name]',
    libraryTarget: 'umd',
  },
  module: {
    rules: [
      { test: /\.tsx?$/, loader: require.resolve('ts-loader') },
      {
        test: /\.s[ac]ss$/i,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
    ],
  },
  plugins: [
    new WebpackManifestPlugin({ fileName: '../../../manifest-plugins.json' }),
  ],
  externals: {
    react: 'react',
  },
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx', '.scss', '.css'],
  },
}
```

