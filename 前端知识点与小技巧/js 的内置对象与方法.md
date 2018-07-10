## js 的内置对象有哪些？列举一下 array 和 string 的常用方法？

**内置对象**：js内置对象就是指javascript自带的一些对象，供开发者使用，这些对象提供了一些常用的功能

**js常见的内置对象：**Math对象、Date对象、Array对象、Number对象、Boolean对象、String对象......

### Array对象

+ **数组转换**

  ​	array.join( ) ;		将数组的值拼接成字符串	不传参默认按 ，进行拼接

+ **数组的增删操作**

  ​	array.push( ) ;	从数组后面添加元素，返回新数组的length

  ​	array.pop( ) ;		从数组的后面删除元素，返回删除的那个元素	

  ​	array.unshift( ) ;	从数组的前面添加元素，返回数组的长度

  ​	array.shift( ) ;		从数组的前面删除元素，返回删除的那个元素

+ **数组的翻转与排序**

  ​	array.reverse( ) ;	翻转数组

  ​	array.sort( ) ;		数组的排序	默认将数组按照字母顺序排序

  ​		sort方法可以传递一个函数作为参数，这个参数用来控制数组如何进行排序

  ​		例：arr.sort(function(a,b){

  ​				return a - b;		如果返回值 > 0 则交换位置

  ​			}) ;

+ **数组的拼接与截取**

  ​	concat：数组合并，不会影响原来的数组，会返回一个新数组。

  ​			 var newArray  = array.concat(array2) ;	

  ​	slice: 数组切分，复制数组的一部分到一个新数组，并返回这个数组

  ​			原来的数组不受影响，包含begin，不包含end

  ​			var newArray = array.slice(begin, end);	

  ​	splice: 删除数组或者增加数据元素

  ​			start:开始位置  deleteCount:删除的个数  items:替换的内容

  ​			array.slice(start, deleteCount, [items]);

+ **数组的查找**

  ​	**indexOf：**用来查找数组中某个元素第一次出现的位置，如果找不到，返回-1

  ​			   array.indexOf(search, [fromIndex]);

  ​	**lastIndexOf：**从后面开始查找数组中元素出现位置,如果找不到，返回-1

  ​			  array.lastIndexOf(search, [fromIndex]);

+ **清空数组**

  ​	array.splice(0,array.leng)	删除数组中所有的元素
  ​	array.length = 0			直接修改数组的长度
  ​	array = [ ]				将数组赋值为一个空数组，推荐

### String对象

#####    字符串方法会返回新的字符串不会改变原字符串，字符串可以遍历，String对象很多方法的名字和和Array的一样

 +  **查找指定字符串**

    ​	**indexOf：**用来查找数组中某个元素第一次出现的位置，如果找不到，返回-1

    ​	**lastIndexOf：**从后面开始查找数组中元素出现位置,如果找不到，返回-1

+ **去除空白**

  ​	trim( );	去除字符串两边的空格，内部空格不会去除

+ **大小写转换**

  ​	 toUpperCase	全部转换成大写字母
    	 toLowerCase	全部转换成小写字母

+ **字符串拼接**

  ​	concat	用法和数组一样，单字符串拼接我们一般用+

+ **字符串截取**

  ​	slice	从start开始，end结束，并且取不到end。
  ​	substring	从start开始，end结束，并且取不到end
  ​	substr 		从start开始，截取length个字符。

+ **字符串的切割**

  ​	split	将字符串分割成数组	功能和数组的join正好相反

+ **字符串的替换**

  ​	replace(searchValue, replaceValue)	

  ​		参数：searchValue:需要替换的值    replaceValue:用来替换的值


### Math对象

**Math对象**：Math对象中分装很多与数学相关的属性和方法

#### 常用方法：

- ##### 属性π

  ​	Math.PI

- ##### 最大值/最小值

  ​	Math.max( ) ;

  ​	Math.min( ) ;

- ##### 随机数

  ​	Math.random( ) ;

- ##### 取整

  ​	Math.ceil( ) ;		向上取整

  ​	Math.floor( ) ;	向下取整

  ​	Math.round( ) ;	四舍五入

### Date对象

**Date对象：**用来处理日期和时间

#### 常用方法：

- **创建一个日期对象**

  ​	var date = new Date( ) ;

  ​		不传参表示为用构造函数创建一个当前时间的对象；

  ​		传入具体时间则表示创建一个指定时间的日期对象

  ​			格式：0000-00-00  或  0000-00-00 00:00:00

- **获取日期的指定部分**

  ​	var  y = date.getFullYear( ) ;	年份

  ​	var  y = date.getMouth( ) + 1;	月份      因为国外的月份是从0开始所以要+1

  ​	var  d  = date.getDate( );		日期

  ​	var  h  = date.Hours( ) ;		小时

  ​	var  mt = date.getMinutes( ) ;	分

  ​	var  s  = date.getSeconds( ) ;	秒

  ​	var  d  = date.getDay( ) ;		星期几	取值为 0 ~ 6  星期天为 0

- **时间戳**

  ​	var date = +new Date( ) ;		时间戳  从1970年1月1日 0时 0分 0秒七至现在的总毫秒数

### Number对象

**Number对象：**数字的包装类型，数字可以直接使用这些方法

- toFixed(2)	保留2位小数
- toString( )转换成字符串

### Boolean对象

**Boolean对象：**布尔类型的包装类型。

- toString( )	转换成字符串

  注：undefined和null没有包装类型，调用toString方法会报错




ps：

​	以上所有资料参考js基础第6天（即4月28日）的课堂笔记















###  







