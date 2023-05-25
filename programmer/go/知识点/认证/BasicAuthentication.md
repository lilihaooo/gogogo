##  Http 基本认证

也叫 Basic Authentication 

桌面应用程序一般不会使用cookie而是把"用户名+冒号+密码"用BASE64算法加密后的字符串放在http request 中的header Authorization中发送给服务端, 这种方式叫做Http基本认证, 当浏览器访问使用基本认证的网站的时候, 浏览器会提示你输入用户名和密码, 如果错误的话就返回401

