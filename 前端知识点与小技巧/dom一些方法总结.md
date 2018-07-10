**dom**

常用的非表单元素属性有哪些**

- href  超链接的url地址
- title  标签的标题属性
- id      标签的id属性
- src     引入外部文件的路径
- innerText   标签内的文本
- innerHTML   标签内的内容

**常用的表单元素**

- value 用于大部分表单元素的内容获取(option除外)

- type 可以获取input标签的类型(输入框或复选框等)

- disabled 禁用属性

- checked 复选框选中属性

- selected 下拉菜单选中属性

- ### 小结:

  disabled, checked, selected 这些布尔值属性,在DOM中通过true/false修改状态

  true 是让属性的作用生效,false 为不生效

**api**

###  offset系列

- offsetParent  用于获取定位的父级元素

- offsetLeft 距离定位父元素的左偏移量

- offsetTop 距离定位父元素的上偏移量

- offsetWidth 当前元素的宽度

  offsetHeight 当前元素的高度

  content+padding+border

- **小问题**:

  offsetParent和parentNode的区别?

  - offsetParent 返回的是离自己最近的定位父元素
  - parentNode 返回的是直接父元素

### client系列

- clientWidth 元素可视区的宽度  

- clientHeight 元素可视区的高度

  content+padding

  ### scroll系列

  - scrollLeft 元素中内容左侧滚动出去的距离

  - scrollTop  元素中内容顶部滚动出去的距离

  - scrollWidth   元素中内容的宽度

  - scrollHeight   元素中内容的高度

    content高度

    **jq**

    在jquery里面可以非常方便的操作元素或者窗口的尺寸。

    - height()与width()：设置或者返回元素的宽度及高度,返回结果是数值类型。(content宽高)
    - innerWidth()与innerHeight()：返回元素的宽度及高度（content + padding）
    - outerWidth()与outerHeigth()：返回元素的宽度及高度（content + padding + border）
    - outerWidth(true)与outerHeight(true)：返回元素的宽度及高度（content + padding + border + margin）

### offset方法

**作用: **设置或者获取元素相对于文档document的位置。

- 设置位置

  **语法: ** jQuery对象.offset({left:num, top: num})


- 获取位置

  **语法: ** jQuery对象.offset()

**注意：**使用offset操作，如果元素没有设置定位(默认position:static)，则会把position修改为relative.会修改left、top

### position方法

**作用: ** 获取相对于其最近的有定位的父元素的位置。

**语法: ** jQuery对象.position()    返回值为对象：{left:num,top:num}

**注意：**position方法只能获取，不能设置

### scrollTop 方法

**作用: ** 设置或获取元素的内容相对顶部滚动出去的距离

- 设置距离

  **语法: ** jQuery对象.scrollTop(num);

$(selector).scrollTop(100);

- 获取距离

  **语法: ** jQuery对象.scrollTop(); //返回num

###  scrollLeft 方法

**作用: ** 设置或获取元素的内容相对左侧滚动出去的距离

- 设置距离

  **语法: ** jQuery对象.scrollLeft(num);

$(selector).scrollTop(100);

- 获取距离

  **语法: ** jQuery对象.scrollLeft(); //返回num

###  小结:

- offset 相对文档的坐标
- position相对定位父元素的坐标,只读
- scorllleft, scrolltop 元素内容滚动出去的距离