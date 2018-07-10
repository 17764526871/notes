### JQuery在项目中的常用方法

- 一般在项目中经常通过jquery来实现DOM驱动;相比js原生,实现同一个功能,代码量更少,兼容性更好.



#### JQuery中的$函数

- 传入一个匿名函数 => 入口函数,DOM树加载完毕执行,可以避免ajax中通过模版渲染时,获取不到元素的问题
- 传入一个DOM对象 => 将DOM对象包装成JQuery对象 , 例如:$(this) / this 的区别
- 传入一个选择器形式的字符串 => 获取对应的DOM元素,并且把DOM元素包装成JQuery对象

#### JQuery对象

- 是DOM对象的包装集
- 把JQuery对象转换成DOM 对象两种方式:
  - 通过下标获取 => JQuery对象[下标值]  ,返回下标对应的DOM对象
  - 通过get()方法 => JQuery对象.get(下标值) ,返回下标对应的DOM对象

#### 方法1.使用jquery获取元素

- 通过jquery选择器获取页面元素:
  - 基本选择器:ID , 类 , 标签 ,并集(使用逗号隔开) ,交集(没有空格,两个都满足)
  - 层级选择器 :子代(使用 > 号) , 后代(使用空格)
  - 筛选选择器(是方法): 
    - children() =>找到直接子元素
    - find() => 找到后代
    - siblings() => 找到兄弟元素,不包括自己
    - parent() =>找到直接父元素
    - eq(index) =>找到对应下标的元素
    - next() => 下一个兄弟元素
    - index() =>返回对应的索引

#### 方法2.使用jquery创建元素

- 创建元素:$('html形式的字符串') ,只创建没有添加到DOM树中

- 添加元素:

  - append()方法:

    - 语法:JQuery对象.append()


    - 参数:jquery对象 / html形式的字符串 / DOM对象 ;有剪切效果

  - html()方法:

    - 语法:jQuery对象.html('html形式的字符串') ; 会覆盖原来的内容

- 清空元素

  - empty()方法:
    - 语法:jQuery对象.empty()
    - 清空指定节点的所有子节点

- 删除元素

  - remove()方法
    - 语法:jQuery对象.remove(),把自己删除

- 克隆元素

  - clone()方法
    - 语法:jQuery对象.clone(boolean)
    - 传true:会克隆所有内容,注册事件也会一起克隆
    - 传false / 默认: 会克隆所有内容

#### 方法3.使用JQuery操作元素属性

- 单个属性:jQuery对象.attr('属性名','属性值')
- 多个属性:jQuery对象.attr({属性名:属性值})
- 获取属性:jQuery对象.attr('属性名'),没有返回undefined
- 移除属性:jQuery对象.removeAttr('属性名'),不传就什么都不做
- prop()方法:操作checked , selected , disable 这类boolean值类型的属性,不可以操作自定义属性
- 设置单个属性:jQuery对象.prop('属性名','属性值')
- 设置多个属性:jQuery对象.prop({属性名 : 属性值})
- 获取属性:jQuery对象.prop('属性名') ,返回true /false

#### 方法4.使用jquery操作CSS

- 行内样式:
  - 单个语法:JQuery对象.css('属性名','属性值')
  - 多个语法:JQuery对象.css({属性名:属性值})
  - 获取:JQuery对象.css('属性名')
- class样式:
  - 添加样式类:JQuery对象.addClass('类名'),传入参数不需要加点
  - 移除样式类:JQuery对象.removeClass(),不传参数,那么会移除所有的类名;传入参数,删除指定的类名
  - 判断是否有样式类:JQuery对象.hasClass('类名') ,返回是true/false
  - 切换样式类:jQuery对象.toggleClass('类名'),如果有这个类名，则移除该样式，如果没有，添加该类名

#### 方法5.使用jquery操作文本和内容

- val()方法:用于设置和获取表单元素的值
  - 设置: jQuery对象.val('值')
  - 获取: jQuery对象.val()
- html()方法
  - 设置内容: jQuery对象.html('html字符串')
  - 获取内容: jQuery对象.html()
- text()方法
  - 设置内容: jQuery对象.text('文本字符串')
  - 获取内容: jQuery对象.text()

小结:

- val()操作表单元素
- html()会识别html结构
- text()只识别文本

#### 方法6.JQuery的事件

- 简单事件绑定

  - click() 点击事件

  - mouseenter(handler)       鼠标进入事件

  - mouseleave(handler)       鼠标离开事件

  - scroll(handler)                 滚动事件

    **缺点：**一次只能绑定一个事件

    ​

- on()方法

  - 语法:$('已经存在的父盒子').on('事件类型','触发事件子元素',function(){})
  - 参数:
  - 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件
  - 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
  - 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
  - 第四个参数：handler，事件处理函数

- 解绑事件

  - off()方法:
    - 语法: jQuery对象.off(参数)
    - 不传参数:解绑匹配元素的所有事件
    - 传入对应的事件类型:解绑匹配元素的对应事件
    - 传入off("click","**") : 解绑所有代理的click事件,元素本身的事件不会被解绑

#### 方法7.使用JQuery实现ajax操作

```
$.ajax({
    type:'get/post',
  url:"",
  data:{...},//参数对象
        dataType:"json",
        beforeSend:function(){
            
        }
        success:function(info){
            
        },
        error:function(){
            
        }
})
如何终止请求 
return  false
```

