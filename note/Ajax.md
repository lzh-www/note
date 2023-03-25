####  网页中如何请求数据？

```javascript
var xhrObj = new XMLHttpRequest();
```

#### 资源的请求方式

- <font color=#1e9ae4>get</font>请求来获取服务器资源

- <font color=#1e9ae4>post</font>请求来向服务器提交数据

#### 什么是Ajax？

- 在网页中利用XMLHttpRequest对象和服务器进行数据交互的方式，就是Ajax.

- Ajax能让我们轻松实现网页与服务器之间的数据交互.

#### jQuery中发起Ajax请求最常用的三种方法

1. ```js
   $.get(url, [data], [callback])
   ```

2. ```js
   $.post(url, [data], [callback])
   ```

3. ```js
   $.ajax({
       type: "", //请求方式，get或post
       url:"",
       data: {},
       success: function(res) {}
   })
   ```

#### 接口

概念Ajax请求数据时，被请求的URL地址，就叫做数据接口。同时，每个接口必须有请求方式。

#### 表单

1. 在网页中主要负责数据采集功能.

2. 3个基本部分组成：
- 表单标签

- 表单域

- 表单按钮



#### cookie与session



cookie: 浏览器在电脑硬盘中开辟的一块空间，主要服务器端存储数据。

- cookie中的数据是以域名的形式进行区分的
- cookie中的数据是有过期时间的，超过时间数据会被浏览器自动删除
- cookie中的数据会随着请求被自动发送到服务器端

session: 实际上就是一个对象，存储在服务器端的内存中，在session对象中也可以存储多条数据，每一条数据都有一个sessionid做为唯一标识





## Ajax加强

- XMLHttpRequest的基本使用

- 数据交换格式

- 封装自己的Ajax函数

- XMLHttpRequest Level2的新特性

- jQuery高级用法

- axios

### 1.XMLHttpRequest的基本使用

##### 1.1 什么是XMLHttpRequest

XMLHttpRequest(xhr)是浏览器提供的Javascript对象，通过它，可以请求服务器上的数据资源。之前所学的jQuery中的Ajax函数，就是基于xhr对象封装出来的。

<img title="" src="file:///E:/Typora笔记/images/2022-08-18-16-46-35-image.png" alt="" width="310" data-align="center">

##### 1.2使用xhr发起GET请求

<img title="" src="file:///E:/Typora笔记/images/2022-08-18-17-00-11-image.png" alt="" width="807">

##### 1.3了解xhr对象的readyState属性

XMLHttpRequest对象的readyState属性是用来表示当前Ajax请求所处的状态。每一Ajax请求必然处于以下状态中的一个:

![](E:\Typora笔记\images\2022-08-18-17-17-29-image.png)



##### 1.4使用xhr发起带参数的GET请求

使用xhr对象发起带参数的GET请求时，只需在xhr.open期间，为URL地址指定参数即可：

![](E:\Typora笔记\images\2022-08-18-17-21-32-image.png)

这种在URL地址后面拼接的参数，叫做查询字符串

##### 1.5查询字符串

定义：查询字符串（URL参数）是指在URL的末尾加上用于向服务器发送信息的字符串（变量）。

格式：键值对的形式，参数=值

![](E:\Typora笔记\images\2022-08-18-17-42-14-image.png)

本质：无论使用 $.ajax(),还是使用$.get(),又或者使用xhr对象发起的GET请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到URL地址的后面，发送到服务器。

![](E:\Typora笔记\images\2022-08-18-17-48-14-image.png)

##### 1.6 URL编码与解码

###### 1.什么是URL编码

###### 2. 如何对URL进行编码与解码

- encodeURI() 编码的函数

- decodeURI() 解码的函数

![](E:\Typora笔记\images\2022-08-18-18-00-20-image.png)

##### 1.7使用xhr发起POST请求

![](E:\Typora笔记\images\2022-08-18-21-53-40-image.png)

---

### 2.数据交换格式

##### 2.1什么是数据交换格式

定义：服务端与客户端之间进行数据传输与交换的格式

常用的二种数据交换格式：**XML**和**JSON**

##### 2.2XML

###### 1.什么是XML

XML的英文全称是Extensible Markup Language ,即可扩展标记语言。

###### 2.XML和HTML的区别

虽然都是标记语言，但是他们二者之间没有任何的关系。

