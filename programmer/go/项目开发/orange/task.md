# golang学习

学习golang项目， 学习过程中掌握软件开发，做到独立开发项目

#### task1

- [ ] 管理员登录、管理员退出、管理员列表增删改查
- 数据表关键字段: 用户名、密码、手机号、邮箱
- 业务要求：支持记录筛选列表、**支持删除管理员后，已登录管理员无法发送 请求、请求日志记录**
- 代码要求：jwt、cors、validate、redis、mysql、路由群组





总结知识点:



## 疑问

---------------------

初始化数据库时这段什么意思?

```
for key, configVal := range settings {
   c := configVal.(map[string]interface{})
   config := getConfig(c)
   conn := newConn(config)
   // todo 最大连接要设置成mysql最大时长的一半
   conn.DB().SetConnMaxLifetime(time.Minute)
   if db.Connections == nil {
      db.Configs = make(map[string]Config)
      db.Connections = make(map[string]Conn)
   }
   //db.LogMode(true)
   db.Configs[key] = config
   db.Connections[key] = conn
}
```



--------------------------

#### github.com/toorop/gin-logrus使用方法总结, 学习方法

------------



字段验证和去除空格是否应该放在handler中?

----------------------

```go  
//todo update
为什么update时用到
conn.Unscoped().Save(&adminDb) UpdateColumn("", "")  UpdateColumns()  gorm.io 去看一下
```



------

日志相关的疑问

// todo log





-----

```
// todo count是否应该放在where 后面
db.Count(&count)
```



---

```
// todo  为什么这里要用一个函数返回 不直接用
func NewAdminApiLogModel() AdminApiLog {
   return AdminApiLog{}
}
```





---

两个日志文件

两个jwt中间件



----

redis 连接池子什么意思? 为什么不直接连接



后台项目不需要登陆日志, 不需要加入redis



## GET的知识点

* 如果时get传入多个参数, 可以放到一个map[string]interface{}中

* 中间件 洋葱模型 (递归调用), 第一个中间的中的text后面的代码最后执行

  * next（）顾名思义就是挂起继续向下走，然后执行完成下面的函数，会反过来最后执行该中间件

    abort（）顾名思义就是终止的意思，也就是说执行该函数，会终止后面所有的该请求下的函数。

* validate使用方法2

  * 结构体加标签

  * ```
    validation.Field(
       &m.Username,
       validation.Required.Error("用户名不得为空"),
       validation.Length(1, 50).Error("名称为1-50个字母或数字")),
    ```

  





## todo

练习接口

redis conn中写死了
