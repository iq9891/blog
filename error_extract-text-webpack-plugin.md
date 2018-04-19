# Module build failed: Error: "extract-text-webpack-plugin" loader

最近配置 webpack 4 的时候遇到有关 `extract-text-webpack-plugin` 的问题。

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
- extract-text-webpack-plugin: 'next'

## 报错信息⤵️

```
ERROR in ./src/assets/styles/views/home.scss
Module build failed: Error: "extract-text-webpack-plugin" loader is used without the corresponding plugin, refer to https://github.com/webpack/extract-text-webpack-plugin for the usage example
    at Object.pitch (/Users/lee/lee/vue-spa-template/tpltest3/node_modules/extract-text-webpack-plugin/dist/loader.js:59:11)
 @ ./src/main.js 2:0-39
 @ multi babel-polyfill ./src/main.js

ERROR in ./node_modules/em-fe/dist/css/emfe.css
Module build failed: Error: "extract-text-webpack-plugin" loader is used without the corresponding plugin, refer to https://github.com/webpack/extract-text-webpack-plugin for the usage example
    at Object.pitch (/Users/lee/lee/vue-spa-template/tpltest3/node_modules/extract-text-webpack-plugin/dist/loader.js:59:11)
 @ ./src/main.js 4:0-33
 @ multi babel-polyfill ./src/main.js
 ```

 ![Module build failed: Error: "extract-text-webpack-plugin" loader](https://raw.githubusercontent.com/iq9891/blog/master/img/error_extract-text-webpack-plugin.png)

 ## 解决方案

 `extract-text-webpack-plugin` 并没有对 webpack 4 进行处理，所以替换成 `mini-css-extract-plugin` 即可。

 ## 源码

 更全的配置，请移步 [176f224](https://github.com/iq9891/vue-spa-template/commit/176f224a224c48840fc589991e141f856e030953) 。
