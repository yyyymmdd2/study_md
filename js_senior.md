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

### 对象创建模式

Object构造函数模式

- 套路: 先创建空Object对象, 再动态添加属性/方法
- 适用场景: 起始时不确定对象内部数据
- 问题: 语句太多

```javascript
  // 先创建空Object对象
  var p = new Object()
  p = {} //此时内部数据是不确定的
  // 再动态添加属性/方法
  p.name = 'Tom'
  p.age = 12
  p.setName = function (name) {
    this.name = name
  }
```

对象字面量模式

- 套路: 使用{}创建对象, 同时指定属性/方法
- 适用场景: 起始时对象内部数据是确定的
- 问题: 如果创建多个对象, 有重复代码

```javascript
  var p = {
    name: 'Tom',
    age: 12,
    setName: function (name) {
      this.name = name
    }
  }
  
    var p2 = {  //如果创建多个对象代码很重复
    name: 'Bob',
    age: 13,
    setName: function (name) {
      this.name = name
    }
  }
```

工厂模式

- 套路: 通过工厂函数动态创建对象并返回
- 适用场景: 需要创建多个对象
- 问题: 对象没有一个具体的类型, 都是Object类型

```javascript
  function createPerson(name, age) { //返回一个对象的函数===>工厂函数
    var obj = {
      name: name,
      age: age,
      setName: function (name) {
        this.name = name
      }
    }

    return obj
  }
```

自定义构造函数模式

- 套路: 自定义构造函数, 通过new创建对象
- 适用场景: 需要创建多个类型确定的对象
- 问题: 每个对象都有相同的数据, 浪费内存

```javascript
  function Person(name, age) {
    this.name = name
    this.age = age
    this.setName = function (name) {
      this.name = name
    }
  }
```

构造函数+原型的组合模式

- 套路: 自定义构造函数, 属性在函数中初始化, 方法添加到原型上
- 适用场景: 需要创建多个类型确定的对象

```javascript
  function Person(name, age) { //在构造函数中只初始化一般函数
    this.name = name
    this.age = age
  }
  Person.prototype.setName = function (name) {
    this.name = name
  }
```

### 继承模式

原型链继承

- 套路
  - 定义父类型构造函数
  - 给父类型的原型添加方法
  - 定义子类型的构造函数
  - 创建父类型的对象赋值给子类型的原型
  - 将子类型原型的构造属性设置为子类型
  - 给子类型原型添加方法
  - 创建子类型的对象: 可以调用父类型的方法

```javascript
  //父类型
  function Supper() {
    this.supProp = 'Supper property'
  }
  Supper.prototype.showSupperProp = function () {
    console.log(this.supProp)
  }

  //子类型
  function Sub() {
    this.subProp = 'Sub property'
  }

  // 子类型的原型为父类型的一个实例对象
  Sub.prototype = new Supper()
  // 让子类型的原型的constructor指向子类型
  Sub.prototype.constructor = Sub
  Sub.prototype.showSubProp = function () {
    console.log(this.subProp)
  }
```



借用构造函数继承

- 套路
  - 定义父类型构造函数
  - 定义子类型构造函数
  - 在子类型构造函数中调用父类型构造

```javascript
  function Person(name, age) {
    this.name = name
    this.age = age
  }
  function Student(name, age, price) {
    Person.call(this, name, age)  // 相当于: this.Person(name, age)
    /*this.name = name
    this.age = age*/
    this.price = price
  }
```

原型链+借用构造函数的组合继承

- 利用原型链实现对父类型对象的方法继承
- 利用super()借用父类型构建函数初始化相同属性

```javascript
  function Person(name, age) {
    this.name = name
    this.age = age
  }
  Person.prototype.setName = function (name) {
    this.name = name
  }

  function Student(name, age, price) {
    Person.call(this, name, age)  // 为了得到属性
    this.price = price
  }
  Student.prototype = new Person() // 为了能看到父类型的方法
  Student.prototype.constructor = Student //修正constructor属性
  Student.prototype.setPrice = function (price) {
    this.price = price
  }
```



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

- 变量声明提升
  - 通过var定义(声明)的变量, 在定义语句之前就可以访问到
  - 值: undefined
