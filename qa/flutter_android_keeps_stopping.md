# flutter android keeps stopping

## 环境

- mac catalina 10.15.5
- flutter 1.17.3
- dart 2.8.4
- vs code 1.45.1
- 安卓模拟器 Pixel 3a XL API 29
- flutter 应用名字 [first_flutter](https://github.com/iq9891/first_flutter)

# 问题

最近修改 Android 启动图片，在网上海搜了很多解决方案，在 [launch_background.xml](https://github.com/iq9891/first_flutter/blob/master/android/app/src/main/res/drawable/launch_background.xml) 中配置如下代码：

```
<?xml version="1.0" encoding="utf-8"?>
<!-- Modify this file to customize your launch splash screen -->
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@android:color/white" />
    <item name="android:windowFullscreen">true</item>
    <item name="android:windowDrawsSystemBarBackgrounds">false</item>
    <!-- You can insert your own image assets here -->
    <item>
        <bitmap
          android:gravity="center"
          android:src="@mipmap/launch_image"
        />
    </item>
</layer-list>
```

启动安卓的时候就报错了报错如下： 

```
first_flutter keeps stopping
```

截图如下：

![flutter android keeps stopping](https://user-images.githubusercontent.com/5716990/83975308-c871b280-a925-11ea-83e8-d6f2e63f4420.jpg)

解决方案：

对比新建的 flutter 项目，发现下面两句不生效导致的安卓报错，去掉即可

```
<item name="android:windowFullscreen">true</item>
<item name="android:windowDrawsSystemBarBackgrounds">false</item>
```
