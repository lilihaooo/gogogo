## Task6

task5 完善:

1. **用户端 jwt 登陆   ??? 角色**
2. **布局调整    ??? 不明白怎么调整**

   ?? :    将userModle下的user_coupons.go 放到couponModel中吗? 

     我觉得应该放在userModel中, 因为user是主体!!!

   ![image-20230214003606809](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20230214003606809.png)
3. 请求方式调整  **GET接口是获取数据, 不能修改状态     POST或者PUT全改或者PATCH(推荐)数据修改数据**
4. 逻辑纠正后, 相关代码纠正 usedNum  (可以领取的优惠券列表 中要显示已经领完的券)
5. 添加接口: 每个用户的优惠券列表



Task 6:

1. 领券 用redis队列实现  push pop  每秒读取10条
   1. 用户领券时将信息放入redis  list "claim_coupon"
   2. 定时任务每秒从 claim_coupon 中读取10条数据
   3. 验证
   4. 插入到mysql中,利用事务保证数据一致性, 还有乐观锁(where (total > usernum))
   5.  将执行结果 msg set到 :key requireId value:msg(成功或者失败)   前端轮询读取

