## kratos



todo: https://go-kratos.dev/docs/guide/wire/    依赖注入









(server = controller，biz = 实际server)

* proto
  * 通过proto生成的http接口时, 一定要加google.api.http 这个option

* biz

  * ```
    GreeterUsecase   业务场景的集合
    ```

  * 服务名.go   ----   Repo 是抽象出来的数据库操作接口, 在data层实现这个接口

    ```
    type GreeterRepo interface {
    	Save(context.Context, *Greeter) (*Greeter, error)
    	Update(context.Context, *Greeter) (*Greeter, error)
    	FindByID(context.Context, int64) (*Greeter, error)
    	ListByHello(context.Context, string) ([]*Greeter, error)
    	ListAll(context.Context) ([]*Greeter, error)
    }
    ```

    

* server
  * 生成http 和grpc 的server 
  * http和grpc会挂载server都会挂载service.GreeterService



* service     
  * 里面的方法和api中的proto生成该服务的go 文件中的方法是对应的, 也就是说service中的xxxService 结构体一定要实现api中go 文件中那个定义的所有的方法.



* data 
  * data.go 连接数据库
  * greeter.go 实现biz层中 biz.GreeterRepo (type GreeterRepo interface) 中定义的数据库操作



* conf 
  * conf.proto  解析配置的]configs/config.yaml中的配置文件对应





* wire 

  * ```
    var ProviderSet = wire.NewSet(NewProductService)  // 注入实现的接口(controller)
    ```

  * ```
    var ProviderSet = wire.NewSet(NewGRPCServer, NewHTTPServer)  // 注入http, GRPC 服务
    ```





##   

