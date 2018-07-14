# call的模拟实现

## call

> 让函数执行并且将this指向第一个参数传递的值

模拟call实现思路:

1. 将函数设置为this指向的对象的属性
2. 执行该函数
3. 删除该函数

举个列子:

```js
var obj = {a: 1};
function fn() {
  	console.log(this.a);
}

fn.call(obj);

//改造如下
//将函数设置为this指向的对象的属性
obj = {
  	a: 1,
    fn: function() {
		console.log(this.a);
    }
}
//执行该函数
obj.fn();
//删除该函数
delete obj.fn;
```

这么简单的模拟会存在几个问题:

1. call函数能传递不确定数量的参数
2. this参数可以传递null/undefined, 在非严格模式下传递这两个值,js会将this指向window

针对第一个问题可以利用arguments这个类数组对象解决,如下:

```js
//将fn函数改变如下
function fn(name, age) {
  	console.log(name, age, this.a);
}
fn.call(obj, 'joah', 18);

//可用for循环对arguments对象遍历, arguments的第二项到最后一项就是我们需要的其它参数
var args = [];
for (var i = 1, len = arguments.length; i < len; i++) {
  	args.push('arguments[' + i + ']');
}
//循环完后 ['arguments[1]', 'arguments[2]']
//为什么要将数组的每一项改成字符串类型的呢? 下面进行解答
```

不定长的参数问题解决了，接着要把这个参数数组放到要执行的函数的参数里面去。在ES6中可以使用扩展运算符(...)将数组展开, 这里我们使用eval函数.

eval:

> eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码。
>
> 语法: eval(string) //string: 要计算的字符串，其中含有要计算的 JavaScript 表达式或要执行的语句。

```js
eval('obj.fn(' + args + ')');
//这里有个疑问: args = ['arguments[1]', 'arguments[2]'], 而eval('obj.fn(' + args + ')') = eval('obj.fn(arguments[1], arguments[2])'), 这是为什么呢?

//底层会调用Array.prototype.toString()方法,将args 每一项拼接成一个字符串
//例如: 'a' + ['1', '2'] === 'a1,2'        
```

这样一来就解决了参数问题,  对call函数模拟改进如下

```js
//call模拟
Function.prototype.myCall = function(context) {
  	//this指的是上下文的环境，这里就是指的调用call的函数，即在context对象上创建了一个属性,指向调用call的函数
	context.fn = this;
  	var args = [];
    for (var i = 1, len = arguments.length; i < len; i++) {
		args.push('arguments[' + i + ']');
    }
  	eval('context.fn(' + args + ')');
  	delete context.fn;
}

//测试
var obj = {a: 1};
function fn(name, age) {
  	console.log(name, age, this.a);
}
fn.myCall(obj, 'joah', 18); //joah 18 1
```

针对传入null或undefined问题,只需要添加一行代码进行处理就行

```js
context = context || window;
```

对call函数模拟再次改进如下:

```js
Function.prototype.myCall = function(context) {
  	var result, //接收函数执行的返回值
        args = [];
  	context = context || window;
  	context.fn = this;
    for (var i = 1, len = arguments.length; i < len; i++) {
      	args.push('arguments[' + i + ']');
    }
  	result = eval('context.fn(' + args + ')');
  	delete context.fn;
  	return result;
}

//测试 
var a = 1;
function fn(name, age) {
  	console.log(name, age, this.a);
}
fn.myCall(null, 'joah', 18); //joah 18 1
```

注: 真实的call函数比这模拟出来的要复杂，会添加一些健壮性代码来处理环境等问题。如：在nodejs 中如果传入undefined this会只想global 而不是window。这里模拟过程只是为了了解学习。