#### 常见的JavaScript库

- jQuery

- Prototype

- YUI

- Dojo

- Ext JS

- 移动端的zepto

#### jQuery的概念

- jQuery是一个快速，简洁的JavaScript库，其设计的宗旨是“write less ,Do More”,即写更少的代码，做更多的事情。

- 把js中的DOM操作做了封装，我们可以快速的查询使用里面的功能。

- jQuery封装了JavaScript常用的功能代码，优化了DOM操作，事件处理，动画设计和Ajax交互。

#### jQuery的优点

- 轻量级

- 跨浏览器兼容

- 链式编程，隐式迭代

- 对事件，样式，动画支持，大大简化了DOM操作

- 直接插件扩展开发

- 免费开源

#### jQuery基本使用

1. [jQuery的下载](https://jquery.com/)

2. 引入jQuery文件

#### jQuery的入口函数

```js
$ (function () {
    页面DOM加载完成的入口
})
//类似于原生js中的
window.addEventListener("load", function() {
})
```

```js
$ (document).ready(function () {
    页面DOM加载完成的入口
})
```

#### jQuery对象和DOM对象

**<font color=#23a9f2>1.获取的方式不同</font>**

(1) 用原生js获取来的对象就是DOM对象

(2) jQuery方法获取的元素就是jQuery对象 

> 本质是利用$对DOM对象包装后产生的对象（**伪数组形式存储**）

**<font color=#23a9f2>2.相互转换</font>**

(1) DOM对象转换为jQuery对象:  **$(DOM对象)**

(2) jQuery对象转换为DOM对象

```js
$("element")[index]
```

```js
$("element").get(index)
```

#### jQuery常用的API

> 1. <a href="#xzq">**jQuery选择器**</a>
> 
> 2. <a href="#ys">**jQuery样式操作**</a>
> 
> 3. <a href="#xg">**jQuery效果**</a>
> 
> 4. <a href="#sx">**jQuery属性操作**</a>
> 
> 5. <a href="#wb">**jQuery文本属性值**</a>
> 
> 6. <a href="#yshu">**jQuery元素操作**</a>
> 
> 7. <a href="#cc">**jQuery尺寸，位置操作**</a>
> 
> 8. <a href="#sj">**jQuerys事件**</a>

#### <a id="xzq">1.jQuery选择器</a>

- 层级选择器

- 筛选选择器
  
  **<font>:eq(index)</font>** 
  
  **:checked（查找被选中的表单元素）**

#### 2.jQuery筛选方法

- parent()

- parents('"选择器") 可以返回指定祖先元素

- children(selector) 类似子代选择器

- find(selector) 类似后代选择器

- siblings(selector) 除了自身元素之外的所有亲兄弟

- nextAll([expr]) 

- prevtAll([expr])

- hasClass(class) 判断是否有某个类名

- eq(index)

#### 3.隐式迭代

- 遍历内部DOM元素（伪数组形式存储）的过程
- 对同一类元素做了同样的操作

#### 4.获取当前元素的索引号

```js
$(element).index()
```

#### 5.链式编程

1. 为了节省代码量，看起来更优雅

```js
$(function() {
    $("#top li").mouseover(function() {
        $(this).css("background", "pink").siblings().css("background", "red")
    })
})
```

#### <a id="ys">6.样式操作</a>

**<font color=#23a9f2>1.操作CSS方法</font>**

1.参数只写属性名，则是返回属性值

```js
$(element).css("color");
```

2.参数是**属性名，属性值**，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号

```js
$(element).css("color", "pink");
```

3.参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开，属性可以不加引号。

```js
$(element).css({"color":"white", "font-size":"20px"})
```

```js
$(element).css({
    width: 400,
    height: 400,
    backgroundColor: "red"
})
```

**<font color=#23a9f2>2.设置类样式方法</font>**

1.添加类

```js
$("div").addClass("类名") //这里的类名不用加点
```

2.移除类

```js
$("div").removeClass("类名")
```

3.切换类

```js
$("div").toggle("类名")
```

**<font color=#23a9f2>3.jQuery类操作和js原生类操作区别</font>**

1. 原生JS中className会覆盖元素原先里面的类名

2. jQuery里面类操作只是对指定类进行操作，不影响原先的类名

#### <a id="xg">7. jQuery效果</a>

![](D:\Typora笔记\images\2022-08-12-20-16-55-image.png)

1. 后面跟的参数都是一样的

```js
hide([[speed], [easing], [fn]])
```

2. 事件切换

```js
hover([over],out) //鼠标经过，鼠标离开
```

```js
hover(
 function() {},
 function() {}
)
```

3. 动画队列以及停止排队方法
- 动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行

- 停止排队stop()<font color=red>要写在动画或者效果的前面</font>，相当于停止结束上一次的动画
4. 渐进方式调整到指定的不透明度

```js
fadeTO([[speed], opacity, [easing],[fn]])
```

opactiy透明度**必须写**，取值0~1之间

speed(slow/normal/fast)**必须写**

easing(swing/linear)

5. 动画

```js
animate(params, [speed], [easing], [fn])

animate({height:'300px',opacity:'0.4'},"slow");
```

params是以**对象**的形式传递的，必须写。属性名可以不用带引号，如果是复合属性则需要采取驼峰命名法(Camel 标记法书写)backgroundColor。其余参数可以省略

#### <a id="sx">8.jQuery属性操作</a>

**<font color=#23a9f2>8.1 设置或获取元素固有属性值prop()</font>**

1. 获取属性语法

```js
prop("属性")
```

2. 设置属性语法

```js
prop("属性","属性值")
```

**<font color=#23a9f2>8.2设置或获取元素自定义属性值attr()</font>**

1. 获取属性语法

```js
attr("属性") //类似原生getAttribute()
```

2. 设置属性语法

```js
attr("属性","属性值") //类似原生setAttribute()
```

**<font color=#23a9f2>8.3数据缓存data()</font>**

1. 附加数据语法

```js
data("name","value") //向被选元素附加数据
```

2. 获取数据语法

```js
dat("name") //向被选元素获取数据
```

获取data-index h5自定义属性，不用写data-，而且返回的是数字型

#### <a id="wb">9.jQuery内容文本值</a>

1. 普通元素内容html() （相当于原生innerHTML）

```js
html() //获取元素的内容，连同标签一起获取
```

```js
html("内容") // 设置元素的内容
```

2. 普通元素文本内容text() （相当于原生innerText）

```js
text() //获取元素的文本内容，只获取文本内容
```

```js
text("文本内容") //设置元素的文本内容
```

3. 表单的值val() （相当于原生value）

```js
$("input").val() //获取表单值
```

```js
$("input").val("内容") //设置表单值
```

#### <a id="yshu">10.元素操作（遍历/创建/添加/删除）</a>

**<font color=#23a9f2>10.1jQuery隐式迭代是对同一元素做了同样的操作。如果想要给同一类元素做不同操作，就需要用到遍历</font>**。

**遍历对象**

```js
$("div").each(function (index, domEle) {xxxx;})
```

```js
var arr = ["red","green","blue"];
("div).each(function(index,domEle) {
 console.log(index) //返回的是索引号
 $(domEle).css("color",arr[index])
})
```

1. each()方法遍历匹配的每一个元素。主要用DOM处理

2. 里面的回调函数有2个参数：index是每个元素的索引号；demEle是每一个<font color=red>DOM元素对象，不是jquery对象</font>

3. 我们需要给这个dom元素转换为jquery对象<font color=red>$(domEle)</font>

**遍历数据**

```js
$.each(object, function (index, domEle) {xxxx;})
```

```js
$.each($("div"), function(i,ele) {})
$.each(arr,function(i,ele) {
    console.log(i);
    console.log(ele);
})
$.each({
    name: "andy",
    age: 18,
    sex: "男"
},function(i,ele) {
    console.log(i); //输出的是属性名
    console.log(ele); //输出的是属性值
})
```

1. $.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象

2. 里面的函数有2个参数：index是每个元素的索引号; element遍历内容

**<font color=#23a9f2>10.2 创建元素/添加/删除</font>**

创建元素

```js
$("<li>内容</li>")
```

添加元素

1. 内部添加（父子关系）

```js
element.prepend("内容") // 把内容放入目标元素前面
```

```js
element.append("内容") // 把内容放入目标元素后面
```

2. 外部添加（兄弟关系）

```js
element.before("内容") // 把内容放入目标元素前面
```

```js
element.after("内容") // 把内容放入目标元素后面
```

删除元素

```js
element.remove() //删除匹配的元素本身
```

```js
element.empty() //删除匹配的元素集合中所有的子节点
```

```js
element.html("") //清空匹配的元素内容
```

#### <a id="cc">11.JQuery尺寸，位置操作</a>

**<font color=#23a9f2>11.1尺寸方法</font>**

| 语法                                 | 用法                                   |
| ---------------------------------- | ------------------------------------ |
| width()/height()                   | 取得匹配元素宽度和高度值，只算width/height          |
| innerWidth()/innerHeight()         | 取得匹配元素宽度和高度值，包含padding               |
| outerWidth()/outerHeight()         | 取得匹配元素宽度和高度值，包含padding,border        |
| outerWidth(true)/outerHeight(true) | 取得匹配元素宽度和高度值，包含padding,border,margin |

 **<font color=#23a9f2>11.2位置方法</font>**

1. offset()设置或获取元素偏移量

```js
offset() //获取距离文档的位置
```

```js
offset().top //获取距离文档顶部的位置
```

```js
$("div").offset({
    top: 200,
    left: 200
}) 
```

2. position()获取带有定位的元素偏移量

```js
position() //获取距离有定位父级元素偏移量，如果没有则以文档为准
```

```js
$("div").position({
    top: 200,
    left: 200
}) 
```

3. scrollTop()/scrollLeft()设置或获取元素被卷去的头部和左侧

```js
 var boxTop = $(".container").offset().top;
 $(window).scroll(function() {
    if($(document).scrollTop() >= boxTop) {
        $(".back").fadeIn();
    } else {
        $(".back").fadeOut();
    }
})
```

#### <a id="sj"> 12.JQuery事件</a>

> 1. jQuery事件注册
> 
> 2. jQuery事件处理
> 
> 3. jQuery事件对象

单个事件注册

```js
element.事件(function() {})
```

事件处理on

```js
element.on(events, [selector], fn)
```

可以绑定多个事件，多个处理事件处理程序

```js
$("div").on({
    mouseover: function(){},
    mouseout: function(){},
    click: function(){}
})
```

如果事件处理程序相同

```js
$("div").on("mouseover mouseout", function() {
    $(this).toggleClass("current");
})
```

on**实现事件委托**和给动态元素绑定事件

给**父元素**绑定某个事件，但是触发的是**子元素**

```js
$("ul").on("click", "li", function() {
    alert('hello world!');
})
```

事件解绑

```js
$("p").off() //解绑p元素所有事件处理程序
```

```js
$("p").off("click") //解绑p元素上面的点击事件 后面的foo是侦听函数名
```

```js
$("ul").off("click","li") //解绑事件委托
```

one()只能触发一次

```js
$("p").one("click", function() {
    alert(11);
})
```

自动触发事件

```js
element.click() //第一种简写形式
```

```js
element.trigger("type") //第二种自动触发模式
```

不会触发元素的默认行为

```js
element.triggerHandler(type) //第三种自动触发模式
```

**事件对象**

事件被触发，就会有事件对象的产生

```js
element.on(events, [selector], function(event) {})
```

阻止默认行为：event.preventDefault() 或者 return false

阻止冒泡：event.stopPropagation()

#### 13. jQuery对象拷贝

把某个对象拷贝给另一个对象使用，区分深拷贝和浅拷贝

```js
$.extend([deep], target, object1, [objectN])
```

#### 14. 多库共存

jQuery解决方案:

1. 把里面的$符号统一改为jQuery.

2. jQuery变量规定新的名称：$noConflict()

#### 15. 补充的方法

截取字符串**substr()**

保留小数**toFixed()**

去除字符串二端的空格**trim()**

事件**change,scroll**

重置滚动条位置**resetui()**
