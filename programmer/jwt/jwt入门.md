## jwt

#### 理解

​	jwt 就是通过对称加密, 把用户id加密成jwt_token存到客户端, 每次请求携带这jwt_token, 服务器直接解码;

* 使用场景: 授权认证

  * 一旦用户登录, 后续每一个请求都包含了jwt, 系统在每次处理请求之前, 都要进行jwt安全验证, 通过后在进行处理

    

* 组成

  * header 描述签名中的加密算法

  ```
  {
  	'typ': JWT,  //类型
  	'alg': 'HS256'  //payload加密算法
  }
  base64编码后构成第一部分
  ```

  * Payload  载荷

  ```
  {
  	'id': '333',
  	'name': 'lihao'
  }
  注意: 不能存放敏感的数据: 手机号码, 密码...
  base64编码后构成第二部分
  ```
  
  * 签名
  
  ```
  将base64加密后的header和加密后的payload用.拼接, 在利用header中的算法进行加密
  ```
  
  作用: 防止篡改payload中的数据!!!





md5: 单向加密算法 , 无法解密;

jwt缺点: 一旦生成无法修改(例如有效期90天, 无法提前过期)

​	建议, 时间有效时间设置短一些; 

注销: 浏览器清除cookie, 但是jwt还是可以使用