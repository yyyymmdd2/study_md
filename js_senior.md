# js高级

## 变量

### 数据类型

有哪些分类?

- 基本类型

  - string:    任意字符串
  - number:   任意数字 
  - boolean:    true/false
  - undefined:    undefined
  - null:   null

- 引用类型

  - Object:    任意对象

  - Function:   一种特别的对象，可以执行

  - Arrary:   键是数字，值有序

怎么判断?

- typeof

  可以判断undefined、string、number、boolean、function

  不能判断null和object、array和object

- instanceof

  可以判断对象的具体类型

- ===
  可以判断null和undefined
  

undefined与null的区别?  

- undefined代表定义未赋值
- null代表赋值了，但值为null

什么时候给变量赋值为null呢?

- 初始赋值，表明这个变量以后会赋值个对象
- 结束前，让对象成为垃圾对象

严格区别变量类型与数据类型?

- 数据类型
  - 基本类型
  - 对象类型
- 数据类型（变量内存值的类型）
  - 基本类型：保存基本类型的数据
  - 引用类型：保存的是地址值



### 数据、变量和内存三者关系

什么是数据?

- 存储在内存中代表特定信息的'东东', 本质上是0101...
- 数据的特点: 可传递, 可运算
- 一切皆数据
- 内存中所有操作的目标: 数据

什么是内存?

- 内存条通电后产生的可储存数据的空间(临时的)

- 内存产生和死亡: 内存条(电路版)==>通电==>产生内存空间==>存储数据==>处理数据==>断电==>内存空间和数据都消失

- 一块小内存的2个数据：内部存储的数据和地址值


内存分类

- 栈: 全局变量/局部变量

- 堆: 对象

什么是变量?

- 可变化的量, 由变量名和变量值组成

- 每个变量都对应的一块小内存, 变量名用来查找对应的内存, 变量值就是内存中保存的数据

内存,数据, 变量三者之间的关系

- 内存用来存储数据的空间
- 变量是内存的标识

var a = xxx, a内存中到底保存的是什么?

- xxx是基本数据, 保存的就是这个数据
- xxx是对象, 保存的是对象的地址值
- xxx是一个变量, 保存的xxx的内存内容(可能是基本数据, 也可能是地址值)

关于引用变量赋值问题

- 2个引用变量指向同一个对象, 通过一个变量修改对象内部数据, 另一个变量看到的是修改之后的数据
- 2个引用变量指向同一个对象, 让其中一个引用变量指向另一个对象, 另一引用变量依然指向前一个对象

在js调用函数时传递变量参数时, 是值传递还是引用传递

- 理解1: 都是值(基本/地址值)传递
- 理解2: 可能是值传递, 也可能是引用传递(地址值)

JS引擎如何管理内存?

- 内存生命周期
	- 分配小内存空间, 得到它的使用权
	- 存储数据, 可以反复进行操作
	- 释放小内存空间
- 释放内存	​    
	- 局部变量: 函数执行完自动释放
	
	- 对象: 成为垃圾对象==>垃圾回收器回收
	
## 	对象

### 基础

什么是对象?

- 多个数据的封装体
- 用来保存多个数据的容器
- 一个对象代表现实中的一个事物

为什么要用对象?

- 统一管理多个数据

对象的组成

- 属性: 属性名(字符串)和属性值(任意)组成
- 方法: 一种特别的属性(属性值是函数)

如何访问对象内部数据?

- .属性名: 编码简单, 有时不能用
- ['属性名']: 编码麻烦, 能通用

什么时候必须使用['属性名']的方式?

- 属性名包含特殊字符: - 空格
- 属性名不确定，属性名是个变量

## 函数

### 基础

什么是函数？

- 实现特定功能的n条语句的封装体
- 只有函数是可以执行的, 其它类型的数据不能执行

为什么要用函数?

- 提高代码复用
- 便于阅读交流

如何定义函数?

- 函数声明
- 表达式

如何调用(执行)函数?

- test(): 直接调用
- obj.test(): 通过对象调用
- new test(): new调用
- test.call/apply(obj): 临时让test成为obj的方法进行调用，改变类别的this

### 回调函数

什么函数才是回调函数?

- 你定义的
- 你没有调
- 但最终它执行了(在某个时刻或某个条件下)

常见的回调函数?

- dom事件回调函数
- 定时器回调函数
- ajax请求回调函数
- 生命周期回调函数

### IIFE

匿名函数自调用

作用

- 隐藏实现
- 不会污染外部(全局)命名空间
- 用它来编码js模块

```javascript
;(function () {
    var a = 1
    function test () {
      console.log(++a)
    }
    window.$ = function () { // 向外暴露一个全局函数
      return {
        test: test
      }
    }
  })()
```

### 函数的this

this是什么?

- 任何函数本质上都是通过某个对象来调用的,如果没有直接指定就是window
- 所有函数内部都有一个变量this
- 它的值是调用函数的当前对象

如何确定this的值?

- test()  直接调用是window
- p.test()	对象调用是当前这个对象
- new test() 	新创建的对象，返回的值就是
- p.call(obj)    obj，强制改变this

### 原型和原型链

函数的prototype属性

- 每个函数都有一个prototype属性, 它默认指向一个Object空对象(即称为: 原型对象)
- 原型对象中有一个属性constructor, 它指向函数对象

```javascript
  function Fun () {

  }
  console.log(Fun.prototype)  // 默认指向一个Object空对象(没有我们的属性)
  // 原型对象中有一个属性constructor, 它指向函数对象
  console.log(Fun.prototype.constructor===Fun)
```

- 给原型对象添加属性(一般都是方法)，函数的所有实例对象自动拥有原型中的属性(方法)。

显式原型与隐式原型

- 每个函数function都有一个prototype，即显式原型(属性)
- 每个实例对象都有一个__proto__，可称为隐式原型(属性)
- 对象的隐式原型的值为其对应构造函数的显式原型的值
- 函数的prototype属性: 在定义函数时自动添加的, 默认值是一个空Object对象
- 对象的__proto__属性: 创建对象时自动添加的, 默认值为构造函数的prototype属性值
- 程序员能直接操作显式原型, 但不能直接操作隐式原型(ES6之前)

```javascript
  var fn = new Fn()  // 内部语句: this.__proto__ = Fn.prototype
  console.log(Fn.prototype===fn.__proto__) // true
  //给原型添加方法
  Fn.prototype.test = function () {
    console.log('test()')
  }
  //通过实例调用原型的方法
  fn.test()
```

原型链

- 访问一个对象的属性时，先在自身属性中查找，找到返回，如果没有, 再沿着\_\_proto\_\_这条链向上查找, 找到返回，如果最终没找到, 返回undefined。

- 函数的显示原型指向的对象默认是空Object实例对象(但Object不满足)

```javascript
  console.log(Fn.prototype instanceof Object) // true
  console.log(Object.prototype instanceof Object) // false
  console.log(Function.prototype instanceof Object) // true
```

- 所有函数都是Function的实例(包含Function和Object)

```javascript
console.log(Function.__proto__===Function.prototype) // true
console.log(Object instanceof Function) // true
```

- Object的原型对象是原型链尽头

```javascript
console.log(Object.prototype.__proto__) // null
```

instanceof是如何判断的?

- 表达式: A instanceof B
- 如果B函数的显式原型对象在A对象的原型链上, 返回true, 否则返回false

### 执行上下文与执行上下文栈

变量提升与函数提升