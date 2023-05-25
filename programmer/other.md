* xss 攻击是用户输入了 html 源码. 防范: 对用户输入的值进行过滤







##### node.js

* node.js  是JavaScript的后端运行环境

* 浏览器  是JavaScript的前端运行环境
  * 也就是说一段js代码可以放到浏览器中执行, 也可以放到nodejs中执行
  * 在node.js中无法调用 DOM, BOM, ajax等浏览器内置api
  * 学了node.js可以用js写后端应用, web应用/ 接口
* composer 和 npm差不多, 前者是PHP依赖工具，后者是nodejs的依赖工具，原理都是一样的。





##### docker

* 打包程序和运行环境, 把环境和程序一起发布的容器
* 其他人拿到这个包后就可以直接运行程序
* 为了解决在我的机器上可以运行, 在其他机器上就不能运行的问题



##### ci/cd





## 后端需要学习的知识

* 栈和队列
* hash表
* 进程, 线程
* 锁
* redis
  * 缓存, 减少数据库压力, 提高性能
  * 分布式锁, 解决并发冲突
  * 单点登陆, 提高用户体验
  * 排行榜
  * 计数器
  * 布隆过滤器
  * 消息队列
  * 发布订阅
* 设计模式  -- 解决一类问题的代码
  * 单例模式
  * 工厂模式
  * 观察者模式
* 高并发编程
  * 线程池
  * 锁
  * 队列
  * 并发包
  * 同步异步
  * 秒杀系统
  * 订单超卖问题

* linux

  * top 命令的参数含义
    * 系统信息浏览命令
    * 资源的占用
    * 系统的负载
    * 帮助我们锁定有问题的进程, 线程

* git

  * 上传下载
  * 工作区
  * 分支
  * 代码合并
  * 回退
  * 解决冲突

* 微服务

  * 

  





tomcat

1. [Apache](https://so.csdn.net/so/search?q=Apache&spm=1001.2101.3001.7020)和Tomcat 都是web网络服务器。

2. Apache是web服务器(静态解析，入HTML), tomcat是java应用服务器, 动态解析,比如 jsp,php





学习方式:

* 看文档, 边看边敲
* 看别人的代码
* 





1. 解压
2. 安装依赖
3. 配置

./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --enable-mbstring --with-openssl --enable-ftp --with-gd --with-jpeg-dir=/usr --with-png-dir=/usr --with-mysql=mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-pear --enable-sockets --with-freetype-dir=/usr --with-zlib --with-libxml-dir=/usr --with-xmlrpc --enable-zip --enable-fpm --enable-xml --enable-sockets --with-gd --with-zlib --with-iconv --enable-zip --with-freetype-dir=/usr/lib/ --enable-soap --enable-pcntl --enable-cli --with-curl

4. make && make install

5. cp php.ini-生产/开发 .../php/etc/php.ini

6. .../php/etc 中将php-fpm.conf.默认 改名为php-fpm.conf

7. 修改php-fpm.conf

   ​	取消 pid的分号; 用于启动php-fpm

8. .../php/etc/php-fpm.d中 将 www.conf.default.默认 改名为 www.conf

9. 建立php/bin/php的软连接/设置全局变量  用于全局访问

   in -s  

​	



/usr/local/php/sbin/php-fpm -t 测试开启php-fpm

 /usr/local/php/sbin/php-fpm

 关闭: kill -INT `cat /usr/local/php/var/run/php-fpm.pid` 

重启: kill -USR2 `cat /usr/local/php/var/run/php-fpm.pid`

![image-20221120024534491](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221120024534491.png)





















apache

* 使用 find / -name "apachectl"查找文件
  目录下执行 ./apachectl -v





开启HTTPd    service httpd start

/usr/local/httpd/bin/apxs



./configure --prefix=/usr/local/php --with-apxs2=/usr/local/httpd/bin/apxs --with-config-file-path=/usr/local/php/etc --enable-mbstring --with-openssl --enable-ftp --with-gd --with-jpeg-dir=/usr --with-png-dir=/usr --with-mysql=mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-pear --enable-sockets --with-freetype-dir=/usr --with-zlib --with-libxml-dir=/usr --with-xmlrpc --enable-zip --enable-fpm --enable-xml --enable-sockets --with-gd --with-zlib --with-iconv --enable-zip --with-freetype-dir=/usr/lib/ --enable-soap --enable-pcntl --enable-cli --with-curl





 ./configure --prefix=/usr/local/php --enable-mbstring --enable-ftp --with-gd --with-pdo-mysql=mysqlnd   --enable-zip --enable-fpm --enable-xml --enable-sockets --with-gd --with-zlib --with-iconv --enable-zip --with-freetype-dir=/usr/lib/ --enable-soap --enable-pcntl --enable-cli --with-curl

 



ervice php-fpm restart







![image-20221120162041420](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221120162041420.png)

i

![image-20221120162141723](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221120162141723.png)

###### ![image-20221120162219955](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221120162219955.png)

openat(AT_FDCWD, "/usr/local/php/bin/php-cli.ini", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/local/php/etc/php-cli.ini", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/local/php/bin/php.ini", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/local/php/etc/php.ini", O_RDONLY) = 3







 ./configure –prefix=/usr/local/php –with-config-file-path=/usr/local/php/etc –with-mysqli –with-openssl –with-gd –enable-gd-native-ttf –enable-gd-jis-conv –with-png-dir –with-jpeg-dir –with-freetype-dir –with-iconv-dir –with-zlib-dir –enable-ftp –disable-ipv6 –with-bz2 –enable-mbstring –with-libxml-dir –enable-sockets –enable-exif –disable-debug –with-mcrypt –enable-pcntl –enable-sigchild –enable-sysvmsg –enable-pdo –with-pdo-mysql –with-curl –enable-fpm
configure: error: invalid variable name: `–prefix'



./configure --prefix=/usr/local/php --with-fpm-user=www --with-fpm-group=www --with-curl --with-freetype-dir --enable-gd --with-gettext --with-iconv-dir --with-kerberos --with-libdir=lib64 --with-libxml-dir --with-mysqli --with-openssl --with-pcre-regex --with-pdo-mysql --with-pdo-sqlite --with-pear --with-png-dir --with-jpeg-dir --with-xmlrpc --with-xsl --with-zlib --with-bz2 --with-mhash --enable-fpm --enable-bcmath --enable-libxml --enable-inline-optimization --enable-mbregex --enable-mbstring --enable-opcache --enable-pcntl --enable-shmop --enable-soap --enable-sockets --enable-sysvsem --enable-sysvshm --enable-xml --enable-zip --enable-fpm --enable-cli









```
systemctl start php74-php-fpm
```
