# Babel

* Babel 6 - Released 2015
* Babel 7 - Released Aug 2018

Don't confuse Babel with Webpack. Babel is a compiler and Webpack is a module bundler (your build system).

* [James Kyle's Babel Handbook](https://github.com/thejameskyle/babel-handbook/)

```
▶ npm install --save-dev @babel/core @babel/cli @babel/preset-env
▶ npm install --save @babel/polyfill

// If you have npm@5.2.0, you can use npx
▶ npx babel

▶ env NODE_ENV=development node_modules/.bin/babel-node

▶ npx babel src --out-dir lib --plugins=@babel/plugin-transform-arrow-functions
```

## .babelrc or package.json or babel.config.js?

* JSON5 format
* Using `babel.config.js` is recommended since Babel 7. Not a replacement for `.babelrc`??

## Main Packages

* @babel/core - where the transform takes place: `babel.transform("code()")`
* @babel/cli - compile files from command line.
* @babel/node

```
> import * as babel from "@babel/core"
SyntaxError: /path/repl: Modules aren't supported in the REPL
> 1 | import * as babel from "@babel/core"
    | ^
```

**Modules aren't supported in the REPL**. If you want to use ES6-style module-loading in Node REPL, it is not supported due to technical limitations.

## Plugins

By default Babel does anything. You need to plugins for babel to do anything useful.

Plugins are used to transform syntax without waiting for browser support.

* babel-plugin-macros

## Presets

Instead of adding all the plugins we want one by one, we can use a "preset" which is pre-determined set of plugins.

* **@babel/preset-env** - We already deprecated babel-preset-latest a while ago, as well as babel-preset-es2016, etc. No more yearly decision on what preset to use. Without any configuration, by just using the `@babel/preset-env`, it will include all plugins to support modern JavaScript development (ES2015, ES2016, etc.).
* **@babel/preset-react**

You can configure your preset at `babel.config.js`.

## Polyfill and useBuiltIns

@babel/polyfill is provided as a convenience and you need to use it with @babel/preset-env and the `useBuiltIns` option in order to not include the whole polyfill which isn't always needed.

```js
// Use it at your application's entry point
import '@babel/polyfill';

// Or if you have access to webpack.config.js
module.exports = {
  entry: ['@babel/polyfill', './app.js']
};
```

## Loose Mode is not Spec compliant

Babel tries to be compact and use less dependency, but this may be difficult to do in cases. That's why you see those "loose" transforms that tradeoff spec compliancy for performance. It will be faster, but it may not be so compliant.

If you need a faster/smaller build, you should use the `loose` option which will purposely disregard certain spec changes like runtime checks and other edge cases.

