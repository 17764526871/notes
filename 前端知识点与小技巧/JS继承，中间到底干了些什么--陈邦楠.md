# JS继承，中间到底干了些什么

#### 1.实现new函数

在JS中初始化一个实例的时候，会调用new去完成实例化，那么new函数到底干了些什么事情，

- 实例可以访问构造函数中的对象
- 实例可以访问构造函数prototype中的内容

此外，我们都知道在chrome,firefox等浏览器中，实例化的对象一般都通过 __proto__指向构造函数的原型，所以会有一条如下的对应关系

```
function Person () {}
var p = new Person()
p.__proto__ = Person.prototype

```

所以我们可以实现最简单的new的山寨函数

```
function mockNew() {
     var obj = new Object()
     //获取构造函数
     var Constructor = [].shift.call(arguments)
     //绑定原形链
     obj.__proto__ = Constructor.protoype
     //调用构造函数
     Constructor.apply(obj,arguments)
     return obj
}

```

通过以上方法，我们就山寨了一个最简单的new方法，这个山寨的new方法可以更好的帮我们去理解继承的全部过程。

#### 2.原形链继承过程以及缺点解析

首先我们都知道原形链继承会存在一定的问题，红宝书上说的很清楚，这种继承方式会产生两个问题

- 无法向构造函数传入参数
- **引用类型**的数据会被实例共享

第一个原因很清楚也很容易解决，那么为什么会专门对引用类型产生问题呢，还是先上代码

```
//父类Animal
function Animal() {
    this.name = 'animal'
    this.food = ['food']
}

Animal.prototype = {
    constructor: Animal,
    //更改name
    setName: function(name) {
        this.name = name
    },
    //更改food
    giveFood: function(food) {
        this.food.push(food)
    }
}

//子类AnimalChild
function AnimalChild() {}
//绑定原形链
AnimalChild.prototype = new Animal()

let cat = new AnimalChild()
let dog = new AnimalChild()
cat.setName('cat')
cat.giveFood('fish')

console.log(cat.name)  //cat 输出cat很正常
console.log(dog.name)  //animal 这个就有点神奇了

console.log(cat.food)  // ['food','fish']
console.log(dog.food)  // ['food','fish']

```

通过以上的例子，我们发现原形式继承并不是所有的数据都会共享，**产生影响的数据只有引用类型的**，这个的原因是为什么呢，我们来使用我们的山寨new方法回顾整个过程

```
//实例话父类，绑定到子类的原形链上
AnimalChild.prototype = mockNew(Animal)

```

当我们这么调用的时候，回顾一下mocknew的执行过程，其中会执行这样一步

```
//在构造的过程中，子类会调用父类构造函数
Animal.apply(obj,arguments)

```

这步的执行，会导致本身在父类构造函数中的this.name被绑定到了一个新的函数上，因为最终的返回值被复制到子类型的protoype上，所以，子类的protoye长得是以下模样

```
//打印子类的prototype
console.log(AnimalChild.prototype)

//打印结果
AnimalChild.prototype = {
    name: 'animal',
    food: ['food'],
    __proto__: {
        constructor: Animal,
        setName: function() {},
        giveFood: function() {}
    }
}

```

可以看出借由new方法，**父类构造函数中的变量绑在在子类的原形上(prototype),而父类的原形绑在了子类原形的原形实例上(prototype.proto )**

紧接着我们在实例化子类型实例

```
var cat = mockNew(animalType)

```

这步我们会修改cat对象的__proto__属性，最终生成的cat实例打印如下

```
console.log(cat)

//打印的结果
cat = {
    __proto__: {
        name: 'animal',
        food: ['food'],
        __proto__: {
            constructor: Animal,
            setName: function() {},
            giveFood: function() {}
        }
    }
}

```

可以看出所有父类型的变量都被绑定在了实例的原形上，那为什么引用类型的数据类型会产生错误呢，这其实和引用类型的修改方式有关

当我们修改name的时候，函数会主动在对象本身去赋值，及

```
cat.name = 'cat'
console.log(cat)

//打印结果
cat = {
    //绑定在对象上，而不是原形链
    name: cat
    __proto__: {
        name: 'animal',
        food: ['food'],
        //.....
    }
}

```

而当我们对引用类型的数组进行操作的时候，**函数会优先找函数本身时候有这个变量，如果没有的话，回去原形链上找**

```
cat.name.push('fish')
console.log(cat)

//打印结果
cat = {
    __proto__: {
        name: 'animal',
        //在原形链上修改
        food: ['food'，'fish'],
        //.....
    }
}

```

#### 3.寄生组合式继承

虽然说原形式继承会带来问题，但是实现的思路是非常有用的，**对于父类的方法，变量，统统放在原形链上，继承的时候，将同名的内容统统覆盖，放在对象本身，这样就解决了函数的继承和内容的重写**

基于此，寄生组合的方法得到重视，下面分析以下执行过程，依然是使用上面的Animal和AnimalChild类

```
//寄生组合式方法调用

//声明父类
function Animal() {
    this.name = 'animal'
    this.food = ['food']
}

Animal.prototype = {
    constructor: Animal,
    //更改name
    setName: function(name) {
        this.name = name
    },
    //更改food
    giveFood: function(food) {
        this.food.push(food)
    }
}

//开始继承
function AnimalChild() {
    Animal.call(this)
}

function f() {}
f.prototype = Animal.prototype
var prototype = new f()

prototype.constructor = AnimalChild
AnimalChild.prototype = prototype


```

上述代码和原形式继承主要有两点区别

- 在子类型中使用call调用父类
- 通过new一个空函数交换prototype

首先说一下第一点，调用call，调用call之后，**相当于在子类的构造函数内部执行了一变父类的构造函数，这个时候，父函数内部通过this声明得一些属性都转嫁到了子函数的构造函数中**，这样就解决了原形式继承中变量共享的问题

其次，下面的prototype赋值方法带有一点优化的属性，因为父类构造函数中的内容通过call已经全部拿到了，只需要再将原形绑定就可以了，此外，通过new的方式，子类的挂在原形链上的方法实际上是和父类原形方法跨层级的

```
//为子类添加原形方法
AnimalChild.prototype.childMethod = function() {}
console.log(AnimalChild.prototype)

//打印结果
AnimalChild.prototype = {
    construcor: AnimalChild,
    //绑定在原形上
    childMethod: function() {},
    
    //父类的原形方法都在这里
    __proto__: {
        setName: function() {},
        giveFood: function() {}
    }
}

```

#### ES6中的super

通过寄生组合式继承我们可以得到如下结论，加入B继承了A，那么可以得到一个等式

```
B.prototype.__proto__ = A.prototype

```

满足这个等式的话其实我们就可以说B继承了A的原形链接

在ES6中的super效果下，其实实现了两条等式

```
B.__proto__ = A

//原形链相等
B.prototype.__proto__ = A.prototype

```

第二条等式我们理解，那么第一条等式是什么意思呢，在寄生组合式继承中，我们使用call的方式去调用父类构造函数，而在ES6中，我们可以理解为 **子类的构造函数是基于父类实例的加工，super返回的是一个父类的实例**，这样也就解释了等式一之间的关系。

当然，ES6中的实现方法更为优雅，借由一个ES6中提供的Api:**setPrototypeOf**,可以用如下方式实现

```
class A {}

class B {}

//原形继承
Object.setPrototypeOf(B.prototype, A.prototype);
//构造函数继承
Object.setPrototypeOf(B, A);
```