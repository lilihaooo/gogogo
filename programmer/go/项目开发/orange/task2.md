#### task2

1.golang 执行执行任务 备份数据库 1小时备份一次  生成日期时间.dump文件   github.com/robfig/cron/v3 未完成

2.数据验证  使用validator包  完成

3.文件上传 完成

4.写一个  统计每天使用DELETE请求的个数(按照不同管理员区分, 比如 完成

用户名  日期  个数

admin  2023-01-12   12
admin  2023-01-11   18
tommmm 2023-01-12   1









时间: 1天

 

5.预习 redis数据结构
redis的list使用方式

定时任务发放优惠券  领取优惠券

了解生产者  消费者模式



6.订单处理



6.统计模块 sql



7.docker 部署 Nginx linux

8.面试

9.微服务  了解





## 开发

#### todo:

```
Avatar   string `json:"avatar"` //todo 头像格式未验证
```





#### 思路:

* 统计

  SELECT username, DATE_FORMAT(created_at, '%d/%m/%y') date, count(*) count
  FROM admin_api_log
  WHERE method = "DELETE"
  GROUP BY date, username

  

* 管理员头像上传



#### 预习:

list 列表

* lpush
* llen
* lrange 0 -1所有
* lrange 0 0 第一个元素



set 无序集合

* 与list比较 list可以插入重复的语句, set不会
* sadd key value
* smembers key
* sismenbers key



zset 有序集合  可以实现热搜功能

* zadd key1 排名值 value

* zadd key1 排名值 value

* zrange key1 0 -1 
* zrevrange key1 倒序 0 -1 







#### 问题: 

* 删除管理员后, 头像要删除吗?

* ```
  // todo 打印 和logWrite的区别
  //logWrite.Error("定时备份数据库脚本失败,生成文件失败1：", err.Error())
  fmt.Println("定时备份数据库脚本失败,生成文件失败1：", err.Error())
  ```

* ```
  // todo windows上不能运行定时任务?
  cmd := exec.Command("/bin/sh", "-c", commandDump)
  ```