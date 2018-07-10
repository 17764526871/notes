# 选择器

 ## 关系选择器

​	E + F  选择E元素后面的第一个元素 并且这个元素是F元素 

​	E ~ F  选择E元素后面所有的F兄弟元素

## 属性选择器

​        [attr^="val"] 从头匹配属性为attr值为val的元素

​	[attr$="val"] 从尾匹配属性为attr值为val的元素

​	[attr*="val"]从任意位置匹配属性为attr值为val的元素

## 伪类选择器
### child系列语法

需求: 从相同的元素筛选出第一个或者最后一个或者倍数为几的某一些元素

​    	E:nth-child() 选择第几个孩子 并且为E的元素

​	nth-of-type() 选择第几个E元素

​	N元素从0开始逐次加1

​	:focus

​	:checked

​	:disabled

​	:enabled
## 伪元素选择器

​	:before

​	:after

​	::first-letter

​	::first-line

​	::selection

### 其他伪类选择器
```
:of-type系列，  用法与child系列很像，但是找的是子元素中对应类型			
	区别：兄弟元素不是一种类型的情况下：
	E:nth-child(n)  获取第n个元素 并且类型必须是E
	E:nth-of-type(n)  获取第n个E元素 
:focus    查找获取到焦点的文本框
:checked 获得选中的checkbox
:disabled 获得不可用的框
:enabled 获得可用的框
:not(selector)选择不匹配selector的那些元素
:target  获取当前活跃的锚链接
```

​	```
::first-letter  :获取元素的第一个字符
::first-line   :获取元素的第一行
::selection   ：获取选中的元素
```

# css3阴影

## 文字阴影
```
text-shadow: X轴偏移 Y轴偏移 羽化大小 颜色  
```
阴影可以写多个，中间用逗号隔开

## 盒子阴影
```
box-shadow: X轴偏移 Y轴偏移 羽化大小 阴影大小 颜色 内外阴影
```
## 边框图片
```
border-image：值
简写：border-image:url('border.png') 26 round;
```
# 渐变

## 线性渐变

> linear-gradient指沿着某条直线朝一个方向产生的渐变效果。

线性渐变的核心：

+ 渐变的方向
+ 颜色
【演示：渐变-线性渐变.html】

【演示：导航按钮.html】

【案例：渐变-案例-发廊效果.html】
## 径向渐变

> radial-gradient指从一个中心点开始沿着四周产生渐变效果

径向渐变的核心：

+ 圆的大小
+ 圆心的位置
+ 颜色

```css
/*1. 最简单的渐变*/
background-image: radial-gradient(red, green);

/*2. 指定圆的半径和圆心*/
background-image: radial-gradient(200px at center, red, green);

/*3. 指定椭圆*/
background-image: radial-gradient(200px 80px at center, red, green);

/*4. 指定范围*/
background-image: radial-gradient(200px at center, green 50%, red 50%);

```

【演示：径向渐变-语法.html】

【案例：径向渐变-立体小球.html】
# 过渡

## 过渡的属性
```css
/*transition-property：设置过渡属性
/*也可以是width,height*/
transition-property:all;

/*transition-duration:设置过渡时间*/
transition-duration:1s;

/*transition-delay：设置过渡延时*/
transition-delay:2s;

/*transition-timing-function:设置过渡的速度*/
/*linear，ease，ease-in，ease-out，ease-in-out， steps(10)*/
transition-timing-function:linear;
```
## 属性合写

```css
/* 属性 时间 延时 速度 */
transition: width 1s 3s linear;
```

【案例：手风琴效果】
# 2D转换
> transform: 转换，是CSS3最具颠覆性的几个特性之一，既可以用于2D转换，也可以用于3D转换。
>
> transform：2D转换，元素在平面上实现移动、旋转、缩放、斜切等操作
## scale缩放

```css
transform: scaleX(0.5);/*让宽度变化*/
transform: scaleY(0.5);/*让高度变化，注意不能写多个transform，不然会覆盖。*/
transform: scale(0.5);/*让宽度和高度同时变化*/
```
## translate平移

```javascript
transform: translateX(100px);
transform: translateY(100px);
transform: translate(100px, 100px);
transform: translate(50%, 50%);
```
## rotate旋转

```javascript
transform: rotate(360deg);//旋转360度
transform: rotate(-360deg);//逆时针旋转360度
```

注意：

