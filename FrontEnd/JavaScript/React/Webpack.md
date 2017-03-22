# Webpack

* [Webpack v2 Quick Start](http://bendyworks.com/blog/webpack-v2-quick-start)
* [From zero to webpack, one error at the time](http://www.jumoel.com/2017/zero-to-webpack.html)
* [Webpack 2 Loader Variations](http://andrewhfarmer.com/webpack-2-loader-variations/)

```js
module: {
  rules: [
    {
      test: /\.css$/,
      use: [
        'style-loader',
        'css-loader'
      ]
    }
  ]
}

// Production
module: {
  rules: [
    {
      test: /\.css$/,
      use: ExtractTextPlugin.extract({
        fallback: 'style-loader',
        use: 'css-loader'
      })
    }
  ]
}
```

```js
// Shim jQuery
resolve: {
  alias: {
    jquery: 'jquery/src/jquery'
  }
},

plugins: [
  new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery'
  })
]
```

## Code Splitting

2 splitting worth doing:

1. Vendor chunks
2. Application chunks

## NamedModulesPlugin

Webpack, by default, assigns modules integer ids based on order. So when modules are changed, all ids could change, invalidating the cache. To use names instead of ids, we can use NamedModulesPlugin.

However, it will make the file sizes larger as well as expose internal file paths of modules to outside world.

Use Webpack NamedModulesPlugin to use deterministic module names instead of non-deterministic integer ids.

## Production

`webpack -p` is equivalent to:

```
webpack --optimize-minimize --define process.env.NODE_ENV="production"
```

Make sure you don't use it twice at the CLI and at the webpack.config.js file. Remove `-p` or you will have double minification which will result in bad bugs.

## Long-term Caching: Chunkhash

Note that Hash is for "entire" build and chunkhash is for individual file.

* [Caching assets long term with Webpack](https://medium.com/connect-the-dots/caching-assets-long-term-with-webpack-5ad24a4c39bd#.427deo91l)

Long-term bundle caching is achieved with content-based hashing policy: `[chunkhash]`.

You should not use `[chunkhash]` or `[hash]` for development as this will cause memory leak, because the dev server does not know when to clean up the old files.

## Hot Reload

* [Hot reload all the things!](https://hackernoon.com/hot-reload-all-the-things-ec0fed8ab0#.dok0iuu17)
