# this[NS] is not a function

最近配置 webpack 4 的时候遇到有关 `mini-css-extract-plugin` 的问题。

## 操作环境

- 开发环境： OS X El Capitan 10.11.6
- 开发工具： [Atom](https://atom.io)
- node: v9.11.1
- npm: 5.0.3
- webpack: 4.5.0
- postcss-loader: 2.1.3
- css-loader: 0.28.11
- node-sass: 4.8.3
- sass-loader: 7.0.1
- mini-css-extract-plugin: 0.4.0

## 报错信息⤵️

```
ERROR in ./src/views/Home.vue (./node_modules/mini-css-extract-plugin/dist/loader.js!./node_modules/css-loader?{"minimize":true,"sourceMap":true}!./node_modules/vue-loader/lib/style-compiler?{"optionsId":"0","vue":true,"scoped":false,"sourceMap":false}!./node_modules/sass-loader/lib/loader.js?{"sourceMap":true}!./node_modules/vue-loader/lib/selector.js?type=styles&index=0!./src/views/Home.vue)
Module build failed: TypeError: this[NS] is not a function
    at childCompiler.runAsChild (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/mini-css-extract-plugin/dist/loader.js:147:15)
    at compile (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compiler.js:242:11)
    at hooks.afterCompile.callAsync.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compiler.js:487:14)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:24:1)
    at AsyncSeriesHook.lazyCompileHook [as _callAsync] (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/Hook.js:35:21)
    at compilation.seal.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compiler.js:484:30)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook [as _callAsync] (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/Hook.js:35:21)
    at hooks.optimizeAssets.callAsync.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compilation.js:966:35)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook [as _callAsync] (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/Hook.js:35:21)
    at hooks.optimizeChunkAssets.callAsync.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compilation.js:957:32)
    at _err0 (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:11:1)
    at /Users/lee/lee/vue-spa-template/tpltest7/node_modules/uglifyjs-webpack-plugin/dist/index.js:334:11
    at _class.runTasks (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/uglifyjs-webpack-plugin/dist/uglify/index.js:63:9)
    at UglifyJsPlugin.optimizeFn (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/uglifyjs-webpack-plugin/dist/index.js:253:16)
 @ ./src/views/Home.vue 2:2-356
 @ ./src lazy ^\.\/.*$ namespace object
 @ ./src/tools/loadcomponents.js
 @ ./src/routers/index.js
 @ ./src/main.js
 @ multi babel-polyfill ./src/main.js

ERROR in ./src/App.vue (./node_modules/mini-css-extract-plugin/dist/loader.js!./node_modules/css-loader?{"minimize":true,"sourceMap":true}!./node_modules/vue-loader/lib/style-compiler?{"optionsId":"0","vue":true,"scoped":false,"sourceMap":false}!./node_modules/sass-loader/lib/loader.js?{"sourceMap":true}!./node_modules/vue-loader/lib/selector.js?type=styles&index=0!./src/App.vue)
Module build failed: TypeError: this[NS] is not a function
    at childCompiler.runAsChild (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/mini-css-extract-plugin/dist/loader.js:147:15)
    at compile (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compiler.js:242:11)
    at hooks.afterCompile.callAsync.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compiler.js:487:14)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:24:1)
    at AsyncSeriesHook.lazyCompileHook [as _callAsync] (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/Hook.js:35:21)
    at compilation.seal.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compiler.js:484:30)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook [as _callAsync] (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/Hook.js:35:21)
    at hooks.optimizeAssets.callAsync.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compilation.js:966:35)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook [as _callAsync] (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/Hook.js:35:21)
    at hooks.optimizeChunkAssets.callAsync.err (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/webpack/lib/Compilation.js:957:32)
    at _err0 (eval at create (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/tapable/lib/HookCodeFactory.js:24:12), <anonymous>:11:1)
    at /Users/lee/lee/vue-spa-template/tpltest7/node_modules/uglifyjs-webpack-plugin/dist/index.js:334:11
    at _class.runTasks (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/uglifyjs-webpack-plugin/dist/uglify/index.js:63:9)
    at UglifyJsPlugin.optimizeFn (/Users/lee/lee/vue-spa-template/tpltest7/node_modules/uglifyjs-webpack-plugin/dist/index.js:253:16)
 @ ./src/App.vue 2:2-346
 @ ./src/main.js
 @ multi babel-polyfill ./src/main.js
 ```

 ![this[NS] is not a function](https://raw.githubusercontent.com/iq9891/blog/master/img/error_this_is_not_a_function.png)

 ## 解决方案

 `mini-css-extract-plugin` 使用的必须有 loader ，有调用。但如果光有 loader ，没有调用，那么就会报上面的错误。怎么解决呢？加上调用就可以了

 ```
 // build/webpack.prod.conf.js

 var MiniCssExtractPlugin = require("mini-css-extract-plugin");

 var webpackConfig = merge(baseWebpackConfig, {
   // other options...
   plugins: [
     // 提取
     new MiniCssExtractPlugin({
       filename: utils.assetsPath('css/[name].[contenthash].css')
     })
   ]
 })
 ```

 ## 源码

 更全的配置，请移步 [176f224](https://github.com/iq9891/vue-spa-template/commit/176f224a224c48840fc589991e141f856e030953) 。
