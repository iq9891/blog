# Mac 命令行登录 Linux 无需密码的配置

## 正常的命令行登录

```
ssh 用户名@192.168.1.XXX
```

之后还得输入密码，那么如何不输入密码快捷键搞定呢？

## 无需密码的命令行登录配置

1. 编写 `login.exp` 文件，内容如下： 

```
#!/usr/bin/expect

set timeout 30
spawn ssh [lindex $argv 0]@[lindex $argv 1] -p [lindex $argv 3]
expect {
	"(yes/no)?"
	{send "yes\n";exp_continue}
	"password:"
	{send "[lindex $argv 2]\n"}
}
interact
```

2. 将 `login.exp` 放到 `/usr/local/bin/` 目录下
3. 使用

- 点击 iTerm2 -> preferences -> profiles
- 点击左下的 `+`
- 编辑 Name 快捷键(Shortcut key)
- 在 `Send text at start` 中 `login.exp 用户名 ip 密码 端口` ， 如 `login.exp iq9891 192.168.1.XXX 123 22`
- 退出，然后按快捷键测试，完成