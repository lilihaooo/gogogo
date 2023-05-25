## 环境配置

* yum安装

  * yum install 名称
* 查找文件/目录的位置

  * find / -name apache  
* vim 撤销

    esc :u u u 每按一次u撤销一步

    U: 撤销到编辑前

* vim 查找

  esc

  ```
  /关键字       //向下查找
  n            //表示重复查找动作，即查找下一个
  
  ?关键字       //向上查找
  N            //向上查找一个
  ```

* 重启apache服务器

    1、启动服务
    systemctl start 服务名

    2、停止服务
    systemctl stop 服务名

    3、重启服务
    systemctl restart 服务名

    4、查看服务是否已启动
    systemctl is-active 服务名

    5、查看服务的状态
    systemctl status 服务名

    6、启用开机自启动服务
    systemctl enable 服务名

    7、停用开机自启动服务
    systemctl disable 服务名

    8、查看服务是否为开机自启动
    systemctl is-enabled 服务名

    9、只重启正在运行中的服务
    systemctl try-restart 服务名

    10、显示所有的服务状态—空格翻页 q推出
    systemctl list-units --type service --all

    11、查看启动成功的服务列表
    systemctl list-unit-files|grep enabled

    12、查看启动失败的服务列表
    systemctl --failed

    13、查看所有服务的状态—空格翻页 q推出
    systemctl list-unit-files --type service