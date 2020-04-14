# No Xcode or CLT version detected

## 问题

```
gyp: No Xcode or CLT version detected!
gyp ERR! configure error
gyp ERR! stack Error: `gyp` failed with exit code: 1
gyp ERR! stack     at ChildProcess.onCpExit (/Users/lee/lee/lib/vue/vue-cli/node_modules/node-gyp/lib/configure.js:351:16)
gyp ERR! stack     at ChildProcess.emit (events.js:193:13)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:255:12)
gyp ERR! System Darwin 19.2.0
gyp ERR! command "/Users/lee/.nvm/versions/node/v11.15.0/bin/node" "/Users/lee/lee/lib/vue/vue-cli/node_modules/.bin/node-gyp" "rebuild" "--release"
gyp ERR! cwd /Users/lee/lee/lib/vue/vue-cli/node_modules/fibers
gyp ERR! node -v v11.15.0
gyp ERR! node-gyp -v v5.0.5
gyp ERR! not ok
node-gyp exited with code: 1
Please make sure you are using a supported platform and node version. If you
would like to compile fibers on this machine please make sure you have setup your
build environment--
Windows + OS X instructions here: https://github.com/nodejs/node-gyp
Ubuntu users please run: `sudo apt-get install g++ build-essential`
```

## 复现步骤

更新 XCode 之后，重新用 yarn 安装依赖

## 问题

遇到问题，首先执行 `sudo xcode-select --install` ，但是并没有成功，报错如下：

``` 
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

上面的问题是因为已经安装了，所以得先执行 `sudo rm -rf /Library/Developer/CommandLineTools`

## 完整解决步骤

1. `sudo rm -rf /Library/Developer/CommandLineTools`
2. `xcode-select --install`
