## 登陆认证流程

* session

  * 通过session id (客户端)访问到session
  * 缺点: 集群无法共享   ----- 解决用token+redis可以实现

  *  SESSION 的实现中采用COOKIE技术，SESSION会在客户端保存一个包含session_id(SESSION编号)的COOKIE；在服务器端保存其他 session变量，比如session_name等等。当用户请求服务器时也把session_id一起发送到服务器，通过session_id提取所保存在服务器端的变量，就能识别用户是谁了。同时也不难理解为什么SESSION有时会失效了。
  * 生命周期: 浏览器关闭
  * login.php

  ```
  <?php
      session_start();//启用session
  //    $user = $_GET['user'];//接收表单提交的数据
  //    $pass =$_GET['pass'];//接收表单提交的数据
      //使用apifox
      $user = $_POST['user'];//接收表单提交的数据
      $pass =$_POST['pass'];//接收表单提交的数据
      if ($user == 'lihao' && $pass == '123456') {
      $_SESSION['user'] = $user;
          header("Location:http://localhost/test/demosessionlogin/index.php");
      }else{
          echo  json_encode(['code'=>0,'msg'=>'登陆失败']);
      }
  ```

  * index.php

  ```
  <?php
      session_start();//启用session
      if (empty($_SESSION['user'])) {
          echo  json_encode(['code'=>0,'msg'=>'不能访问']);
      }else{
          echo  json_encode(['code'=>1,'msg'=>'可以访问']);
          echo '<hr>';
          var_dump($_SESSION['user']);
      }
  ```

* cookie

  * 当用户成功登录网站后，服务器会把用户信息保存到用户的cookie中，当再次访问同一个网站的其他脚本时就会携带cookie中的数据一起访问，在服务器的每一个脚本中都可以接受携带的cooike数据，不需要每次访问一个页面就重新输入一次登录者信息。
  * 生命周期 setcookie('username',$_POST['username'],time()+3600),的第三个参数
  * login.php

  ```
  <?php
  header('Content-type:text/html;charset=utf-8');//设置编码格式防止乱码
  if ($_POST['username']==='ahua' && $_POST['password']==='12345'){
      if (setcookie('username',$_POST['username'],time()+3600)){
          //将数据存入客户端
          header('Location:index.php');//跳转到成功页面
      }else{
          echo 'cokkie设置失败';
      }
  }else{
  	echo '用户名或密码错误，登录失败';
  }
  ?>
  ```

  * index.php

  ```
  <?php
  header('Content-type:text/html;charset=utf-8');//设置编码格式防止乱码
  if (isset($_COOKIE['username']) && $_COOKIE['username']==='ahua') {
  //cookie传入
      echo 'ahua欢迎回来';
  }else{
      echo '<a href="login.php">请登录</a>';
  }
  ?>
  ```

  

* token

  * 应用 token + redis
  * token类似于session id:
    * redis: key: token value: userid
    * 通过token在redis中拿到userid, 在从数据库中拿到user
    * token依赖于redis
    * 缺点每次要根据token查询真实内容, 对服务器压力较大
  
  1.前端传账号密码给后端
  
  2.后端将账号密码作处理[加密](https://so.csdn.net/so/search?q=加密&spm=1001.2101.3001.7020)生成token,并返回给前端
  
  3.前端将token存入缓存，在每次请求时，在[header](https://so.csdn.net/so/search?q=header&spm=1001.2101.3001.7020)或url中将token传给后端
  
  4.将前端传来的token与数据库账号密码生成的token作比对，相等则成功。
