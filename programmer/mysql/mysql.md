## mysql

#### TODU

1. 建立索引
2. 

#### 增删改查

insert into student (name, sex, age) values ('lihao', 1, 18)

update student  set  name = 'lihao1', age = 26 where id = 2

delete from  student where id = 1

select name, age from student where id = 10 



## sql优化

1. 优化sql语句
   * 需要哪些字段就查询哪些字段
2. 使用索引
3. 优化表结构
4. 优化储存引擎
5. 优化服务器参数
6. 使用缓存
7. 合理分配内存
8. 合理分配磁盘空间
9. 合理设置事务的隔离级别
10. 合理使用储存过程



## 索引

#### 种类

1. 主键索引
2. 普通索引: 普通索引适用于查询条件中的等值查询,可以有重复值和空值
3. 唯一索引: 用于确保字段的唯一性
4. 全文索引: 用于文本搜索
5. 复合索引: 用于多个字段的组合查询
6. 空间索引: 用于空间数据查询

#### 分类

1. 单列索引

2. 组合索引

   * 最左原则  将选择性最高的字段放在最右边

     ```
     mysql> select count(DISTINCT staff_id) / count(*) AS staff_id_selectivity, count(DISTINCT customer_id) / count(*) AS customer_id_selectivity, count(*) from payment\G;
     *************************** 1. row ***************************
        staff_id_selectivity: 0.0005
     customer_id_selectivity: 0.0500
                    count(*): 10000000
     1 row in set (6.29 sec)
     ```

   * 组合索引失效

     ```
     生效的规则是：从前往后依次使用生效，如果中间某个索引没有使用，那么断点前面的索引部分起作用，断点后面的索引没有起作用； 比如
     
     where a=3 and b=45 and c=5 .... 这种三个索引顺序使用中间没有断点，全部发挥作用；
     where a=3 and c=5... 这种情况下b就是断点，a发挥了效果，c没有效果
     where b=3 and c=4... 这种情况下a就是断点，在a后面的索引都没有发挥作用，这种写法联合索引没有发挥任何效果；
     where b=45 and a=3 and c=5 .... 这个跟第一个一样，全部发挥作用，abc只要用上了就行，跟写的顺序无关（a,b,c）多列索引使用的示例，说明：（a,b,c）组合索引和(a,c,b）是不一样的
     ```

   * 案例

     ```
     给tabel加上了(a,b,c)组合索引
     (0)    select * from mytable where a=3 and b=5 and c=4;
     abc三个索引都在where条件里面用到了，而且都发挥了作用
     (1)    select * from mytable where  c=4 and b=6 and a=3;
     这条语句列出来只想说明 mysql没有那么笨，where里面的条件顺序在查询之前会被mysql自动优化，效果跟上一句一样
     (2)    select * from mytable where a=3 and c=7;
     a用到索引，b没有用，所以c是没有用到索引效果的
     (3)    select * from mytable where a=3 and b>7 and c=3;
     a用到了，b也用到了，c没有用到，这个地方b是范围值，也算断点，只不过自身用到了索引
     (4)    select * from mytable where b=3 and c=4;
     因为a索引没有使用，所以这里 bc都没有用上索引效果
     (5)    select * from mytable where a>4 and b=7 and c=9;
     a用到了  b没有使用，c没有使用
     (6)    select * from mytable where a=3 order by b;
     a用到了索引，b在结果排序中也用到了索引的效果，前面说了，a下面任意一段的b是排好序的
     (7)    select * from mytable where a=3 order by c;
     a用到了索引，但是这个地方c没有发挥排序效果，因为中间断点了，使用 explain 可以看到 filesort
     (8)    select * from mytable where b=3 order by a;
     b没有用到索引，排序中a也没有发挥索引效果
     ```







#### 数据库连接池:

​	多个线程去抢夺一个连接的话, 性能低.

​	每个线程去创建,或者销毁一个连接的话, 建立网络连接很耗时.

​	连接池的好处:

​	一批建立好的连接放在池子里, 用的时候去池子中拿, 不用的是由还到池子中, 解决了频繁创建和销毁连接的问题

​	常见的数据库连接池有DBCP，C3P0，Druid，等等，





#### 事务:

事务没有提交只是修改了内存中的数据, 磁盘中的数据没有被修改

事务没有提交系统宕机了, 对磁盘中的数据没有被修改, 恢复后还是原理的数据

