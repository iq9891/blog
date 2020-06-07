# flutter android 启动图撑满屏幕

## 问题

怎么让配置的安卓启动图片撑满屏幕？ 原来的代码如下

```
<bitmap
  android:gravity="center"
  android:src="@mipmap/launch_image"
/>
```

## 解决

去掉 `android:gravity="center"` 代码即可

```
<bitmap
  android:src="@mipmap/launch_image"
/>
```