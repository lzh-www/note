# Node.js



JavaScript基础语法+Node.js内置API模块(fs,path,http等)+第三方API模块(express,mysql等)；

Node是一个基于Chrome V8引擎的JavaScript代码运行环境。



### 1.fs文件系统模块

读取文件内容

```js
const fs = require('fs')
fs.readFile('文件路径',['文件编码'],function(error,result) {
    //err读取
    //dataStr打印
})
```

判断文件读取是否成功

```js
const fs = require('fs')
fs.readFile('','',function(error,result) {
    if(error) {
        console.log('读取失败' + error.message)
    }
    console.log('读取成功' + result)
})
```

写入文件内容

```js
fs.writeFile(file, data[,options], callback)
```

```js
const fs = require('fs');
fs.writeFile('./files/2.txt'// 写入哪个文件,'写入的数据',function(err) {
    console.log(err);
})
```

判断文件写入是否成功

```js
const fs = require('fs');
fs.writeFile('./files/2.txt','abcd',function(err) {
    if (err) {
        return console.log('写入失败'+err.message);
    }
    console.log('写入成功')
})
```

fs模块-路径动态拼接的问题

解决：

- 提供一个完整的绝对路径

- __dirname + '文件'；表示当前文件夹所处的目录



### 2.path路径模块

导入path模块

```js
const path = require('path')
```

path.join() 方法用来将多个路径片段拼接成一个完整的路径字符串

```js
path.join(__dirname,'/files/1.txt') //路径是一个字符串记得加''
```

path.basename() 方法用来路径字符串中，将文件名解析出来

path.extname() 方法可以获取路径中的扩展名部分



### 3.http模块

http模块是Node.js官方提供，用来创建web服务器的模块。通过http模块提供的**http.createServer()**方法，就能方便的把一台普通电脑，变更成一台Web服务器，从而对外提供Web服务。

#### 创建Web服务器的基本步骤

1. 导入http模块
2. 创建web服务器实例
3. 为服务器实例绑定request事件，监听客户端的请求
4. 启动服务器

##### 1.导入http模块

```js
const http = require('http')
```

##### 2.创建web服务器实例

```js
const server = http.createServer()
```

##### 3.为服务器实例绑定request事件，监听客户端的请求

```js
server.on('request',function(req,res) {
    
})
```

**req请求对象**

它包含了与客户端相关的数据和属性

```js
req.url //客户端请求的地址
req.method //客户端请求类型
req.headers //获取请求报文 具体信息 + ['']
```

**res响应对象**

```js
res.end(内容) //向客户端发送指定的内容，并结束这次请求的处理过程
res.writeHead(http状态码, {'Content-Type': 'text/html; charset=utf-8'}) //设置状态码，内容类型
```

解决中文乱码问题

```js
res.setHeader('Content-Type', 'text/html; charset=utf-8') //要写在res.end()先
```

##### 4.启动服务器

```js
server.listen(8080,function() {
    console.log('http://127.0.0.1:80')
})
```

#### 根据不同的url响应不同的html内容

实现步骤

1. 获取请求的url地址
2. 设置默认的响应内容为404 Not found
3. 判断用户请求的是否为/或index.html首页
4. 判断用户请求的是否为/about.html关于首页
5. 设置响应头，防止中文乱码
6. 使用res.end()把内容响应给客户端



### 4.模块化

#### 4.1模块分类

- 内置模块
- 自定义模块
- 第三方模块（包）

#### 4.2exports对象

exports和module.exports指向的是同一对象，最终共享以module.exports为准；

require()模块，得到的永远是module.exports指向的对象；

不要在同一模块中不要使用exports和module.exports

#### 4.3CommonJS模块化规范



#### 4.4npm



> 全局安装=>命令行工具
>
> 局部安装=>库文件



##### 1.在项目中安装包的命令



```js
npm install // 包的完整名称 （npm i  包的完整名称 ）
```

```js
npm uninstall // 包的完整名称
```

```js
npm init -y // 初始化包管理配置文件
```



##### 2.nodemon工具



