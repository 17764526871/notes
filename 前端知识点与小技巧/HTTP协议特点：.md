### HTTP协议特点：

**无状态的,  多次请求之间没有相关性**

> 即同一用户请求同一网站的不同页面，服务器无法识别是否是同一用户发起的请求。因此，用户无法进行连续的业务逻辑。

如：登录，已在A页面登录，请求B页面，提示未登录。

**cookie特点**：在cookie中数据设置后，浏览器再次请求服务器指定页面时，会自动携带cookie中的数据到服务器，在服务器中可以获取cookie中的数据；

- cookie中的数据 可以被同一个网站的页面所共享
- 不同浏览器的cookie 不能共享
- cookie的数据存储在浏览器中，每次请求服务器，在请求报文中携带cookie的数据，发送给服务器
- 服务器端无法直接操作cookie，是通过在服务器端设置响应头的的方式，通知浏览器对cookie进行设置，
- cookie中的数据有效期，不设置是会话级别的, 浏览器关闭，会话结束，数据销毁
- cookie存储容量小，约4kb



- 在服务器端存储数据的容器
- session容器是一个数组的形式，通过超全局变量$_SESSION 进行取值和设置
- session在使用前，必须先 session_start 开启session 机制
- session中的数据可以被当前网站所共享
- ​


- 在服务器端存储数据的容器
- session容器是一个数组的形式，通过超全局变量$_SESSION 进行取值和设置
- session在使用前，必须先 session_start 开启session 机制
- session中的数据可以被当前网站所共享









如果用户登录成功，在服务器中记录用户的登录状态

- 执行session_start(), 生产session文件，在session文件中，记录当前用户的信息

- 通过响应头部，给浏览器的cookie设置sessionID

- if($name=='zs'&&$pwd=='666'){
    //登录成功
    session_start();
    $_SESSION['username']=$name;
  }

- 后续访问其他页面（个人中心），浏览器会自动发送cookie中存放的sessionID到服务器

- 服务器会浏览器传递根据sessionID,找到对应的session文件，查看其中是否存放有当前用户的信息

  - 是： 用户已登录 ，正常浏览

  - 否：用户未登录，跳转到登录页

  - session_start();

    if(!empty($_SESSION['username'])){
      //正常浏览
    }else{
      header('location:./04-login.html');
      die();//后面代码不执行
    }