- 函数声明提升
  - 通过function声明的函数, 在之前就可以直接调用
  - 函数定义(对象)

执行上下文

- 代码分类（位置）
  - 全局代码
  - 函数(局部)代码

- 全局执行上下文
  - 在执行全局代码前将window确定为全局执行上下文
  - 对全局数据进行预处理
  - var定义的全局变量==>undefined, 添加为window的属性
  - function声明的全局函数==>赋值(fun), 添加为window的方法
  - this==>赋值(window)
  - 开始执行全局代码

- 函数执行上下文

  - 在调用函数, 准备执行函数体之前, 创建对应的函数执行上下文对象(虚拟的, 存在于栈中)

  - 对局部数据进行预处理

  - 形参变量==>赋值(实参)==>添加为执行上下文的属性

  - arguments==>赋值(实参列表), 添加为执行上下文的属性

  - var定义的局部变量==>undefined, 添加为执行上下文的属性

  - function声明的函数 ==>赋值(fun), 添加为执行上下文的方法

  - this==>赋值(调用函数的对象)

  - 开始执行函数体代码

执行上下文栈

- 在全局代码执行前, JS引擎就会创建一个栈来存储管理所有的执行上下文对象
- 在全局执行上下文(window)确定后, 将其添加到栈中(压栈)
- 在函数执行上下文创建后, 将其添加到栈中(压栈)
- 在当前函数执行完后,将栈顶的对象移除(出栈)
- 当所有的代码执行完后, 栈中只剩下window

```javascript
  console.log('gb: '+ i)
  var i = 1
  foo(1)
  function foo(i) {
    if (i == 4) {
      return
    }
    console.log('fb:' + i)
    foo(i + 1) //递归调用: 在函数内部调用自己
    console.log('fe:' + i)
  }
  console.log('ge: ' + i)

1. 依次输出什么?
  gb: undefined
  fb: 1
  fb: 2
  fb: 3
  fe: 3
  fe: 2
  fe: 1
  ge: 1
2. 整个过程中产生了几个执行上下文?  5
```

### 作用域与作用域链

作用域

- 理解
  - 就是一块"地盘", 一个代码段所在的区域
  - 它是静态的(相对于上下文对象), 在编写代码时就确定了

- 分类
  - 全局作用域
  - 函数作用域
  - 没有块作用域(ES6有了)
- 作用
  - 隔离变量，不同作用域下同名变量不会有冲突

作用域与执行上下文

- 区别1
  - 全局作用域之外，每个函数都会创建自己的作用域，作用域在函数定义时就已经确定了。而不是在函数调用时
  - 全局执行上下文环境是在全局作用域确定之后, js代码马上执行之前创建
  - 函数执行上下文是在调用函数时, 函数体代码执行之前创建
- 区别2
  - 作用域是静态的, 只要函数定义好了就一直存在, 且不会再变化
  - 执行上下文是动态的, 调用函数时创建, 函数调用结束时就会自动释放
- 联系
  - 执行上下文(对象)是从属于所在的作用域
  - 全局上下文环境==>全局作用域
  - 函数上下文环境==>对应的函数使用域

作用域链

- 理解
  - 多个上下级关系的作用域形成的链, 它的方向是从下向上的(从内到外)
  - 查找变量时就是沿着作用域链来查找的
- 查找一个变量的查找规则
  - 在当前作用域下的执行上下文中查找对应的属性, 如果有直接返回, 否则进入2
  - 在上一级作用域的执行上下文中查找对应的属性, 如果有直接返回, 否则进入3
  - 再次执行2的相同操作, 直到全局作用域, 如果还找不到就抛出找不到的异常

### 闭包

理解闭包

- 如何产生闭包?
  - 当一个嵌套的内部(子)函数引用了嵌套的外部(父)函数的变量(函数)时, 就产生了闭包
- 产生闭包的条件?
  - 函数嵌套
  - 内部函数引用了外部函数的数据(变量/函数)

常见的闭包

- 将函数作为另一个函数的返回值

```javascript
  function fn1() {
    var a = 2
    function fn2() {
      a++
      console.log(a)
    }
    return fn2
  }
  var f = fn1()
  f() // 3
  f() // 4
```

- 将函数作为实参传递给另一个函数调用