可以自动检测到目录中的文件更改时通过重新启动应用程序来调试基于[node](https://so.csdn.net/so/search?q=node&spm=1001.2101.3001.7020).js的应用程序

```js
npm install -g nodemon
```



##### 3.npm下载地址切换工具nrm



```js
npm install -g nrm
```

```js
nrm ls
```

```js
nrm use 地址
```



#### 4.5node_modules文件夹



>  `.bin`二进制文件，里面放了我么需要执行的命令



#### 4.6package文件夹



##### 1.项目依赖



- 在项目开发阶段和线上运营阶段，都需要依赖的第三方包，称为项目依赖
- 使用npm install 包名命令下载的文件会默认被添加到package.json文件中dependencies字段中
- `-S`



##### 2.开发依赖



- 在项目开发阶段需要依赖，线上运营阶段不需要依赖的第三方包，称为开发依赖
- 使用npm install 包名 --save-dev 命令下载的文件会默认被添加到package.json文件中devDendencies字段中

```js
npm install //项目依赖和开发依赖都会下载
```

```js
npm install --production //只会安装项目依赖 -D
```



#### 模块的加载机制



- 内置模块的加载机制

- 自定义模块的加载机制

- 第三方模块的加载机制

- 目录作为模块




#### 静态资源

```js
const http = require('http')
const url = require('url')
const path = require('path')
const fs = require('fs')
const mime = require('mime')

const app = http.createServer()
app.on('request', (req,res) => {
    //获取用户的请求路径
    let pathname = url.parse(req.url).pathname
    pathname = pathname == '/' ? '/index.html' : pathname;
    //将客户的请求路径转换为实际的服务器硬盘路径
    let lealPath = path.join(__dirname, 'public', pathname)
    //返回资源的类型
    let type = mime.getType(lealPath)
    //读取文件
    fs.readFile(lealPath, (error, result) => {
        //读取失败
        if(error != null) {
            res.writeHead(404, {'content-type':'text/html;charset=utf-8'})
            res.end('文件读取失败！');
            return
        }
        res.writeHead(200, {'content-type': type})
        res.end(result)
    })
})
app.listen(80, () => {
    console.log('http server running at http://127.0.0.1');
})
```

#### 路由

路由是指客户端请求地址与服务器端程序代码的对应关系，简单的说，就是请求什么响应什么。

```js
const http = require('http')
const url = require('url')
const app = http.createServer()
app.on('request', (req, res) => {
    //获取客户端请求的方式,转换成小写
    let method = req.method.toLowerCase()
    let pathname = url.parse(req.url).pathname
    res.writeHead(200, {'content-type':'text/html; charset=utf-8'})
    if (method == 'get') {
        if(pathname == '/' || pathname == '/index') {
            res.end('欢迎来到首页')
        } else if (pathname == '/list') {
            res.end('欢迎来到列表页')
        } else {
            res.end('获取页面失败！')
        }
    } else if (method == 'post') {

    }
})
app.listen(80, () => {
    console.log('http server running at http://127.0.0.1');
})
```

#### node.js异步编程

<img src="E:\Typora笔记\images\image-20220827205326652.png" alt="image-20220827205326652" style="zoom: 67%;" />

回调地狱：在回调函数中又嵌套回调函数一直嵌套

##### 解决异步编程回调地狱

promise

##### 异步函数

![image-20220828083741113](E:\Typora笔记\images\image-20220828083741113.png)

<img src="E:\Typora笔记\images\image-20220828083756780.png" alt="image-20220828083756780" style="zoom:80%;" />

<img src="E:\Typora笔记\images\image-20220828084920656.png" alt="image-20220828084920656" style="zoom:50%;" />





***



### 1.初识Express



#### 1.1Express简介



##### 1. 什么是Express



- 基于Node.js平台，快速，开发，极简的Web开发框架
- 作用和Node.js内置的http模块类似，是专门用来创建Web服务器的
- 本质：就是一个npm上的第三方包，提供了快速的创建Web网站的服务器的便捷方法
- express基于http内置模块封装



##### 2.Express能作做什么



最常见的二种服务器

- Web网站服务器：专门对外提供Web服务器网页资源的服务器
- API接口服务器：专门对外提供API接口的服务器



#### 1.2Express的基本使用



##### 1.安装

```js
npm i express@4.17.1
```



##### 2.创建基本的Web服务器



<img src="E:\Typora笔记\images\image-20220825000034213.png" alt="image-20220825000034213" style="zoom:80%;" />



##### 3.监听GET请求



<img src="E:\Typora笔记\images\image-20220825000150231.png" alt="image-20220825000150231" style="zoom:80%;" />



##### 4.监听POST请求



<img src="E:\Typora笔记\images\image-20220825000513492.png" alt="image-20220825000513492" style="zoom:80%;" />



##### 5.把内容响应给客户端



<img src="E:\Typora笔记\images\image-20220825000242128.png" alt="image-20220825000242128" style="zoom:80%;" />



##### 6.获取URL中携带的查询参数



<img src="E:\Typora笔记\images\image-20220825000617002.png" alt="image-20220825000617002" style="zoom:80%;" />



##### 7.获取URL中的动态参数



<img src="E:\Typora笔记\images\image-20220825000735174.png" alt="image-20220825000735174" style="zoom:80%;" />



#### 1.3托管静态资源



#### 1.4send()的好处



1. send方法内部会检测响应内容的类型、
2. send方法会自动设置http状态码
3. send方法会帮我们自动设置响应的内容类型以及编码



### 2.Express 路由

##### 构建模块化路由

```js
const express = require('express')
//创建网站服务器
const app = express()
//创建路由对象
const home = express.Router()
//为路由对象匹配请求路径
app.use('/home', home)
home.get('/index', (req,res) => {
    res.send('欢迎')
})
app.listen(80, () => {})
```

<img src="E:\Typora笔记\images\image-20220830142523204.png" alt="image-20220830142523204" style="zoom: 80%;" />

##### GET参数获取

![image-20220830143655251](E:\Typora笔记\images\image-20220830143655251.png)

##### post参数获取



















### 3.Express中间件

中间件就是一堆方法，可以接收客户端发来的请求，可以对请求做出响应，也可以将请求继续交给下一个中间件继续处理。

<img src="E:\Typora笔记\images\image-20220830091746692.png" alt="image-20220830091746692" style="zoom: 67%;" />

##### 中间件函数



```js
const mw = function(req,res,next) {
    console.log('这是最简单的中间件函数')
    next()
}
```



##### 全局生效的中间件



```js
//只接收当前设置的请求路由
app.use('/request',(req, res, next) => {
    console.log('请求走了app.use中间件/request中间件');
    next()
})
```

```js
app.use(mw)
//接收所有的请求中间件
app.use((req,res,next) => {
    console.log('这是最简单的中间件函数')
    next()
})
```



##### 局部生效的中间件(不使用app.use())



```js
app.get('', mw, function(req,res) {
	res.send('')
}) //创建路由
```



##### 中间件的5个注意事项



1. 一定要在创建路由之前注册中间件
2. 客户端发送过来的请求，可以连续调用多个中间件进行处理
3. 执行完中间件的业务代码之后，不要忘记调用next()函数
4. 为了防止代码逻辑混乱，调用next()函数后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间，共享req和res对象



##### 中间件的分类



1. 应用级别的中间件
2. 路由级别的中间件
3. 错误级别的中间件
4. Express内置
5. 第三方



##### 3.错误级别的中间件必须注册在所有路由之后

```js
app.get('/index', (req, res,next) => {
    // throw new Error('程序错误')
    fs.readFile('./dem.txt', (err, result) => {
        if(err != null) {
            next(err)
        } else{
            res.send(result)
        }
    })
})
app.use((err,req,res,next) => {
    res.status(500).send(err.message)
})
```



##### 4.Express内置中间件

- express.static 快速托管静态资源的内置中间件

- express.json 解析JSON格式的请求体数据
- express.urlencoded 解析URL-encoded格式的请求体数据

<img src="E:\Typora笔记\images\image-20220824221715901.png" alt="image-20220824221715901" style="zoom:67%;" />

在服务器端，可以通过**req.body** 来获取JSON格式的表单数据和url-encoded格式的数据

JSON格式数据默认是undefined

url-encoded格式数据默认是空对象



### 4.使用Express写接口



#### 4.1创建基本的服务器

<img src="E:\Typora笔记\images\image-20220824231423219.png" alt="image-20220824231423219" style="zoom: 50%;" />

#### 4.2创建API路由模块

<img src="E:\Typora笔记\images\image-20220824231748289.png" alt="image-20220824231748289" style="zoom: 67%;" />

#### 4.3编写GET接口

<img src="E:\Typora笔记\images\image-20220824232222828.png" alt="image-20220824232222828" style="zoom: 67%;" />

#### 4.4编写POST接口

<img src="E:\Typora笔记\images\image-20220825090343131.png" alt="image-20220825090343131" style="zoom: 67%;" />



#### 4.5CORS跨域资源共享



##### 1.接口跨域问题



主要方案：

- CORS（主流的解决方案，推荐使用）
- JSONP（有缺陷的解决方案，只支持GET请求）



##### 2.使用CORS中间件解决跨域问题



CORS是Express的一个第三方中间件。通过安装和配置cors中间件，可以很方便地解决跨域问题。

使用步骤分为如下3步：



1. 安装中间件

```js
npm install cors
```

2. 导入中间件

```js
const cors = require('cors')
```

3. 在路由之前调用配置中间件

```js
app.use(cors())
```



##### 3.CORS响应头部 - Access-Control-Allow-Origin



<img src="E:\Typora笔记\images\image-20220825095211886.png" alt="image-20220825095211886" style="zoom:80%;" />



##### 4.CORS响应头部 - Access-Control-Allow-Headers



<img src="E:\Typora笔记\images\image-20220825095142236.png" alt="image-20220825095142236" style="zoom:80%;" />



##### 5. CORS响应头部 - Access-Control-Allow-Methods



<img src="E:\Typora笔记\images\image-20220825095118270.png" alt="image-20220825095118270" style="zoom:80%;" />



##### 8.CORS请求的分类

客户端在请求CORS接口时，根据**请求方式**和**请求头**的不同，可以将CORS的请求分为两大类，分别是：

- 简单请求
- 预检请求（OPTION）



#### 4.6.JSONP接口



##### 1. JSONP的概念与特点



概念：浏览器端通过<script>标签的src属性，请求服务器上的数据，同时，服务器返回一个函数的调用。

特点：

- JSONP不属于真正的Ajax请求，因为它没有使用XMLHttpRequest这个对象
- JSONP仅支持GET请求，不支持POST.PUT.DELETE等请求



##### 2.创建JSONP接口的注意事项



如果项目中已经配置了CORS跨域资源共享，为了防止冲突，必须在配置CORS中间件之前声明JSONP的接口。否则JSONP接口会被处理成开启了CORS的接口。

<img src="E:\Typora笔记\images\image-20220825101310974.png" alt="image-20220825101310974" style="zoom:67%;" />

***



###  5.前后端身份认证



#### 5.1在Express中使用Session认证



##### 1.安装express-session中间件



```js
npm install express-session
```



##### 2.配置express-session中间件

<img src="E:\Typora笔记\images\image-20220825193940206.png" alt="image-20220825193940206" style="zoom:67%;" />

##### 3.向session中存数据

当express-session中间件配置成功后，即可通过req.session来访问和使用sessio对象，从而存储用户的关键信息：

<img src="E:\Typora笔记\images\image-20220825195028352.png" alt="image-20220825195028352" style="zoom:67%;" />

##### 4.从session中取数据

可以直接从req.session对象上获取之前存储的数据

<img src="E:\Typora笔记\images\image-20220825195203344.png" alt="image-20220825195203344" style="zoom:67%;" />

##### 5.清空session

调用req.session.destroy函数，即可清空服务器保存的session信息。

<img src="E:\Typora笔记\images\image-20220825195600722.png" alt="image-20220825195600722" style="zoom:67%;" />

#### 5.2JWT认证机制



##### 1.JWT的组成部分



Header（头部），Payload（有效荷载），Signature（签名）

三者之间使用英文的"."分隔，格式如下：



```js
Header.payload.Signature
```



##### 2.JWT的三个部分各自代表的含义



JWT的三个组成部分，从前到后分别是Header,Payload,Signature

其中：

- Payload部分才是真正的用户信息，他是用户信息经过加密之后生成的字符串。
- Header和Signture是安全性相关的部分，只是为了保证Token的安全性。



##### 3.JWT的使用方式



客户端收到服务器返回的JWT之后，通常会将它存储在localStorage或sessionStorage中。

此后，客户端每次与服务器通信，都要带上这个JWT的字符串，从而进行省份认证。推荐的做法是把JWT放在HTTP请求头的Authorization字段中，格式如下：



```js
Authorization: Bearer <token>
```



#### 5.3 在Express中使用JWT

























