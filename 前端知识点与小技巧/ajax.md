#### 1.ajax

本质上是在HTTP协议的基础上以异步的方式与服务器进行通信,最关键的一步就是从服务器获得请求数据  

#### 2.ajax请求步骤

```
//1. 创建一个XMLHttpRequest对象
var xhr = new XMLHttpRequest();

//2. 设置请求行
// 第一个参数:请求方式  get/post
// 第二个参数:请求的地址 需要在url后面拼上参数列表
xhr.open("get", "01.php?name=Jepson");  //如果是post请求则不需要在URL后面添加参数

//3. 设置请求头
//请求头中可以设置Content-Type,用以说明请求主体的内容是如何编码,get请求时没有请求体,无需设置
xhr.setRequestHeader("content-type","application/x-www-form-urlencoded");

// 3. 设置请求体
xhr.send(null);  get请求
xhr.send( "name=Jepson&age=18" );  post请求


//处理请求
//给xhr注册一个onreadystatechange事件，当xhr的状态发生状态发生改变时，会触发这个事件。
xhr.onreadystatechange = function () {

  if(xhr.readyState == 4){ //响应完成
    if(xhr.status===200){  //响应成功
    //1. 获取状态行
    console.log("状态行:"+xhr.status);

    //2. 获取响应头
    console.log("所有的响应头:"+xhr.getAllResponseHeaders());
    console.log("指定响应头:"+xhr.getResponseHeader("content-type"));

    //3. 获取响应体
    console.log(xhr.responseText);

  }
}
}



```

#### 3.jsonp 的原理，有什么优缺点？

ajax请求受同源策略影响，不允许进行跨域请求，而script标签src属性中的链接却可以访问跨域的 js脚本，利用这个特性，服务端不再返回JSON格式的数据，而是返回一段调用某个函数的js代码，在src 中进行了调用，这样实现了跨域。 

####  Jsonp 优点: 

完美解决在测试或者开发中获取不同域下的数据,用户传递一个 callback 参数给服务端，然后服务端返回数据时会将这个 callback 参数作为函数名来包裹住 JSON 数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。 

#### Jsonp 缺点: 

![img](file:///C:/Users/94212/AppData/Local/Temp/msohtmlclip1/01/clip_image001.gif)

Jsonp 只支持 get 请求而不支持 post 请求,也即是说如果想传给后台一个 json 格式的数据,此时问题就来了,浏览器会报一个 http 状态码 415 错误,告诉你请求格式不正确. 