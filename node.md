# Node

## Node简介

- 什么是Node.js
  - Node.js 是一个基于Chorome V8 引擎的JavaScript运行环境
- 什么是V8引擎？
  - V8引擎是一款专门解释和执行JS代码的虚拟机，什么程序只要集成了V8引擎都可以执行js代码
-  NodeJS不是一门编程语言，Nodejs是一个运行环境。 这个运行环境最大的特点就是提供了操作系统底层的API
- Node环境和浏览器环境区别
  - 内置对象不同	浏览器 (window)	NodeJS  (global)
  - this默认指向不同  浏览器 (window)	NodeJS  (global)
  - API不同

## Node模块

- 一个文件就是一个模块
- 每个文件中的变量函数都是私有的，对其他文件不可见
- 每个文件的变量函数必须通过exports暴露之后其他文件才可使用
- 其他文件暴露的变量函数必须通过require()导入模块才可以使用

## NPM使用

- 全局安装（存储在全局node_modules）

  ```
  npm install -g 包名
  npm uninstall -g 包名
  upm update -g 包名
  ```

- 本地安装（存储在当前项目的node_modules）

  ```
  npm init
  npm init -y   初始化package.json文件
  
  npm install 命令根据这个配置文件，自动下载所需模块。即项目所需的运行和开发环境
  
  npm install 包名
  npm uninstall 包名
  upm update 包名
  
  npm install 包名 --save
  npm install 包名 --save-dev
  
  包描述文件 package.json，定义了当前项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）
  
  npm i   所有的包都会安装
  npm i --production  只会安装dependencies的包
  npm i --development 只会安装devDependencies的包
  ```

## Buffer对象

- 什么是Buffer?

  Buffer是NodeJS全局对象上的一个类，专门用来存储字节数据的类，本质是数组。

- 如何创建一个Buffer对象

```javascript
// 创建一个指定大小的Buffer
Buffer.alloc(size[, fill[, encoding]])
Buffer.allocUnsafe(size)
Buffer.allocUnsafeSlow(size)

//根据数组/字符串创建一个Buffer对象
Buffer.from(string[, encoding])
```

- Buffer的实列方法

```javascript
// 将二进制数据转为字符串
buf.toString()

// 往Buffer中写数据
//string <string> 要写入buf的字符串
//offset <integer> 开始写入string之前要跳过的字节数 默认0
//length <integer> 要写入的字节数。默认值：buf.length - offset
//encoding <string> string的字符编码   默认值: uft8
buf.write(string[, offset[, length]][, encoding])

// 从指定位置截取新Buffer
start <integer> 新 Buffer 开始的位置。默认值: 0。
end <integer> 新 Buffer 结束的位置（不包含）。默认值: buf.length。
buf.slice([start[, end]])
```

- Buffer静态方法

```javascript
// 检查是否支持某种编码格式
Buffer.isEncoding(encoding)
// 检查是否是Buffer类型对象
Buffer.isBuffer(obj)
// 获取Buffer实际字节长度
Buffer.byteLength(string[, encoding])
// 合并Buffer中的数据
Buffer.concat(list[,totalLength])
```

## 