# 从零开始搭建前端脚手架

Vue.js 是目前比较流行的前端框架之一，那么开发一个基于 Vue.js 的组件是每个前端的心愿。在每次开发新的 Vue.js 组件的时候，都会做的事情有下面几项：
  - 创建项目目录
  - git 初始化
  - npm 初始化
  - 搭建开发环境
    - 语法检测
    - 代码编译
    - 代码打包
    - 本地预览及热重载
  - 搭建生产环境
    - 语法检测
    - 代码编译
    - 代码打包及压缩
  - 持续集成的配置

那么为什么不把这些工作有效的提炼出来，让他一键生成呢？目前一键生成的工具有很多，如 [yeoman](http://yeoman.io/) 等。yeoman 搭建项目需要提供 yeoman 的脚手架包 。 yeoman 的脚手架包本质上就是一个具备完整文件结构的项目样板，用户需要手动地把这些脚手架包下载到本地，然后 yeoman 就会根据这些脚手架包自动生成各种不同的项目。

yeoman 固然好用，但总是多了一步很是麻烦，还得下载脚手架包。市面上还流行 cli 技术，就是针对远程仓库的模板根据一些配置拉取到本地。显然 cli 的模式很好，不用下载就可以。我们依据这个原理自己搭建了一款叫做 [fecli](https://github.com/fe6/fecli) 的脚手架。

## 技术栈

- 开发环境： OS X El Capitan 10.11.6
- 开发工具： [Atom](https://atom.io)
- [Node.js](https://nodejs.org)：整个脚手架的运行环境。本脚手架的 Node.js 版本： 9.11.1 。
- [es6](http://es6.ruanyifeng.com)： JavaScript 的新语法。
- [commander](https://www.npmjs.com/package/commander)：TJ大神开发的工具，能够更好地组织和处理命令行的输入。本脚手架的 commander 版本： 2.15.1 。
- [co](https://www.npmjs.com/package/co)：异步流程控制工具。本脚手架的 co 版本： 4.6.0 。
- [co-prompt](https://www.npmjs.com/package/co-prompt)：分步接收用户的输入。本脚手架的 co-prompt 版本： 1.0.0 。
- [chalk](https://www.npmjs.com/package/chalk)：色彩丰富的终端工具。本脚手架的 chalk 版本： 2.3.2 。
- [ora](https://www.npmjs.com/package/ora)：典雅的终端微调器，可以控制终端输出。本脚手架的 ora 版本： 2.0.0 。

## 项目核心

一张图说明整体的架构。⤵️

![fecli 架构图](https://raw.githubusercontent.com/iq9891/blog/master/img/fecli.png)

### 关于模板

**模板** 就是未来拉取下来的东西。这个模板里往往会有一些环境的配置，语法检测的配置，单元测试的配置，持续集成的配置等。

模板的相关信息会存放在 **templates.json** 文件中。用户也可以通过一些命令操作 **templates.json** 中的内容。

### 脚手架的文件结构

``` bash
.
├── bind/                     # 运行命令的入口文件
│   └── ...
├── lib/                      # 核心代码
│   ├── table.js              # 模板列表表格形式的封装
│   ├── tip.js                # 终端提示信息的封装
│   ├── cli/                  # 命令管理
│   │   └── ...
│   └── cmd/                  # 命令操作
│   │   └── ...
├── public/                   # 命令预览
│   └── ...
└── templates.json            # 模板管理
```

## 配置全局使用

新建一个目录 `mkdir fecli` ，并进入 `cd fecli` 。然后 npm 初始化一下 `npm init` 。 为了可以全局使用，我们需要在 **package.json** 里面设置一下：

```
"bin": {
  "fe": "./bin/fe.js"
},
```

本地调试的时候，在项目根目录下执行： `npm link` 。
即可把 **fecli** 命令绑定到全局，以后就可以直接以 **fe** 作为命令开头。

## 入口文件的设置

在 package.json 里面写入依赖并执行 `npm install` 或者 `yarn install`：

```
"dependencies": {
  "chalk": "^2.3.2",
  "co": "^4.6.0",
  "co-prompt": "^1.0.0",
  "commander": "^2.15.1",
  "ora": "^2.0.0"
}
```

在根目录下建立 **\bin** 文件夹，在里面建立一个 [`fe.js`](https://github.com/fe6/fecli/blob/master/bin/fe.js) 文件。这个 **bin/fe.js** 文件是整个脚手架的入口文件，所以我们首先对它进行编写。

首先是一些初始化的代码，很简单就是引用了一下命令管理的文件([lib/cli/index.js](https://github.com/fe6/fecli/blob/master/lib/cli/index.js))：

```
require('../lib/cli/');
```


## 命令管理 ([lib/cli/index.js](https://github.com/fe6/fecli/blob/master/lib/cli/index.js))

首先是一些初始化的事情：

```
const program = require('commander');
const packageInfo = require('../../package.json');


program
    .version(packageInfo.version)
```

我们通过 **commander** 来设置不同的命令。 **command** 方法是设置命令的名字。 **description** 方法是设置描述。 **alias** 方法是设置简写。 **action** 方法是设置回调。

```
program
    .command('init') // fe init
    .description('生成一个项目')
    .alias('i') // 简写
    .action(() => {
      require('../cmd/init')();
    });

program
    .command('add') // fe add
    .description('添加新模板')
    .alias('a') // 简写
    .action(() => {
      require('../cmd/add')();
    });

program
    .command('list') // fe list
    .description('查看模板列表')
    .alias('l') // 简写
    .action(() => {
      require('../cmd/list')();
    });

program
    .command('delete') // fe delete
    .description('删除模板')
    .alias('d') // 简写
    .action(() => {
      require('../cmd/delete')();
    });
```

如果没有参数，运行帮助方法。接下来是解析 program.args 中的参数：

```
program.parse(process.argv);

if(!program.args.length){
  program.help()
}
```

运行 `fe` 之后的结果：

![运行 fe 结果](https://raw.githubusercontent.com/iq9891/blog/master/img/fecli-pre.png)

**commander** 的具体使用方法在这里就不展开了，可以直接到[官网](https://github.com/tj/commander.js/)去看详细的文档。


## 处理用户输入

在项目根目录下建立 **/lib/cmd** 文件夹，专门用来存放命令处理文件。
在根目录下建立 **templates.json** 文件并写入如下内容，用来存放模版信息：

```
{"tpl":{}}
```

### 添加模板 (`fe add`)

>进入 /lib/cmd 并新建 [add.js](https://github.com/fe6/fecli/blob/master/lib/cmd/add.js) 文件。

```
'use strict'
const co = require('co');
const prompt = require('co-prompt');
const fs = require('fs');

const table = require('../table');
const tip = require('../tip');
const tpls = require('../../templates');

const writeFile = (err) => {
  // 处理错误
  if (err) {
    console.log(err);
    tip.fail('请重新运行!');
    process.exit();
  }

  table(tpls);
  tip.suc('新模板添加成功!');
  process.exit();
};

const resolve = (result) => {
  const { tplName, gitUrl, branch, description, } = result;
  // 避免重复添加
  if (!tpls[tplName]) {
    tpls[tplName] = {};
    tpls[tplName]['url'] = gitUrl.replace(/[\u0000-\u0019]/g, ''); // 过滤unicode字符
    tpls[tplName]['branch'] = branch;
    tpls[tplName]['description'] = description;
  } else {
    tip.fail('模板已经存在!');
    process.exit();
  };

  // 把模板信息写入templates.json
  fs.writeFile(__dirname + '/../../templates.json', JSON.stringify(tpls), 'utf-8', writeFile);
};

module.exports = () => {
  co(function *() {
    // 分步接收用户输入的参数
    const tplName = yield prompt('模板名字: ');
    const gitUrl = yield prompt('Git https 链接: ');
    const branch = yield prompt('Git 分支: ');
    const description = yield prompt('模板描述: ');
    return new Promise((resolve, reject) => {
      resolve({
        tplName,
        gitUrl,
        branch,
        description,
      });
    });
  }).then(resolve);
};
```

### 删除模板 (`fe delete`)

>进入 /lib/cmd 并新建 [delete.js](https://github.com/fe6/fecli/blob/master/lib/cmd/delete.js) 文件。

```
'use strict'
const co = require('co');
const prompt = require('co-prompt');
const fs = require('fs');

const table = require('../table');
const tip = require('../tip');
const tpls = require('../../templates');

const writeFile = (err) => {
  if (err) {
    console.log(err);
    tip.fail('请重新运行!');
    process.exit();
  }
  tip.suc('新模板删除成功!');

  if (JSON.stringify(tpls) !== '{}') {
    table(tpls);
  } else {
    tip.info('还未添加模板!');
  }

  process.exit();
};

const resolve = (tplName) => {
  // 删除对应的模板
  if (tpls[tplName]) {
    delete tpls[tplName];
  } else {
    tip.fail('模板不经存在!');
    process.exit();
  }

  // 写入template.json
  fs.writeFile(__dirname + '/../../templates.json', JSON.stringify(tpls), 'utf-8', writeFile);
};

module.exports = () => {
  co(function *() {
    // 分步接收用户输入的参数
    const tplName = yield prompt('模板名字: ');
    return new Promise((resolve, reject) => {
      resolve(tplName);
    });
  }).then(resolve);
};
```

### 初始化项目 (`fe init`)

>进入 /lib/cmd 并新建 [init.js](https://github.com/fe6/fecli/blob/master/lib/cmd/init.js) 文件。

```
'use strict'
// 操作命令行
const exec = require('child_process').exec;
const co = require('co');
const ora = require('ora');
const prompt = require('co-prompt');

const tip = require('../tip');
const tpls = require('../../templates');

const spinner = ora('正在生成...');

const execRm = (err, projectName) => {
  spinner.stop();

  if (err) {
    console.log(err);
    tip.fail('请重新运行!');
    process.exit();
  }

  tip.suc('初始化完成！');
  tip.info(`cd ${projectName} && npm install`);
  process.exit();
};

const download = (err, projectName) => {
  if (err) {
    console.log(err);
    tip.fail('请重新运行!');
    process.exit();
  }
  // 删除 git 文件
  exec('cd ' + projectName + ' && rm -rf .git', (err, out) => {
    execRm(err, projectName);
  });
}

const resolve = (result) => {
  const { tplName, url, branch, projectName, } = result;
  // git命令，远程拉取项目并自定义项目名
  const cmdStr = `git clone ${url} ${projectName} && cd ${projectName} && git checkout ${branch}`;

  spinner.start();

  exec(cmdStr, (err) => {
    download(err, projectName);
  });
};

module.exports = () => {
 co(function *() {
    // 处理用户输入
    const tplName = yield prompt('模板名字: ');
    const projectName = yield prompt('项目名字: ');

    if (!tpls[tplName]) {
      tip.fail('模板不存在!');
      process.exit();
    }

    return new Promise((resolve, reject) => {
      resolve({
        tplName,
        projectName,
        ...tpls[tplName],
      });
    });
  }).then(resolve);
}
```

### 显示模板列表 (`fe list`)

>进入 /lib/cmd 并新建 [list.js](https://github.com/fe6/fecli/blob/master/lib/cmd/list.js) 文件。

```
'use strict'
const table = require('../table');

module.exports = () => {
  table(require('../../templates'));
  process.exit();
};
```

现在我们的 **fecli** 脚手架工具已经搭建好了，一起来尝试一下吧！

## 使用测试

- `fe add` 添加模板

![fe add 运行结果](https://github.com/fe6/fecli/raw/master/public/add.gif)

- `fe delete` 添加模板

![fe delete 运行结果](https://github.com/fe6/fecli/raw/master/public/delete.gif)

- `fe list` 添加模板

![fe list 运行结果](https://github.com/fe6/fecli/raw/master/public/list.gif)

- `fe init` 添加模板

![fe init 运行结果](https://github.com/fe6/fecli/raw/master/public/init.gif)

## 项目源码

更多源码信息请移步 [fecli](https://github.com/fe6/fecli) 。
