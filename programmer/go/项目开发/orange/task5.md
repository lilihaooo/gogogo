修改之前代码

1.used_num创建时候必须为0

​																				1, 验证去掉required

![image-20230208004045260](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230208004045260.png)

2.错误信息提示能汉化(i18n)

​	label:"优惠券ID"



**3.时间格式验证**



4.admin_id必须是管理员id 验证

​						其实不用验证! 因为AdminId是jwt 获取的

![image-20230208015050228](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230208015050228.png)

**5.gorm返回时间数据格式化为  yyyy-mm-dd HH:ii:ss**



6.删除的数据在数据库在数据库里验证是否存在

![image-20230208015913527](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230208015913527.png)

7.数据库存在同样未删除优惠券名称是否存在  存在无法添加

​	时间关系未改

8.优惠券修改状态可以增加多接口,或者前端增加status参数

​	时间关系未改

9.GET接口是获取数据, 不能修改状态     POST或者PUT全改或者PATCH(推荐)数据修改数据

​	todo 学习restful规则

10.预发券num验证, coupon_id优惠券是否存在. time_point 劈开分别时间校验

![image-20230208233424520](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230208233424520.png)

11.gorm升级为v2   gorm.io

12.数据库常量值定义为一个const

**13.发券日志增加时间筛选**

​	**问题:** 筛选参数要不要验证, 原因: 参数不为空就会会进入到sql 语句中, 但是在程序中也不会报错, 单独执行sql 会报错

14.连表数据起别名

15.使用gorm 写发券的查询语句



**时间校验**

![image-20230209005936779](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230209005936779.png)





前台项目:

user

​	使用另外一个数据库 

​	登陆注册

​	**领券 mysql** 

​			问题: 参数如何传递 get post?

​		日期格式可以这样判断

![image-20230211165536975](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230211165536975.png)

​	**// 领券 队列redis**

​	**有效时间**





**学习restful规则**

