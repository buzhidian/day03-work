## 一、数组方法

1.  Array.from 把类数组结构、或者带有 length 的结构转化成数组，from 是构造函数的方法
2.  Array.of() 可以把一组参数转换为数组，of 更方便，只要传参数就转化为数组
3.  Array.isArray([])  也是构造函数的方法，用来检测是否是数组
    还有 new Array() instanceof Array 也能检测数组

4.  fill 填充数组
5.  copyWithin 复制数组里的某一部分，插入到数组里的某个位置
    第一个参数是插入的位置，第二个参数是开始复制的位置，第三个是结束的位置
6.  reverse（倒序）不是排序，只是颠倒数组，原数组发生改变
7.  sort 返回值是排序后的数组，原数组也会发生改变
8.  concat 合并数组，原数组不变，返回合并后的新数组
9.  slice 截取数组，原数组不变，返回新的数组，参数是 (开始的位置，结束的位置 ) ，包头不包尾
    如果参数是负数，就加上数组的长度；如果是一个参数，就直接截到最后
10.  splice 删除 替换 插入，原数组发生改变;
     删除 传两个参数 （开始的位置，删除的个数） ，返回删除的值
     替换和插入，是三个甚至更多参数；
     开始的位置 删除的长度（要插入的话第二个参数是 0） 要替换或者插入的值
11.  indexOf 从左往右找下标
     lastIndexOf() 从右往左找下标
     如果有就返回位置，没有就返回-1
12.  includes 判断是否含有元素，返回 布尔值
13.  push 末尾添加 改变原数组，返回 新数组的长度
14.  pop 末尾删除 改变原数组，返回 删除的元素
15.  unshift 开头添加 改变原数组，返回 新数组的长度
16.  shift 开头删除 改变原数组，返回 删除的元素



**数组的高阶函数 接收一个函数作为参数**

1. find 查找，只要找到满足条件的就不再继续找了，返回值是找到的第一个值

2. filter 过滤，筛选满足条件的 放在一个新的数组中，返回值就是筛选出来的数据

3. findIndex 根据条件查找数组内匹配项的下标

4. every 都满足就返回 true

5. some 有一个满足就返回 true

6. map 和 forEach 都是循环遍历
   forEach 没有返回值，对数组循环然后做一个操作，原数组会变；如果数组里是基本数据类型不会变，复杂数据类型才会变
   map 对原数组进行操作，得到一个新的数组，必须有返回值，返回新的数组
   
7. flat
   将多维数组扁平化，并返回一个新数组。方法接受一个数值，表示要扁平化的数组维度
   
8. reduce 方法接收一个函数作为累加器

   - 接收一个函数作为累加器（accumulator），数组中的每个值***（从左到右）***开始缩减，最终为一个值。
   - 第二个参数作为第一次调用的a的值

9. reduceRight 

   - 和reduce一样是累加器，不过是***从右往左计算***
   - 第二个参数作为第一次调用的a的值

   

## 二、闭包

MDN上关于闭包的解释：

​	一个函数对其周围状态的引用捆绑在一起，这样的组合就是闭包。也就是说，闭包让你可以在一个内层函数中访问到其外层函数的作用。在JavaScript中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。

一句话：**闭包是指有权访问另一个函数作用域中变量的函数**。

其实是打通函数内部与函数外部链接一个桥梁，是函数外部拿到函数内部的变量。

**特点：**

1. 函数嵌套函数
2. 有返回值
3. 返回值是一个回调函数

**优点：**可以避免全局变量污染，延长变量生命周期。

**缺点：**由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则造成网页的性能问题；在低版本IE中，可能会导致内存泄漏，解决方法是：在退出函数之前，将不使用的局部变量全部删除。



## 三、事件循环（Event Loop）

- JS是单线程的，即同一时间只能执行一个任务
- 在JS中，任务分为同步任务和异步任务
  1. **同步任务**：在主线程上执行的，形成一个执行栈，前一个任务执行完成后执行后一个任务；
  2. **异步任务**：通过回调函数实现在做任务的同时还能做其他任务。定时器、ajax、事件函数等
- 异步任务又分为宏任务和微任务
  - 宏任务：setTimeout，setInterval，ajax，dom事件监听...
  - 微任务：.then，async/await...

**事件的执行过程**

优先执行同步任务，
遇到异步任务推入任务队列中，等同步任务执行完再执行任务队列中的异步任务，
异步任务又分宏任务和微任务，先执行微任务，再执行宏任务。



## 四、this

#### 1.为什么要有this

在常见的编程语言中，几乎都有this这个关键字，但是JavaScript中的this和常见的面向对象语言中的this不太一样：

- 常见面向对象的编程语言中，比如Java、C++、Swift、Dart等等一系列语言中，this通常只会出现在类的方法中。
- 也就是你需要有一个类，类中的方法（特别是实例方法）中，this代表的是当前调用对象。
- 但是JavaScript中的this更加灵活，无论是它出现的位置还是它代表的含义。

