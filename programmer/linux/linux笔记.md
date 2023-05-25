# Linux 学习笔记

## 命令

##### 语法: 命令	[-选项]	[参数]

* clear 清屏

  

* ls 显示目录
  * -l 长格式 lang
  * -a 所有包括隐藏文件 (.开头的文件)
  * -R 递归展示
  * 参数可以为 /, 等某个目录
    * ls -a /lihao 查看/lihao中的所有文件

  * 组合使用
    * ls -al 所有文件长格式显示

* ls -ah 显示隐藏文件



##### 操作文件

* cd

* pwd 显示当前目录

* cd ~    或者 cd    回家

  

* touch

  * 文件不存在: 创建
  * 文件存在: 修改文件的创建时间
  * touch aa.txt bb.txt cc.txt 同时创建

* mkdir

  * 创建目录
  * mkdir aa bb
  * mkdir -p 递归创建

* cp 

  * 复制文件或者目录
  * cp 文件 [文件2] 目录
  * cp 目录 目录    要求目录为空
  * cp -人目录 目录   递归处理

  

##### 编辑/查看文件

* vi
* cat
  * cat 文件地址



## 学习路线







## 知识点

多用户管理方式的

* 默认 root 密码 ?
* root 超级管理员
* 符号
  * 超级管理员 #
  * 普通 $ 自能操作自己的文件



目录结构

![image-20221103002811916](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20221103002811916.png)





注意

* 区分大小写
* tab 自动补全





remdir 删除目录





* 防火墙
  * firewall-cmd --state 防火墙状态
  * service firewalld stop 关闭防火墙
  * service firewalld start





* 安装文件

  比如make install一般表示进行安装，make uninstall 是卸载，不加参数就是默认的进行源代码编译。





* gcc
  * linux中的gcc是由GNU推出的一款功能强大的、性能优越的多平台编译器。gcc编译器能将C、C++语言源程序和目标程序编译、连接成可执行文件。
