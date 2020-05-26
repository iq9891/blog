# node: No such file or directory



几年前，第一次玩 mac ，所以多年前不小心没卸载 node ，直接安装的 nvm ，结果导致切换版本总是报下面的错误；

```
nvm is not compatible with the npm config "prefix" option: currently set to "/Users/XXX/.nvm/versions/node/v0.12.7"
Run `nvm use --delete-prefix v4.6.2` to unset it.
```

当时处理的问题是直接把原装 node 卸载，结果一直在命令行工具启动的时候，node 都找不到。今天终于找到了办法，记录一下。

解决方案:

将 nvm 管理的所要用的 node 软链到程序目录，每次打开就找到了

```
ln –s .nvm/versions/node/v13.14.0/bin/node /usr/local/bin/node
```