- 单位是deg，角度，不是px
- 正值顺时针转，负值逆时针转
- 可以通过transition-origin设定旋转原点

/*transition-property：设置过渡属性
/*也可以是width,height*/
transition-property:all;

/*transition-duration:设置过渡时间*/
transition-duration:1s;

/*transition-delay：设置过渡延时*/
transition-delay:2s;

/*transition-timing-function:设置过渡的速度*/
/*linear，ease，ease-in，ease-out，ease-in-out， steps(10)*/
transition-timing-function:linear;

## skew斜切(变形)

> skew在实际开发中，是用的最少的一个属性。一般来说，x和y只会倾斜其中的一个

```javascript
/*在水平方向倾斜30deg*/
transform: skewX(30deg);
/*在垂直方向倾斜30deg*/
transform: skewY(30deg);
```
## transform-origin转换原点

> 通过transform-origin可以设置转换的中心原点。

```javascript
transform-origin: center center;
transform-origin: 40px 40px;
```
## 转换合写问题
【案例：盾牌打散与合并效果.html】
# 3D转换


## perspective透视

眼睛和元素的距离  值是像素  值越大  近大远小效果越弱 反之 越强

## translate平移

```javascript
/*沿着X轴的正方向移动45px*/
transform: translateX(45px);
/*沿着Y轴的正方向移动45px*/
transform: translateY(45px);
/*沿着Z轴的正方向移动45px*/
transform: translateZ(45px);

```

【02-3D转换-平移.html】

【立方体.html】

## transform-style

> transform-style 属性规定如何在 3D 空间中呈现被嵌套的元素。注意这个属性只能给父元素添加。

```javascript
flat:默认值，2d显示
preserve-3d: 3d显示
```

transform-style与perspective的区别

```javascript
/*透视：透视只是相当于设置了一个距离，辅助我们查看3D效果的工具，呈现效果为近大远小*/
/*preserve-3d:给父盒子添加，让子元素保留3D的位置，说白了，只有设置了preserve-3d，这个元素才能被称之为3d元素。 */

//一个3d元素可以没有perspective，但是不能没有transform-style
```
# 3D转换

# 动画


## animation详解

> animation是一个复合属性，一共有8个参数

```

animation-name:动画名称，由@keyframes定义的
animation-duration：动画的持续时间
animation-timing-function：动画的过渡类型
animation-delay：动画的延迟时间
animation-iteration-count：动画的循环次数  动画的执行次数  取数值 特殊值：infinite
animation-direction：设置动画在循环中是否反向运动  正逆序播放   正序：normal   逆序：alternate
animation-fill-mode：设置动画时间之外的状态 

​	设置动画结束的状态

​	none  回到初始点

​	backwards  让动画停留在开始阶段

​	forwards 让动画停留在最后一帧

​	both 结合backwards和forwards效果

animattion-play-state:设置动画的状态。

​	控制动画当前的状态

​	running  执行

​	paused 暂停
```
steps(步数)  

让动画以步数去执行  一般来说动画的步数是当前的画面数 - 1

## flex-direction

> flex-diretion主要是用来调整主轴的方向的，默认是水平方向
可选值

```javascript
row：主轴方向为水平向右
column：主轴方向为竖直向下
row-reverse:主轴方向为水平向左
column-reverse:主轴方向是竖直向上。
```

## justify-content(重点)

> justify-content主要用来设置***主轴方向的对齐方式*** ，可选的值有：

可选值：

```javascript
flex-start: 弹性盒子元素将向起始位置对齐
flex-end: 弹性盒子元素将向结束位置对齐。
center: 弹性盒子元素将向行中间位置对齐
space-around: 弹性盒子元素会平均地分布在行里
space-between:第一个贴左边，最后一个贴右边，其他盒子均分，保证每个盒子之间的空隙是相等的。
```
## align-items(重点)

> align-items用于调整***侧轴的对其方式*** ，可选的值有：

```javascript
flex-start： 元素在侧轴的起始位置对其。 
flex-end： 元素在侧轴的结束位置对其。
center： 元素在侧轴上居中对其。
stretch： 元素的高度会被拉伸到最大（不能给死高度）。
```

## flex-wrap

> flex-wrap属性控制flex容器是单行或者多行,默认不换行

```javascript
nowrap： 不换行（默认），会压缩子盒子的宽度。
wrap： 当宽度不够的时候，会换行。
```
## align-content

