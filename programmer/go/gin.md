```
// 获取get参数的方式
func (c *gin.context) Query(key string) string
func (c *gin.context) DefaultQuery(key, Default string) string
func (c *gin.context) GetQuery(key string) string (string bool)
```



```
// 获取post参数
func (c *gin.context) PostFrom(key string) string
```

