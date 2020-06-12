# Trying to embed a platform view but the PrerollContext does not support embedding

## 环境

* [Dart](https://www.dartcn.com/) 2.8.4
* [Flutter](https://flutter.cn/) 1.17.3
* macOS Catalina 10.15.5
* vs code 1.46.0

# 问题

iOS 模拟的时候，vs code 控制台抛出： `Trying to embed a platform view but the PrerollContext does not support embedding`

![image](https://user-images.githubusercontent.com/5716990/84481651-f873d980-acc8-11ea-973a-1adb88f39241.png)


# 解决方案

1. 在 `ios/Runner/Info.plist` 中，添加如下代码：

```
<key>io.flutter.embedded_views_preview</key>
<true/>
```

2. 重启 vs code 和 模拟器，即可生效

