Nginx 配置文件

vim /usr/local/nginx/conf/nginx.conf

Nginx 网站根目录

/www/root





重启

nginx -s reload

开启

nginx







重启php

 







#自己配置的用于解析php, 与下面标记111的配置效果一样
if (!-e $request_filename) {
     rewrite ^/(.*)$ /index.php/$1 last;
}

location ~ .*\.php(\/.*)*$ {
     fastcgi_pass   127.0.0.1:9000;
     include       fastcgi.conf;
     fastcgi_index  index.php;
}



nginx伪静态--配置文件中

if (!-e $request_filename) {

​                         rewrite ^(.*)$ /index.php?s=$1 last;

​                         break;

​            }



启动redis

![image-20221122020638788](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221122020638788.png)





8.将redis-cli,redis-server拷贝到bin下，让redis-cli指令可以在任意目录下直接使用

　　cp /usr/local/redis/bin/redis-server /usr/local/bin/

　　cp /usr/local/redis/bin/redis-cli /usr/local/bin/

 

![image-20221122022520667](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221122022520667.png)





重启redis 强行重启

[root@iZ2vc5jhhbc58ajipyng5aZ bin]# ps -ef|grep redis
root     22594     1  0 12:42 ?        00:00:00 redis-server *:6379
root     22670 19832  0 12:44 pts/0    00:00:00 grep --color=auto redis
[root@iZ2vc5jhhbc58ajipyng5aZ bin]# kill -9 22594
[root@iZ2vc5jhhbc58ajipyng5aZ bin]# redis-server ./redis.conf 
[root@iZ2vc5jhhbc58ajipyng5aZ bin]# pwd
/usr/local/redis/bin
[root@iZ2vc5jhhbc58ajipyng5aZ bin]# 