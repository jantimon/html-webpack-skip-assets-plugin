# Html Webpack Skip Assets Plugin
_Skip adding certain output files to the html file. Built as a drop-in replacement for [html-webpack-exclude-assets-plugin](https://www.npmjs.com/package/html-webpack-exclude-assets-plugin) and works with newer [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) versions_

[![Build Status](https://travis-ci.org/swimmadude66/html-webpack-skip-assets-plugin.svg?branch=master)](https://travis-ci.org/swimmadude66/html-webpack-skip-assets-plugin)

## Configuration

1. Install via `npm i -D html-webpack-skip-assets-plugin`
1. Add to your webpack config AFTER HtmlWebpackPlugin
```javascript
    var HtmlWebpackSkipAssetsPlugin = require('html-webpack-skip-assets-plugin').HtmlWebpackSkipAssetsPlugin;
    // OR for import style
    import {HtmlWebpackSkipAssetsPlugin} from 'html-webpack-skip-assets-plugin'
    ...
    plugins: [
        new HtmlWebpackPlugin({
            filename: join(OUTPUT_DIR, './dist/index.html'),
            hash: false,
            inject: 'body',
            minify: minifyOptions,
            showErrors: false
            template: join(__dirname, './src/index.html'),
            // Skip Assets options can be added here
            excludeAssets: ['polyfill.**.js', /styles\..*js$/i]
            // OR
            skipAssets: ['polyfill.**.js', /styles\..*js$/i]
        }),
        new HtmlWebpackSkipAssetsPlugin({
            // or they can be passed in on the plugin. These 4 lists are combined before running
            excludeAssets: ['polyfill.**.js', /styles\..*js$/i]
            // OR
            skipAssets: ['polyfill.**.js', /styles\..*js$/i]
        })
    ]
```

The plugin takes a configuration argument with a key called `skipAssets`. This is an array of file globs (provided via [minimatch](https://github.com/isaacs/minimatch)) or regex patterns representing which output files to skip adding to the output html. In order to ease migration from html-webpack-exclude-assets-plugin](https://www.npmjs.com/package/html-webpack-exclude-assets-plugin), the plugin also supports passing `excludeAssets` as the option key, as well as the ability to add either key to the HtmlWebpackPlugin options. All provided lists will be concatenated and used to filter the assets.

## Testing
Testing is done via ts-node and mocha. Test files can be found in `/spec`, and will be auto-discovered as long as the file ends in `.spec.ts`. Just run `npm test` after installing to see the tests run.
