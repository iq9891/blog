# mac 使用

## 对应关系

|mac|win|
|---|---|
|command(cmd)|ctrl|
|control|alt|
|option+cmd+i|f12 (谷歌中查找元素)|

## 与 win 不一样的地方

1.  点击选中文件夹，按 **回车** 可重命名文件夹名字
2. 安装软件
 - dmg 结尾的文件，打开之后拖动到 Applications
 - 命令行运行， 如 `brew install git` , 安装 git 软件

## 快捷键

### mac 的快捷方式

|命令|功能|
|----|----|
|cmd + q|关上整个软件(如 关上 atom)，不在后台执行|
|cmd + w|关上整个软件(如 关上 atom)，在后台执行|
|cmd + tab + ]|切换软件标签 向右|
|cmd + tab + [|切换软件标签 向左|
|cmd + tab|切换当前软件运行窗口|


### 在命令行中

> iterm2 打开左侧的 ~ 是 用户 目录

#### iterm2 命令

|命令|功能|
|----|----|
|`ll`|查看当前目录的文件夹级别|
|`ls`|查看当前目录的文件夹|
|`open .`|打开命令行所在目录|
|`rm -rf node_modules`|删除当前目录中的 **node_modules** 文件|
|`mkdir test`|创建 test 文件夹|
|`touch test.md`|创建 test.md 文件|
|`mv test test1`|讲 test 文件夹名字改成 test1|
|`tig`|查看 commit 提交信息， [安装 tig](https://github.com/iq9891/blog/issues/11)|
|`pwd`|查看当前路径|

#### 快捷键

|命令|功能|
|----|----|
|`cmd + d`|同标签内打开新建一个分栏 竖版|
|`cmd + shift + d`|同标签内打开新建一个分栏 横版|
|`cmd + t`|新建一个窗口切换用|
|cmd + shift + `[`( 或 `]` )|切换不同窗口
|cmd + `[`( 或 `]` )|切换同标签内的不同分栏 (cmd + shift + d 之后)|
|`cmd + 数字`|切换到数字窗口，如 cmd + 1 ， 切换到 窗口 1|
|`tab`|可以直接快速选择某一个文件，类似补全|
|`cmd + +`|放大|
|`cmd + -`|放小|
|`control + a`|光标到最前面|
|`control + e`|光标到最后面|

## git 在 o-my-zsh 中的使用

|命令|缩写|
|----|----|
|git commit|gc|
|git add|ga|
|git push|gp|
|git fetch|gf|
|git merge|gm|
|git checkout|gco|
|git status|gst|
|git diff|gd|
|git remote|gr|

### vim

|命令|缩写|
|----|----|
|`: + x`|不保存退出|
|`: + w + q`|保存退出|

### 常用的 shell 工具整理

- [tldr](https://github.com/tldr-pages/tldr) - 查看 linux命令帮助(Too long, Don't read)， usage: `tldr ssh`
- [autojump](https://github.com/wting/autojump) - 快速切换常用目录， usage: `j dir_name`
- [ag](https://github.com/ggreer/the_silver_searcher) - 搜索工具， usage: `ag '\/#\/'`
- [fuck](https://github.com/nvbn/thefuck) - 纠正工具. 上一行输入错了， usage: `fuck`, 输出正确的。
- [k](https://github.com/supercrabtree/k) - zsh 插件，需要用 zsh 的安装方式安装，brew 不起作用。命令行美化工具, 常用在git 仓库内
  ```
  ll # 原样式查看
  k  # 美化样式查看
  ```
- [so](https://github.com/ca0gu0/so) - SSH远程登录工具
- [hr](https://github.com/LuRsT/hr) - 用于在终端展示分行符
- [tcplstat](https://github.com/calvinwilliams/tcplstat) - 网络监控工具
- [cz-cli](https://github.com/commitizen/cz-cli) - git commit 工具
- [tig](https://github.com/jonas/tig) - git log 查看工具