```javascript
  function showDelay(msg, time) {
    setTimeout(function () {
      alert(msg)
    }, time)
  }
  showDelay('atguigu', 2000)
```

闭包的作用

- 使用函数内部的变量在函数执行完后, 仍然存活在内存中(延长了局部变量的生命周期)
- 让函数外部可以操作(读写)到函数内部的数据(变量/函数)
- 定义JS模块
  - 具有特定功能的js文件
  - 将所有的数据和功能都封装在一个函数内部(私有的)
  - 只向外暴露一个包信n个方法的对象或函数
  - 模块的使用者, 只需要通过模块暴露的对象调用方法来实现对应的功能

闭包的生命周期

- 产生: 在嵌套内部函数定义执行完时就产生了(不是在调用)
- 死亡: 在嵌套的内部函数成为垃圾对象时

```javascript
  function fn1() {
    //此时闭包就已经产生了(函数提升, 内部函数对象已经创建了)
    var a = 2
    function fn2 () {
      a++
      console.log(a)
    }
    return fn2
  }
  var f = fn1()
  f() // 3
  f() // 4
  f = null //闭包死亡(包含闭包的函数对象成为垃圾对象)
```

闭包的缺点及解决

- 缺点
  - 函数执行完后, 函数内的局部变量没有释放, 占用内存时间会变长
  - 容易造成内存泄露
- 解决
  - 能不用闭包就不用
  - 及时释放

## 线程机制与事件机制

### 进程与线程

进程：程序的一次执行, 它占有一片独有的内存空间

线程： CPU的基本调度单位, 是程序执行的一个完整流程

进程与线程

- 一个进程中一般至少有一个运行的线程: 主线程
- 一个进程中也可以同时运行多个线程, 我们会说程序是多线程运行的
- 一个进程内的数据可以供其中的多个线程直接共享
- 多个进程之间的数据是不能直接共享的

浏览器运行是单进程还是多进程?  有的是单进程，有的是多进程。

浏览器运行是单线程还是多线程?	都是多线程运行的

### 浏览器内核

什么是浏览器内核?

- 支持浏览器运行的最核心的程序

不同的浏览器可能不太一样

- Chrome, Safari: webkit
- firefox: Gecko
- IE: Trident
- 360,搜狗等国内浏览器: Trident + webkit

内核由很多模块组成

- html,css文档解析模块 : 负责页面文本的解析
- dom/css模块 : 负责dom/css在内存中的相关处理
- 布局和渲染模块 : 负责页面的布局和效果的绘制
- 布局和渲染模块 : 负责页面的布局和效果的绘制
- 定时器模块 : 负责定时器的管理
- 网络请求模块 : 负责服务器请求(常规/Ajax)
- 事件响应模块 : 负责事件的管理

### 定时器引发的思考

定时器真是定时执行的吗?

- 定时器并不能保证真正定时执行
- 一般会延迟一丁点(可以接受), 也有可能延迟很长时间(不能接受)

定时器回调函数是在分线程执行的吗?

- 在主线程执行的, js是单线程的

定时器是如何实现的?

- 事件循环模型

### JS是单线程的

如何证明js执行是单线程的?

- setTimeout()的回调函数是在主线程执行的
- 定时器回调函数只有在运行栈中的代码全部执行完后才有可能执行

为什么js要用单线程模式, 而不用多线程模式?

- JavaScript的单线程，与它的用途有关。
- 作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。
- 这决定了它只能是单线程，否则会带来很复杂的同步问题

代码的分类

- 初始化代码
- 回调代码

js引擎执行代码的基本流程

- 先执行初始化代码: 包含一些特别的代码   回调函数(异步执行)
  - 设置定时器
  - 绑定事件监听
  - 发送ajax请求
- 后面在某个时刻才会执行回调代码

### 事件循环模型

模型的2个重要组成部分

- 事件(定时器/DOM事件/Ajax)管理模块
- 回调队列

模型的运转流程

- 执行初始化代码, 将事件回调函数交给对应模块管理
- 当事件发生时, 管理模块会将回调函数及其数据添加到回调列队中
- 只有当初始化代码执行完后(可能要一定时间), 才会遍历读取回调队列中的回调函数执行

### Web Workers

