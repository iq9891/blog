# libcrypto.so.6: cannot open shared object file

## 问题

`error while loading shared libraries: libcrypto.so.6: cannot open shared object file: No such file or directory`

## 环境

**CentOS**

## 解决方案

- `yum install libcrypto.so.6` 安装模块
- `cd /usr/lib64` 进入目录
- `ll *ssl*` 查看
- `ln -s libssl.so.1.0.1e libssl.so.6` 软链
- `ll *libcrypto*` 检测是否成功