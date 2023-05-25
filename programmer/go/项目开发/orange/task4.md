## 后台管理 --- task4

* 优惠券
  1. crud
  2. 状态 更改
* 优惠卷预发
  1. crud
  2. 状态 更改
* 定时任务, 发券 (事务)
* 定时任务数据库备份
* 发放优惠券日志







## 问题

* model层:

![image-20230204111030226](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230204111030226.png)





* 划线部分的数据由来
* ![image-20230205214313993](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230205214313993.png)





* 时间类型, 绑定参数报错(将*time.TIme改为string类型)

  ![image-20230205220207903](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230205220207903.png)

  

  请求:

  {

    "coupon_id": 1,

    "num": 10,

    "start_time": "2023-02-04 19:24:30",

    "end_time": "2023-02-04 19:24:30",

    "time_point": "12:00. 17:30",

    "status": 1

  }

parsing time "\"2023-02-07 21:57:05.000000\"" as "\"2006-01-02T15:04:05Z07:00\"": cannot parse " 21:57:05.000000\"" as "T"



* 数据验证

![image-20230205230227765](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230205230227765.png)



*  日志相关

  ![image-20230206002210949](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230206002210949.png)







* 数据库备份报错

  ![image-20230206011946727](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230206011946727.png)

​							定时备份数据库脚本失败2： exit status 127





* 关于接口

  ![image-20230206014759741](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230206014759741.png)

![image-20230206014831192](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230206014831192.png)

​					这个接口提供的是id, 为什么显示的名称

​					



