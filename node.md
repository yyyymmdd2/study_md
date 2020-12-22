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

## path模块

```javascript
// basename用于获取路径的最后一个组成部分
let res = path.basename('/a/b/index.html');	// html
let res = path.basename('/a/b/index.html', ".html");	// .html

// dirname用于获取路径中的目录，除最后一个部分以外的内容
let res = path.dirname('/a/b/index.html');	// /a/b/

// extname 用于获取路径中最后一个组成部分的扩展名
let res = path.extname('/a/b/index.html');	// html

// isAbsolute 判断路径是否是绝对路径  path.isAbsolute(路径)
// linux	/开头是绝对路径    路径分隔符是左斜杠 /
// windows  盘符开头是绝对路径   路径分隔符是右斜杠 \

// path.sep 用于获取当前操作系统中路径的分隔符
// Linux  /
// Windows  \
console.log(path.sep);

// path.delimiter获取当前操作系统环境变量的分隔符
// Linux   :
// Window   ;
console.log(path.delimiter);

// path.parse(path): 将路径转换为对象
console.log(path.parse("/a/b/c/index.js"));
/*
{
  root: '/',
  dir: '/a/b/c',
  base: 'index.js',
  ext: '.js',
  name: 'index'
}
*/

// path.format(pathObject)：将对象转换为路径
console.log(path.format({
    root: '/',
    dir: '/a/b',
    base: 'index.html',
    ext: '.html',
    name: 'index'
}));
// /a/b\index.html

// path.join([...paths])  用于拼接路径   如果参数有..  上一级目录

// path.normalize(path)    规范化路径
let res = path.normalize("/a//b///index.html")
console.log(res);

// path.relative(from, to)  计算相对路径
let res = path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
console.log(res);	// ..\..\impl\bbb

// path.resolve([...paths])  用于解析路径
// 如果后面的参数是绝对路径，那么前面的参数忽略
```

## fs模块

### 查看文件状态

```javascript
// fs.stat(path[, options], callback)
// fs.statSync(path[, options])
fs.stat(__dirname, (err, stats) => {
   if (err) {
       console.log("出错了");
   } else {
       //birthtime 文件的创建时间
       // mtime: 文件的修改时间
       console.log(stats);

       if (stats.isFile()) {
           console.log("是文件");
       }else {
           console.log("是文件夹")
       }
   }
});
```

### 文件读取

```javascript
// fs.readFile(path[, options], callback)
// fs.readFileSync(path[, options])
// 没有指定第二个参数，默认会将读取的数据放在Buffer中
// 第二个参数指定为utf8，返回的数据就是字符串
fs.readFile(path.join(__dirname, "data.txt"), (err, data) => {
    if (err) {
        console.log("有错");
    } else {
        console.log(data.toString());
    }
});
```

### 写入文件

```javascript
// fs.writeFile(file, data[, options], callback)
// fs.writeFileSync(file, data[, options])
fs.writeFile(path.join(__dirname, "1.txt"), Buffer.from("fafgasg"), (err) => {
    if (err) {
        console.log("出错了");
    } else {
        console.log("成功写入文件");
    }
});
```

### 追加数据

```javascript
// fs.appendFile(path, data[, options], callback)
// fs.appendFileSync(path, data[, options])
```

### 文件流

```javascript
// fs.createReadStream(path[, options])
// fs.createWriteStream(path[, options])
```

### 目录操作

```javascript
// 1、创建目录
fs.mkdir(path[, options], callback)
fs.mkdirSync(path[, options])

// 2、读取目录
fs.readdir(path[, options], callback)
fs.readdirSync(path[, options])

//3、删除目录
fs.rmdir(path[, options], callback)
fs.rmdirSync(path[, options])
```

## http模块

### 创建服务器

```javascript
//1、创建一个服务器实列对象
let server = http.createServer();
//2. 注册请求监听
server.on("request", (req, res) => {
    /*
    req.url		请求的url  可用url模块解析
    req.method	以什么方式请求的
    */
    
    /*
    获取post请求数据
    首先req，res本质都是流
    流一般可以用on方法箭头事件
        //定义变量保存传递过来的参数
        let arr = [];
        //POST请求需要分批获取
        req.on("data", chunk => {
            arr.push(chunk);
        });
        req.on("end", () => {
            // console.log(str)
            res.end(Buffer.from(arr));
        });
    */

    //告诉浏览器返回的数据是什么类型，返回的数据需要用什么字符集解析
    res.writeHead(200, {
       "Content-Type": "text/plain; charset=utf-8"
    });
    // 结束本次请求并且返回数据
    res.end("发射点发");
});

server.listen(8080);	// 监听端口号
```

## querystring模块

```javascript
// 将参数转换为对象
querystring.parse(str[, sep[, eq[, options]]])
// 将对象转换为参数
querystring.stringify(obj[, sep[, eq[, options]]])
```

