# Running Gradle task 'assembleDebug' Forever

## 问题

运行 安卓 模拟器的时候 `Running Gradle task 'assembleDebug' Forever` 一直在跑，很慢很慢。

## 解决

打开目录 `android/app/build.gradle` 文件中 `compileSdkVersion` 字段都设置为最新 SDK 版本，当前是 29 。设置之后速度飞快。