- HTML被设计用来**描述网页上的内容**，是网页内容的载体。

- XML被设计用来**传输和存储数据**，是数据的载体。

###### 3.XML的缺点

- XML格式臃肿，和数据无关的代码多，体积大，传输效率低。

- 在Javascript中解析XML比较麻烦。

##### 2.3JSON

###### 1.什么是JSON

定义：JSON的英文全称是Javascript Object Notation, 即“Javascript对象表示法”。

**JSON就是JavaScript对象和数组的字符串表示法**，他使用文本表示一个JS对象或数据的信息，因此JSON的本质就是字符串。

作用：JSON是**一种轻量级的文本数据交换格式**，在作用上类似于XML，专门用来存储和传输数据，但是JSON比XML更小，更快，更易解析。

###### 2.JSON的二种结构

**对象结构：** 对象结构在JSON中表示为{}括号起来的内容。数据结构为{key:value, key:value,.....}的键值对结构。其中，key必须使用英文的双引号包裹的字符串，value的数据类型可以是**数字，字符串，布尔值，null，数组，对象**6中类型。

<img title="" src="file:///E:/Typora笔记/images/2022-08-18-23-31-22-image.png" alt="" width="261">

**数组结构：** 数组结构在JSON中表示为[]括号起来的内容。数据结构为["java", "javascript", "30",...]。数组中数据类型可以是**数字，字符串，布尔值，null，数组，对象**6中类型。

<img src="file:///E:/Typora笔记/images/2022-08-18-23-34-40-image.png" title="" alt="" width="616">

###### 3. JSON语法的注意事项

- 属性名必须使用双引号包裹

- 字符串类型的值**必须使用双引号包裹**

- JSON中不允许使用单引号表示字符串

- JSON中不能写注释

- JSON的**最外层**必须是对象或数组格式

- 不能使用undefined或函数作为JSON的值

###### 4.JSON和JS对象的关系

JSON是JS对象的字符串表示法，它使用文本表示一个JS对象的信息，本质是一个字符串

<img src="file:///E:/Typora笔记/images/2022-08-18-23-39-30-image.png" title="" alt="" width="340">

###### 5.JSON和JS对象的转换

JSON字符串转换为JS对象，使用JSON.parse()方法：

<img src="file:///E:/Typora笔记/images/2022-08-18-23-53-41-image.png" title="" alt="" width="564">

JS对象转换为JSON字符串，使用JSON.stringify()方法：

<img src="file:///E:/Typora笔记/images/2022-08-18-23-54-34-image.png" title="" alt="" width="569">

###### 6.序列化 JSON.stringify()和反序列化JSON.parse()

---

### 3.封装自己的Ajax函数

##### 3.1要实现的效果

<img title="" src="file:///E:/Typora笔记/images/2022-08-19-11-36-19-image.png" alt="" width="423">

##### 3.2定义options参数选项

itheima()函数是我们自定义的Ajax函数，它接收一个配置对象作为参数，配置对象中可以配置如下属性：

- method 请求的类型

- url 请求的URL地址

- data 请求携带的数据

- success 请求成功之后的回调函数

##### 3.3处理data函数

需要把data对象，转化成查询字符串的格式，从而提交给服务器，因此提前定义resolveData函数：

<img title="" src="file:///E:/Typora笔记/images/2022-08-19-11-41-33-image.png" alt="" width="413">

##### 3.4定义itheima函数

在itheima()函数中，需要创建xhr对象，并监听onreadystatechange事件：

<img title="" src="file:///E:/Typora笔记/images/2022-08-19-11-43-52-image.png" alt="" width="449">

##### 3.4判断请求的类型

不同的请求类型，对应xhr对象的不同操作，因此需要对请求类型进行if...else...的判断：

<img src="file:///E:/Typora笔记/images/2022-08-19-11-45-49-image.png" title="" alt="" width="605">

---

### 4.XMLHttpRequest Level2的新特性

##### 4.1认识XMLHttpRequest Level2

###### 1.旧版XMLHttpRequest的缺点

- 只支持文本数据的传输，无法用来读取和上传文件

- 传送和接收数据时，没有进度信息，只能提示有没有完成

###### 2.XMLHttpRequest Level2的新功能

- 可以设置HTTP请求的时限

- 可以使用FormData对象管理表单数据

- 可以上传文件

- 可以获取数据传输的进度信息

