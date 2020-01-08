# 设置国内镜像

由于国内网速的无敌慢，所以国内镜像就显得尤为重要。

## yarn 相关

#### 设置镜像

1. 命令： 

```
yarn config set registry https://registry.npm.taobao.org
```

2. 结果： 

```
yarn config v1.21.1
success Set "registry" to "https://registry.npm.taobao.org".
✨  Done in 0.05s.
```

#### 获取镜像

1. 命令：

```
yarn config get registry
```

2. 结果：

```
https://registry.yarnpkg.com
```

## npm 相关

#### 设置镜像

设置淘宝命令： `npm config set registry https://registry.npm.taobao.org`
设置 npm 命令： `npm config set registry http://registry.npmjs.org`


#### 获取镜像

命令： `npm config get registry`

#### 二进制包镜像(可选择添加)

```
npm set chromedriver_cdnurl http://cdn.npm.taobao.org/dist/chromedriver # chromedriver 二进制包镜像
npm set operadriver_cdnurl http://cdn.npm.taobao.org/dist/operadriver # operadriver 二进制包镜像
npm set phantomjs_cdnurl http://cdn.npm.taobao.org/dist/phantomjs # phantomjs 二进制包镜像
npm set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass # node-sass 二进制包镜像
npm set electron_mirror http://cdn.npm.taobao.org/dist/electron/ # electron 二进制包镜像
```