#### 2.this的绑定规则（this的指向）

this的绑定和定义的位置（编写的位置）没有关系；
this的绑定和调用方式以及调用的位置有关系；

- 绑定一：**默认绑定**；

  - 独立的函数调用，我们可以理解成函数没有被绑定到某个对象上进行调用；（this指向window）
- 绑定二：**隐式绑定**；

  - 也就是它的调用位置中，是通过某个对象发起的函数调用；(谁调用this指向谁)
- 绑定三：**显示绑定**；

  - 必须在调用的对象内部有一个对函数的引用（比如一个属性）；
  - 如果没有这样的引用，在进行调用时，会报找不到该函数的错误；
  - 正是通过这个引用，间接的将this绑定到了这个对象上
- 绑定四：**new关键字**

​       指向实例化对象（除非构造函数返回一个引用类型，则new失效。this指针绑定变为返回的引用类型）、
​       new都干了些什么？      

- 绑定五：**箭头函数的绑定**

​       箭头函数就比较特殊了，他没有明确的指向，他里面的 this 其实是根据他的上级来定的，也就是他的 this 
​       向等于他的上级。

**优先级**

箭头函数、new、bind、apply 和 call、欧比届点（obj.）、直接调用。

#### 3.this的指向 总结

如果没有调用者，就指向全局对象 window。

1. 构造函数
   构造函数里的 this 指向实例化对象
2. 箭头函数
   箭头函数里没有 this，用的 this 是上层所在环境的 this
3. 函数是对象的属性
   this 指向这个对象
4. dom 节点调用一个事件 就指向这个 dom
5. 全局调用 就指向 widnow
6. 计时器里的 this 永远指向 window



## 五、原型和原型链

#### 1.显示原型和隐式原型

先创建一个构造函数

注意: 构造函数的首字母一定是大写的

```js
function Person () {
    //...
}

```

构造函数Person通过**prototype**属性就能访问到它的原型对象，**Person.prototype**就是**原型对象**

通过**Person**构造函数创建一个实例

```js
function Person () {
    //...
}
const person = new Person() // 通过new操作符创建一个实例
```

通过new创建的实例上有一个__proto__属性，可以直接访问原型对象Person.prototype。通常，我们将`__proto__`属性称为**隐式原型属性**。

在原型上定义的属性和方法，在实例上能够继承这些属性和方法。

如果原型对象**Person.prototype**需要访问它原来的构造函数可以通过**constructor**属性

#### **2.原型链**

当我们访问一个实例（例如person）的属性或方法时，会先在当前**实例**上查找，若查找不到，会到**原型**上查找，若原型上查找不到，就到**原型的原型**上查找，若还是查找不到就指向**null**。



**总结：**

什么是原型？

**原型是function对象的一个属性，定义了构造函数创造出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法。**

什么是prototype?

**显式原型，是函数（不包含箭头函数）本身存在的一个属性，它指向的是一个对象，即为原型对象。**

什么是 __ proto __ ?

**可以称为隐式原型，或者叫连接点。是对象的一个属性，它里面存储的是该构造函数的原型对象，即prototype.**

什么是构造函数

**构造函数其实是一种特殊的函数，主要用来初始化对象，也就是为对象成员变量赋初始值，它总与new关键字一起使用**

什么是原型链？

**当我们访问一个实例（例如person）的属性或方法时，会先在当前实例上查找，若查找不到，会到原型上查找，若原型上查找不到，就到原型的原型上查找，若还是查找不到就指向null。**



#### 3.为什么要设计JS原型呢？

***如果单纯使用new 构造函数生成对象的话，有一个很明显的缺点，即属性和方法不能共享，且浪费大量的内存。***

 如果方法不放在原型上继承的缺点：

- ***如果方法不放在原型上面的话，构造函数创建对象的时候 ，当构造函数的方法很多的时候，其结构很冗余复杂。***
- ***每次实例一个对象，都需要开辟一个空间，造成内存严重浪费***
- ***每一个对象的属性和方法都是独立的，不会互相影响，这就无法做到数据共享***

原型优点：

- ***可以让构造函数结构变得简单***
- ***可以节省内存的空间***
- ***每一个实例可以共享原型上的方法和属性，达成数据共享***

原型缺点：

***因为数据存在共享，所以可以被修改或者覆盖***





## 六、实现继承的方法

### 1.原型的继承

```js
function Super(){ this.a=1 }
Super.prototype.say = function(){ console.log(‘hhh’) }
function Sub(){}
Sub.prototype = new Super()

const test = new Sub()
console.log( test.say() )// hhh
```

优点：通过原型继承多个引用类型的属性和方法

