## 事务四个特性:ACID

* 原子性, 要么都做，要么都不做

* 一致性, 事 务执行的结果必须是使数据库从一个一致性状态变到另一个一致性状态。如果数据库系统 运行中发生故障，有些事务尚未完成就被迫中断，这些未完成事务对数据库所做的修改有一部分已写入物理数据库，这时数据库就处于一种不正确的状态，或者说是 不一致的状态。

* 隔离性, 个事务的执行不能其它事务干扰。

* 持续性, 也称永久性，指一个事务一旦提交，它对数据库中的数据的改变就应该是永久性的。

  

## 事务的并发问题:

（1）脏读：事务A读取了事务B更新的数据，然后B回滚操作，那么A读取到的数据是脏数据

（2）不可重复读：事务 A 多次读取同一数据，事务 B 在事务A多次读取的过程中，对数据作了更新并提交，导致事务A多次读取同一数据时，结果不一致。

（3）幻读：假设系统管理员A将数据库中所有学生的成绩从具体分数改为ABCDE等级，但是系统管理员B就在这个时候插入了一条具体分数的记录，当系统管理员A改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样，这就叫幻读。 

小结：其中不可重复读的和幻读很容易混淆，不可重复读侧重于修改，幻读侧重于新增或删除。



## mysql的四种隔离级别:

**（1）Read Uncommitted（读取未提交内容)**

没有提交的时候别人就可以读到

**（2）Read Committed（读已取提交内容）**

只有提交后, 别人才可以读出来

**（3）Repeatable Read（可重读）**解决不可重复读 两次读取内容不一致

这是mysql的默认事务隔离级别，它确保同一事务的多个实例在并发读取数据时，会看到同样的数据行。

**（4）Serializable（可串行化）**

这是最高的隔离级别，它通过强制事务排序，使之不可能相互冲突，从而解决幻读问题。简言之，它是在每个读的数据行上加上共享锁。在这个级别，可能导致大量的超时现象和锁竞争，因此使用该隔离级别会造成数据库性能的显著下降。

# ![img](https://img-blog.csdnimg.cn/6241fd4e740e442d90a65367fe4503b5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA55m955m955Sc55Sc5Yaw,size_20,color_FFFFFF,t_70,g_se,x_16)







锁:

​	悲观锁:  数据库的层次加锁的

​			for update

​	乐观锁:  相当于多加一些条件