## php+redis实现队列

* push.php 入队列    浏览器上运行:http://localhost/test/push.php

  ```
  <?php
  //这里经过URL直接传递参数进行 keyword
  //$keyword = $_GET['keyword'];
  $keyword = 'nihao'.time();
  
  $redis = new Redis();
  $redis->connect('127.0.0.1',6379);
  $redis->auth('123456');
  try{
      echo $redis->LPUSH('list',' '.$keyword);
  }catch(Exception $e){
      echo $e->getMessage();
  }
  ```

* pop.php出队列    cmd上运行: C:\Windows\System32\cmd.exe php pop.php

  ``` 
  <?php
  //写个死循环，一直监听.net
  $redis = new Redis();
  $redis->connect('127.0.0.1', 6379);
  $redis->auth('123456');
  
  while(true) {
      try{
          $value = $redis->LPOP('list');
          //这里进行业务处理
          print_r($value);
      }catch(Exception $e){
          echo $e->getMessage();
      }
      //1秒钟执行一次
      sleep(1);
  }
  
  ```

  