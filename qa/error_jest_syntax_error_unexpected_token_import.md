# jest SyntaxError: Unexpected token import

配置 jest 进行单元测试的时候，如果 `jest SyntaxError: Unexpected token import`。那么肯定是 JavaScript 的语法没有降级处理。

## 操作环境

- 开发环境： OS X El Capitan 10.11.6
- 开发工具： [Atom](https://atom.io)
- node: v9.11.1
- npm: 5.0.3
- webpack: 4.5.0
- jest: 22.4.3

## 报错信息⤵️

```
> jest

FAIL  water/icon/icon.test.js
● Test suite failed to run

/Users/lee/lee/component-template/water/icon/icon.test.js:2
import { mount } from 'vue-test-utils';
^^^^^^

SyntaxError: Unexpected token import

at ScriptTransformer._transformAndBuildScript (node_modules/jest-runtime/build/script_transformer.js:316:17)
```

![jest SyntaxError: Unexpected token import](https://raw.githubusercontent.com/iq9891/blog/master/img/error_jest_syntax_error_unexpected_token_import.png)

## 解决方案

如果文件中有高级语法需要用 babel-jest 兼容处理，并且 babel 配置中不能有 [modules](https://babeljs.cn/docs/plugins/preset-env/#modules) 字段。

### 解决之前

```
// package.json
"jest": {
  "transform": {
    ".*\\.(vue)$": "<rootDir>/node_modules/vue-jest"
  }
},
```

```
// .babelrc
{
  "presets": [
    ["env", {
      "modules": false,
      // other config
    }]
  ]
}
```

### 解决之后

```
// package.json
"jest": {
  "transform": {
    ".*\\.(vue)$": "<rootDir>/node_modules/vue-jest",
    ".*\\.(js)$": "<rootDir>/node_modules/babel-jest"
  }
},
```

```
// .babelrc
{
  "presets": [
    ["env", {
      // other config
    }]
  ]
}
```

## 源码

更全的配置，请移步 [component-template](https://github.com/fe6/component-template) 。