> align-content用来设置多行的flex容器的排列方式。

```javascript
flex-start： 各行向侧轴的起始位置堆叠。 
flex-end： 各行向弹性盒容器的结束位置堆叠。
center： 各行向弹性盒容器的中间位置堆叠。
space-between： 各行在侧轴中平均分布。 
space-around： 第一行贴上边，最后一个行贴下边,其他行在弹性盒容器中平均分布。 
stretch：拉伸，不设置高度的情况下。
```
align-items与align-content的区别

```javascript
align-items调整的是侧轴的对其方式，不换行一般用align-items
align-content:必须是多行才生效，如果单行，没有效果。换行了就用align-content。
```

## flex属性

>  flex属性用来设置子盒子如何分配主轴空间

```javascript
flex:1
```

## order属性

> order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```javascript
order:1;
```

## align-self  align-items:

> align-self也是用于设置在侧轴的位置，但是align-self给子元素设置，优先级比align-items的优先级高。

```javascript
取值与align-items的取值一样。
```
H5新增的api

## 给容器设置的样式

### flex-direction


可选值
```javascript
row：主轴方向为水平向右
column：主轴方向为竖直向下
row-reverse:主轴方向为水平向左
column-reverse:主轴方向是竖直向上。
```


### justify-content(重点)

> justify-content主要用来设置***主轴方向的对齐方式*** ，可选的值有：
>

可选值：
```javascript
flex-start: 弹性盒子元素将向起始位置对齐
flex-end: 弹性盒子元素将向结束位置对齐。
center: 弹性盒子元素将向行中间位置对齐
space-around: 弹性盒子元素会平均地分布在行里
space-between:第一个贴左边，最后一个贴右边，其他盒子均分，保证每个盒子之间的空隙是相等的。
```

### align-items(重点)

> align-items用于调整***侧轴的对其方式*** ，可选的值有：

```javascript
flex-start： 元素在侧轴的起始位置对其。 
flex-end： 元素在侧轴的结束位置对其。
center： 元素在侧轴上居中对其。
stretch： 元素的高度会被拉伸到最大（不能给死高度）。
```

### flex-wrap
> flex-wrap属性控制flex容器是单行或者多行,默认不换行

```javascript
nowrap： 不换行（默认），会压缩子盒子的宽度。
wrap： 当宽度不够的时候，会换行。
```

### align-content

> align-content用来设置多行的flex容器的排列方式。

```javascript
flex-start： 各行向侧轴的起始位置堆叠。 
flex-end： 各行向弹性盒容器的结束位置堆叠。
center： 各行向弹性盒容器的中间位置堆叠。
space-between： 各行在侧轴中平均分布。 
space-around： 第一行贴上边，最后一个行贴下边,其他行在弹性盒容器中平均分布。 
stretch：拉伸，不设置高度的情况下。
```

align-items与align-content的区别
```javascript
align-items调整的是侧轴的对其方式，不换行一般用align-items
align-content:必须是多行才生效，如果单行，没有效果。换行了就用align-content。
### flex属性

flex属性与用于子元素分配主轴的空间。

```css
flex:1;
```

### order属性

> order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
```javascript
order:1;
```

### align-self
> align-self也是用于设置在侧轴的位置，但是align-self给子元素设置，优先级比align-items的优先级高。
```javascript
取值与align-items的取值一样。
### 基本使用
# 微信T

## fullpage的使用

1. 引入jQuery文件，因为fullpage是jquery插件
2. 引入fullpage的js文件
3. 页面结构
4. 编写js代码

