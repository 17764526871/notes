操作行内样式的方法

1.设置单个样式

jQuery对象.css("属性","属性值")

2.设置多个样式

jQuery对象.(  {"属性","属性值"....}  )

3.获取行内样式

jQuery对象.css("属性名")

操作class样式的方式

1 添加样式:

jQuery对象.addclass("类名")

2 移除样式

jQuery.对象.removeClass([类名])

注意:如果不传参数,那么会移出所有的类名,传了参数,删除指定的类名

3 判断是否有样式

jQuery对象.hasclass([类名]);

返回true/false

4 切换样式

jQuery对象.toggle("类名")

作用:如果这个jQuery对象身上有这个类名则删除它,没有就添加该类名

jQuery中的隐式迭代:就是jQuery将我们需要循环的默默的给循环了

隐式迭代: jQuery内部会帮我们遍历DOM对象,然后给每一个DOM对象实现具体的操作

创建元素

$("HTML形式的字符串)

注意:没有添加到DOM树上

添加元素

append(参数),这个方法有剪切的效果

语法:jQuery对象.append(参数)

参数形式:

1传入一个jQuery对象

2.传递一个HTML形式的字符串

3传入一个DOM对象

调用html方法

语法:jQuery对象.html("html形式的字符串)

清空元素

语法:jQuery对象.empty()

作用:清空指定节点下的所有子节点

删除元素

语法:jquery对象.remove()

作用:把自己删掉

克隆元素

语法jQuery对象.clone(true/false)

参数:true/false

注意:传true会克隆元素身上所有的内容包括注册的事件(注意:原生注册的事件是不能克隆的只能克隆jQuery对象注册的事件).

传false只是克隆元素的所有的内容