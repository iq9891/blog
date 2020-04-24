# axios拿不到自定义的header头

用axios发送请求获取reponse header中的数据，需要提前在后台添加设置过滤器头部配置、自定义头部属性、并打开过滤器。
然后就是前端发送请求，然后获取reponse headers里面的自定义属性。然后发现获取的永远是下面的几个属性：

```
Object {
  cache-control:"private, must-revalidate",
  content-type:"application/json"
}
```

查看 Network ，发现 ajax 请求中 header 头中确实有 Authorization 字段。如果想让浏览器能访问到其他的 响应头的话：***需要在服务器上设置 Access-Control-Expose-Headers***

```
Access-Control-Expose-Headers : 'Authorization'
```

设置之后，即可好使，如下图：

![结果](https://user-images.githubusercontent.com/5716990/80055743-04f37580-8555-11ea-8e8c-5697e02e7ceb.png)