```

# DOM扩展（重要）

## 类名操作

> 推荐：classList是一个集合，会存储某个元素上所有的类名，使用classList来替代className操作class类

```javascript
//添加类
node.classList.add("classname");
//移除类
node.classList.remove("classname");
//切换类
node.classList.toggle("classname");
//判断类
node.classList.contains("classname");
```

【tab栏案例】

**使用cookie：操作太麻烦，最多只能存储4k ,每次请求都会带上cookie，一般只会有sessionID会存储在cookie中**   

## sessionStorage与localStorage

> HTML5规范提出了解决方案，使用sessionStorage和localStorage存储数据。设置、读取、删除操作很方便

window.sessionStorage的特点
```javascript
1. 声明周期为关闭浏览器窗口
2. 不能在多个窗口下共享数据。
3. 大小为5M
```

window.localStorage的特点
```javascript
1. 永久生效，除非手动删除
2. 可以多个窗口共享
3. 大小为5M
```
# 自定义播放器

全屏切换API：
```javascript
video.requestFullScreen()
div.webkitRequestFullScreen();
div.mozRequestFullScreen();
```
方法：load()、play()、pause()
属性：

```javascript
currentTime:当前时间
duration：总长时间
timeupdate:播放进度更改时触发
volume：控制音量
```
# 文件读取
## file对象
File对象中包含了文件的最后修改时间、文件名、文件类型等信息。

## FileReader对象

FileReader是一个HTML5新增的对象，用于读取文件（必须通过input:file上传）。
```javascript
//创建一个fileReader对象
var fr = new FileReader;
//读取文件的两个方法
readAsText() 以文本的方式读取文件 ,文本文件
readAsDataURL() 以DataURL形式读取文件，图片，视频
//文件读取完成事件：
fr.onload = function(){}
//当文件读取完成，可以通过result属性获取结果
fr.result
```
案例：

```javascript
var file = document.getElementById("file");
    var box = document.getElementById("box");

    file.addEventListener("change", function () {
        console.dir(file);
        
        //files:里面存储了所有上传的文件
        //这个data就是我们上传的那个文件
        var data = file.files[0]
      
        //1. 创建一个文件读取器
        var fr = new FileReader();

        //2. 让文件读取器读取整个文件
        fr.readAsDataURL(data);

        //3. 等待文件读取完
        //onload：文件读取完成后，就会触发
        fr.onload = function () {
            var img = document.createElement("img");
            img.src = fr.result;
            box.innerHTML = "";
            box.appendChild(img);
        }
    });
```
# ES5新增的数组方法

## forEach
**需求：遍历数组["张飞","关羽","赵云","马超"]**

```
var arr = ["张飞","关羽","赵云","马超"];
//第一个参数：element，数组的每一项元素
//第二个参数：index，数组的下标
//第三个参数：array，正在遍历的数组
arr.forEach(function(element, index, array){
  console.log(element, index, array);
});
```
## map
**需求：遍历数组，求每一项的平方存在于一个数组中**

```
var arr = [1,2,3,4,5];
//第一个参数：element，数组的每一项元素
//第二个参数：index，数组的下标
//第三个参数：array，正在遍历的数组
//返回值：一个新数组，每个元素都是回调函数的结果。
var newArray = arr.map(function(element, index, array){
  return element * element;
});
console.log(newArray);//[1,4,9,16,25]
```
## filter

> `filter`用于过滤掉“不合格”的元素
**需求：遍历数组，将数组中工资超过5000的值删除[1000, 5000, 20000, 3000, 10000, 800, 1500]**

```
var arr = [1000, 5000, 20000, 3000, 10000, 800, 1500];
//第一个参数：element，数组的每一项元素
//第二个参数：index，数组的下标
//第三个参数：array，正在遍历的数组
//返回值：一个新数组，存储了所有返回true的元素
var newArray = arr.filter(function(element, index, array){
  if(element > 5000) {
    return false;
  }else {
    return true;
  }
});
console.log(newArray);//[1000, 5000, 3000, 800, 1500]
```
## some
**需求：遍历数组，判断数组是否包含奇数，[2,4,6,8,10,9]**

```
var arr = [2,4,6,8,10,21];
//第一个参数：element，数组的每一项元素
//第二个参数：index，数组的下标
//第三个参数：array，正在遍历的数组
//返回值：布尔类型的值，只要有一个回调函数返回true，就返回true
var flag = arr.some(function(element, index, array){
  console.log(element, index, array);
  if(element %2 == 1){
    return true;
  }else {
    return false;
  }
});
console.log(flag);//true
```
## every

> `every`用于遍历数组，只有当所有的元素返回true，才返回true，否则返回false。

**需求：遍历数组，判断数组是否都是偶数，[2,4,6,8,10,9]**

```
  var arr = [2,4,6,8,10,21];
  //第一个参数：element，数组的每一项元素
  //第二个参数：index，数组的下标
  //第三个参数：array，正在遍历的数组
  //返回值：布尔类型的值，只有当所有的元素返回true，才返回true，否则返回false。
  var flag = arr.every(function(element, index, array){
    console.log(element, index, array);
    if(element %2 == 0){
      return true;
    }else {
      return false;
    }
  });
  console.log(flag);//false