缺点：Sub原型变成了Super的实例，如果Super的实例某个属性是引用值，该引用值就会被应用到所有Sub创建的实例中去，会有污染问题。

### 2.盗用构造函数

```js
function Super = function(){ this.a = 1 }
function Sub = function(){
       Super.call(this)
       this.b = 2
}

const test = new Sub() 
```

优点：每个实例都会有自己的a属性，哪怕是引用值也不会被污染

缺点：Super构造函数中的方法在每个实例上都要创建一遍（除非该方法声明提到全局）；Sub的实例无法访问Super原型上的方法

### 3、组合继承

原型继承+盗用构造函数继承

```js
function Super(){ this.a=[1,2] }
Super.prototype.say = function(){ console.log(‘hhh’) }
function Sub(){
    Super.call(this)
    this b=2
}
Sub.prototype = new Super()
 
const test1 = new Sub()
console.log( test1.say() )// hhh
test1.a.push(3)
console.log(test1.a)// [1,2,3]
const test2 = new Sub()
console.log(test2.a)// [1,2]
```

优点：集合了【原型继承】和【盗用构造函数继承】的优点

缺点：存在效率问题，Super始终会被调用两次

### 4、原型式继承

es5之前

```js
const obj = { a:1 }
function createObj(o){
    const Fn(){}
    Fn.prototype = o
    return new Fn()
}

const test = createObj(obj)
```

es5之后

```js
const obj = { a:1 }

const test = Object.create(obj)
```

优点：对一个对象进行浅克隆创建另一个对象，同时继承该对象的原型属性

缺点：无法判断实例的构造函数是父类还是子类

```js
const obj = { a:[1,2], b:2 }
const test1 = Object.create(obj)
const test2 = Object.create(obj)

test1.a.push(3)
test1.b=3
console.log(test1.a, test2.a)// [1,2,3]  [1,2,3]
console.log(test1.b, test2.b)// 3 2
```

### 5、寄生式继承

构造函数模式+工厂模式

```js
function createObj(o){
    let clone = objectCopy(o)
    clone.say=function(){
        console.log(‘hhh’)
    }
    return clone
}

const obj = { a:1 }
const test = createObj(obj)
```

优点：根据一个对象克隆创建另一个对象，并增强对象

缺点：同【盗用构造函数继承】方法在每个实例上都要创建一遍

注意：objectCopy不是原生接口，是自定义方法，对入参对象进行复制

### 6、寄生式组合继承

盗用构造函数继承 + 原型式继承

``` js
function Super(){ this.a=[1,2] }
Super.prototype.say = function(){ console.log(‘hhh’) }
function Sub(){
    Super.call(this)
    this b=2
}

Sub.prototype = Object.create(Super.prototype)
Sub.prototype.constructor = Sub

const test = new Sub()
```





## 七、深拷贝和浅拷贝

#### 1.深拷贝

另外创建一个一模一样的对象，新对象和原对象不共享内存，修改新对象不会更改原对象；

- **JSON.parse(JSON.stringify())**
- **jQuery.extend()** 
- **递归**

#### 2.浅拷贝

只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共存一块内存。

常见的浅复制有：展开运算符、concat()、 slice() 、Object.assign



## 八、创建对象

### 1、工厂模式

实现：

```js
function fn(a,b){
    let obj = new Object()
    obj.a=a
    obj.b=b
    return obj
}

const test = fn(1,2)

```

优点：解决了创建多个类似对象的问题

缺点：没解决对象标识问题（即新建对象是什么类型）

### 2、构造函数模式

实现：

```js
function Fn(a,b){
    this.a=a
    this.b=b
    this.c=function(){
          console.log(this.a)
    }
}

const test1 = new Fn(1,2)
const test2 = new Fn(1,2)
console.log(test1.c === test2.c)// false

```

优点：new隐式创建对象，写法简洁

缺点：构造函数定义的方法会在每个实例上都要创建一遍（除非该方法声明提到全局）

### 3、原型模式

实现：

```js
function Fn(a,b){
    Fn.prototype.a=a
    Fn.prototype.b=b
    Fn.prototype.c=function(){
          console.log(a)
    }
}

const test = new Fn(1,2)

```

优点：构造函数中定义的属性和方法都可以被对象实例共享

缺点：原型上的属性值如果是引用值，该值会在创建后的实例之间被污染，如下

```js
function Fn(){
    Fn.prototype.a=[1,2]
}

const test1 = new Fn()
const test2 = new Fn()
test1.a.push(3)
console.log(test1.b, test2.b)// [1,2,3] [1,2,3] 
const test3 = new Fn()// 原型上属性会重新赋值
console.log(test1.b, test2.b,test3.b)// [1,2] [1,2] [1,2] 

```

### 4、Object.create()

实现：

```js
const obj = { a:1 , b:2 }

const test = Object.create(obj)
console.log(test.a)// 1

```











