# webpack 4 提取 CSS 等样式文件

`extract-text-webpack-plugin` ，只支持 webpack 4 以下提取 CSS 文件，那么 webpack 4 怎么办呢？下面就为大家详细介绍 webpack 4 提取 CSS 文件的配置方法。

```
yarn add mini-css-extract-plugin
```

## 普通项目配置

> 需要注意的是 `MiniCssExtractPlugin.loader` 和 `style-loader` 由于某种原因不能共存。

```
// webpack.config.js

var MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  // other options...
  module: {
    rules: [
    {
      test: /.scss$/,
      use: [
        MiniCssExtractPlugin.loader,
        'css', 'sass',
      ]
    },
    ]
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: 'style.css'
    })
  ]
}
```

## Vue.js 全家桶的配置

>这里只展示关于提取 CSS 的代码。

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

```
// build/utils.js

var MiniCssExtractPlugin = require("mini-css-extract-plugin");

// other options...
if (options.extract) {
  return [MiniCssExtractPlugin.loader].concat(loaders)
} else {
  return ['vue-style-loader'].concat(loaders)
}
```

## 源码

更全的配置，请移步 [176f224](https://github.com/iq9891/vue-spa-template/commit/176f224a224c48840fc589991e141f856e030953) 。
