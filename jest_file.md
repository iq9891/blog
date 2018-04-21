# jest 测试覆盖报告 File 中并没有测试的文件

jest 编写单元测之后，查看测试报告 File 中并没有包含测试的 vue 文件。

## 情景描述

待测试文件 Icon.vue ，测试报告如下图⤵️

![jest 测试覆盖报告中并没有测试的文件](https://raw.githubusercontent.com/iq9891/blog/master/img/jest_file.png)

## 解决方案

困扰我一天的问题，究竟出在哪里了，我查看了网上流传的各种 vue 的案例，都没啥问题。于是我仔细检查了一下我要测试 Icon.vue 文件。却发现了其中的奥妙所在。发现加上 data 这个方法之后，神奇般的就加入了这个文件

### 解决之前

```
<template>
  <i>这是一个图标组件。</i>
</template>
<script>
export default {
  name: 'WIcon',
}
</script>
```

### 解决之后

```
<template>
  <i>这是一个图标组件。</i>
</template>
<script>
export default {
  name: 'WIcon',
  data () {
    return {}
  }
}
</script>
```

### 最终想要的结果

加入 data 参数之后，测试报告中神奇般的出现了 Icon.vue 文件。

![jest 测试覆盖报告中并没有测试的文件](https://raw.githubusercontent.com/iq9891/blog/master/img/jest_file_after.png)


## 操作环境

- 开发环境： OS X El Capitan 10.11.6
- 开发工具： [Atom](https://atom.io)
- node: v9.11.1
- npm: 5.0.3
- babel-jest： 22.4.3
- jest： 22.4.3
- jest-serializer-vue： 1.0.0
- vue: 2.5.16
- vue-jest： 2.5.0
- webpack： 4.6.0

## 源码

更全的配置，请移步 [component-template](https://github.com/fe6/component-template) 。
