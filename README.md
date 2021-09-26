# babel-plugin-file-loader

This is a 2021 fork of [babel-plugin-file-loader](https://github.com/sheerun/babel-plugin-file-loader) by [@sheerun](https://github.com/sheerun)
and is a temporary shim that fixes importing SVGs from `node_modules` until the original plugin is updated. see [issue #8](https://github.com/sheerun/babel-plugin-file-loader/issues/8) for more information.

## Installation

```bash
yarn add @openovate/babel-plugin-file-loader
```

Or if you like npm:

```bash
npm install @openovate/babel-plugin-file-loader --save
```

Then put following `@openovate/babel-plugin-file-loader` as plugin in `.babelrc`:

```json
{
  "plugins": ["@openovate/babel-plugin-file-loader"]
}
```

This is equivalent to following default configuration:

```json
{
  "plugins": [
    [
      "@openovate/babel-plugin-file-loader",
      {
        "name": "[hash].[ext]",
        "extensions": ["png", "jpg", "jpeg", "gif", "svg"],
        "publicPath": "/public",
        "outputPath": "/public",
        "context": "",
        "limit": 0
      }
    ]
  ]
}
```

## Matching with Webpack 5 file-loader

In Babel. *(.babelrc)*

```json
{
  "plugins": [
    [
      "@openovate/babel-plugin-file-loader",
      {
        "extensions": ["png", "jpg", "jpeg", "gif", "svg"],
        "name": "[md5:hash:base64:7].[ext]",
        "publicPath": "/public/assets"
      }
    ]
  ]
}
```

In webpack using [file-loader](https://www.npmjs.com/package/file-loader). *(webpack.config.js)*

```js
{
  ...
  module: {
    rules: [
      ...
      {
        test: /\.(png|jpe?g|gif|svg)$/i,
        use: [
          {
            loader: 'file-loader',
            options: {
              name: '[md5:hash:base64:7].[ext]',
              publicPath: '/public/assets',
              outputPath: 'assets'
            }
          }
        ]
      }
      ...
    ]
  }
}
```

## More Info

See the original ([babel-plugin-file-loader](https://github.com/sheerun/babel-plugin-file-loader)) documentation.
