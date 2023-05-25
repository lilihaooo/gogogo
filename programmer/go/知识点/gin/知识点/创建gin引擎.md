创建Gin引擎的方法有两种：

```golang
gin.Default()
gin.New()
```

gin.Default()里面调用了gin.New();在调用完gin.New()得到Engine 实例后,还调用了engine.Use(Logger(), Recovery());gin.Default()获取到的Engine 实例集成了Logger 和 Recovery 中间件

New 返回一个新的空白 Engine 实例，没有附加任何中间件。

使用gin.New()初始化Engine 实例;当收到请求后,控制台没有任何输出;