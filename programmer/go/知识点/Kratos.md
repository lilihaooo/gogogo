## kratos

#### 项目结构

* api    ---   维护了微服务使用 proto文件,以及根据proto文件生成的 go 文件

  * .proto IDL文件

  * .go 利用protoc工具生成的go文件, 包括http和grpc的服务相关代码

  * .swagger.json 利用工具生成的swogger接口的文档

    ​	**尽可能去去区分原始的IDL文件和生成的.go和.swagger.json文件**

    ​	开发者更聚焦于原始IDL文件的编写

    ​	有利于IDL文件的传播 -proto文件可以快速生成其语言代码, 独立文件夹更有利于扩散给外部调用者

* cmd

  * 整个项目的入口文件
  * wire.go   维护依赖注入

* internal/biz

  * internal里的业务只能由本项目调用, 不会暴露给外部

  * biz 被理解为业务逻辑的组装层, 关键词: 业务逻辑, 组装层

    * 业务逻辑: 包括但不限于, 会处理很多进阶的内容, 例如:
      * 复合对象的操作, 如操作对象A后, 再操作B
      * 特殊逻辑, 如创建失败时, 等待10s再创建
      * 并发策略, 如并发访问对象A和对象B

    * 组装层: 重点在于组装底层基础的代码, 如CRUD, 而不是biz层直接去操作数据库等

      整体来说, biz这一层应该重点考虑业务逻辑的信息密度, 让业务开发者的重大放在这一层, 把基础实现往下沉

* internal/data
  * data被理解为缓存与数据库的封装, 与底层数据存储相关, 一般跟着数据库类型适配
  
* internal/server
  * http和grpc实例的创建和配置
  * 前面IDL文件(protobuf)生成了RPC方法的接口(interface), 这里就是RPC方法的具体实现
  
* inernal/service 
  * 实现了 api 定义的服务层
  
  * 数据结构的处理层, 处理 DTO 到 biz 领域实体的转换(DTO -> DO)，同时协同各类 biz 交互，但是不应处理复杂逻辑
  
    





##### 串联:

api 接口, 定义了要实现哪些方法

server相当于handler, 对api的具体实现

service, 对请求的数据结构进行转换

biz 业务逻辑

data 操作数据库, redis...