##### 4.2设置HTTP请求时限

<img src="file:///E:/Typora笔记/images/2022-08-19-12-03-18-image.png" title="" alt="" width="475">



<img src="file:///E:/Typora笔记/images/2022-08-19-12-03-27-image.png" title="" alt="" width="400">

##### 4.3FormData对象管理表单数据

<img title="" src="file:///E:/Typora笔记/images/2022-08-20-17-09-59-image.png" alt="" width="384">

<img title="" src="file:///E:/Typora笔记/images/2022-08-19-13-14-42-image.png" alt="" width="537">

##### 4.4上传文件

###### 实现步骤：

1. 定义UI结构

2. 验证是否或者了文件

3. 向FormData中追加文件

4. 使用xhr发起上传文件的请求

5. 监听onreadystatechange事件

###### 1.定义UI结构

<img src="file:///E:/Typora笔记/images/2022-08-19-13-37-17-image.png" title="" alt="" width="406">

###### 2.验证是否选择了文件

<img src="file:///E:/Typora笔记/images/2022-08-19-13-38-51-image.png" title="" alt="" width="430">

###### 3.向FormData中追加文件

<img src="file:///E:/Typora笔记/images/2022-08-19-13-39-56-image.png" title="" alt="" width="429">

###### 4.使用xhr发起上传文件请求

<img src="file:///E:/Typora笔记/images/2022-08-19-13-41-05-image.png" title="" alt="" width="733">

###### 5.监听onreadystatechange事件

![](E:\Typora笔记\images\2022-08-19-13-42-19-image.png)

##### 4.5显示文件上传进度

新版本XMLHttpRequest对象中，可以通过监听xhr.upload.onprogress事件，来获取到文件的上传进度。

![](E:\Typora笔记\images\2022-08-19-13-51-32-image.png)

![](E:\Typora笔记\images\2022-08-19-13-57-53-image.png)

![](E:\Typora笔记\images\2022-08-19-13-58-09-image.png)

---



### 5.jQuery高级用法

##### 5.1jQuery实现文件上传

---



### 6.跨域和JSONP

##### 6.1了解同源策略和跨域

##### 6.2 防抖和节流

防抖：如果事件被频繁触发，防抖能保证只有最后一次触发生效，前面N多次的触发都会被忽略。

节流：如果事件被频繁触发，节流能够减少事件触发的频率，因此，节流是有选择性地执行一部分事件。

---



## HTTP协议



- HTTP协议简介

- HTTP请求

- HTTP响应

- HTTP请求方法

- HTTP响应状态代码



### 1.HTTP协议简介

##### 1.1什么是通信

定义：信息的传递和交换。

通信三要素：主体，内容，方式。

##### 1.2什么是通信协议

定义：通信双方完成通信所必须遵守的规则和约定。

##### 1.3HTTP

HTTP协议即超文本传送协议，它规定了客户端与服务器之间进行网页内容传输时，所必须遵守的传输格式。

HTTP协议的交互模型：请求/响应的交互模型



### 2.HTTP请求消息

![](E:\Typora笔记\images\2022-08-20-17-09-06-image.png)



### 3.HTTP响应消息

![](E:\Typora笔记\images\2022-08-20-17-18-38-image.png)



### 4.HTTP请求方法

![](E:\Typora笔记\images\2022-08-20-19-06-34-image.png)



### 5.HTTP响应状态码

##### 5.1什么是HTTP响应状态码

HTTP响应状态码，也是属于HTTP协议的一部分，用来标识响应的状态。

##### 5.2HTTP响应状态码的组成及分类

HTTP状态码由**3个十进制数字组成**，第一个十进制数字定义了**状态码的类型**，后两个数字用来对状态码进行细分。

![](E:\Typora笔记\images\2022-08-20-18-54-30-image.png)

##### 5.3常见的HTTP响应状态码

###### 1.2**成功相关的响应状态码

![](E:\Typora笔记\images\2022-08-20-18-59-28-image.png)

###### 2.3**重定向相关的响应状态码

![](E:\Typora笔记\images\2022-08-20-19-01-49-image.png)

###### 3.4**客户端错误相关的响应状态码

![](E:\Typora笔记\images\2022-08-20-19-02-47-image.png)

###### 4.5**服务端错误相关的响应状态码

![](E:\Typora笔记\images\2022-08-20-19-05-29-image.png)  



