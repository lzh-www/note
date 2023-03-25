

#  一、ECMAScript相关介绍

| 版本   | 发布日期 | 添加新特性                                                   |
| ------ | -------- | :----------------------------------------------------------- |
| 第6版  | 2015     | 模块化、面向对象语法、Promise、箭头函数、let、const、数组结构赋值等等 |
| 第7版  | 2016     | 幂运算符、数组扩展、async/await关键字                        |
| 第8版  | 2017     | async/await关键字、字符串扩展                                |
| 第9版  | 2018     | 对象结构赋值、正则扩展                                       |
| 第10版 | 2019     | 扩展对象、数组方法                                           |



# 二、ECMAScript6



## 1.let

- 变量名不能重复声明
- 块级作用域
- 不存在变量提升
- 不影响作用域链

 

声明变量

```js
let a;
let a,b,c;
let e = 100;
let f = 521, g = '张三', h = [];
```



1.变量不能重复声明

```js
let star = '张三';
let star = '张三'; //报错
```



2.块级作用域`{}`

```js
{
    let girl = '张三';
}
console.log(girl); //girl is not undefined
```



使用let关键字声明的变量才具有块级作用域，var关键字是不具备这个特点的。

```js
if (true) {
    let num = 100;
    var abc = 200;
}
console.log(num); // num is not undefined
console.log(abc); // 200
```



3.不存在变量提升

```js
console.log(song); //Uncaught ReferenceError: Cannot access 'num' before initialization (初始化前无法访问“num”)
let name = '张三';
```



4.不影响作用域链

```js
{
    let school = '张三';
    function fn() {
        console.log(school);
    }
    fn()
}
// '张三'
```



5.防止循环变量变成全局变量

```js
for (var i = 0; i < 2; i++) {};
console.log(i); // 2
```

```js
for (let i = 0; i < 2; i++) {};
console.log(i); // i is not undefined
```



6.暂时性死区



## 2.const

- 必须要赋初始值
- 变量名不能重复声明
- 一般常量使用大写（潜规则）
- 常量的值不能修改
- 块级作用域
- 对于数组和对象的元素修改，不算做对常量的修改，不会报错



声明

```js
const m = '张三';
```



1.一定要初始值

```js
const A; //Uncaught SyntaxError: Missing initializer in const declaration（常量声明中缺少初始值设定项）
```



2.一般常量使用大写（潜规则）



3.常量的值不可更改

```js
const m = '张三';
m = '李四'; //Uncaught TypeError: Assignment to constant variable.
```



4.块级作用域

```js
{
    const m = '张三';
}
console.log(m); //报错
```



5.对于数组和对象的元素修改，不算做对常量的修改，不会报错。==一般声明数组和对象用const比较合适==；

```js
const TEAM = ['张三', '李四']; 
TEAM.push('王五');
```



let, const, var的区别:star:

| var          | let            | const      |
| ------------ | -------------- | ---------- |
| 函数级作用域 | 块级作用域     | 块级作用域 |
| 变量提升     | 不存在变量提升 | 不存在变量 |
| 值可更改     | 值可更改       | 值不可更改 |



## 3.var、let、const的选择

- 对于var的使用：
  1. 我们需要明白一个事实，var所表现出来的特殊性：比如作用域提升，window全局对象，没有块级作用域等都是一些历史遗留问题；
  2. 其实是Javascript在设计之初的一种语言缺陷；
  3. 当然目前市场上也在利用这种缺陷出一系列的面试题，来考验大家对JavaScript语言本身以及底层的理解；
  4. 但是在实际工作中，我们可以使用最新的规范来编写，也就是不再使用var来定义变量了；

- 对于let,const:
  1. 对于let和const来说，是目前开发中推荐使用的；
  2. 我们会优先推荐使用const，这样可以保证数据的安全性不会被随意的篡改；
  3. 只有当我们明确知道一个变量后续会需要被重新赋值时，这个时候在使用let；
  4. 这种在很多其他语言里面也都是一种约定俗成的规范，尽量我们也遵守这种规范；



## 4.作用域

在ES5中的作用域

1. 全局作用域
2. 函数/局部作用域



在ES6的代码中存在块级作用域

1. 对let/const/function/class声明的类型是有效的

2. if/switch/for块级作用域



作用域的区别：

1. 函数内部可以使用全局变量
2. 函数外部不可以使用局部变量
3. 当函数执行完毕，本作用域内的局部变量会销毁。



## 5.变量的解构赋值

> 按照一定的模式从数组和对象中提取值，对变量进行赋值，这被称为结构赋值。



ES5数组获取元素方法

```js
const F4 = ['小沈', '小白', '小兰', '小黄']
let item1 = F4[0];
let item2 = F4[1];
console.log(item1) //小沈
console.log(item2) //小白
```



ES6数组的解构

如果这个变量没有对应的值则返回undefined

```js
const F4 = ['小沈', '小白', '小兰', '小黄']
let [s, b, l, h, m] = F4;
console.log(s); //小沈
console.log(m); //undefined
```



会按照顺序解构数组里的元素，如果你只想解构某几个元素你需要用`,`隔开，预留位置。

```js
const F4 = ['小沈', '小白', '小兰', '小黄']
let [ , , , h] = F4;
console.log(h); //小黄
```



解构出一个元素，后面的元素放到一个新数组中

```js
const F4 = ['小沈', '小白', '小兰', '小黄']
let [item, ...newF4] = F4;
console.log(item, newF4); // 小沈 ['小白', '小兰', '小黄']
```



解构的默认值

```js
const F4 = ['小沈', '小白', '小兰']
let [itema, itemb, itemc, itemd = '小黄'] = F4;
```



对象的解构

```js
const zhao = {
    name: '李四',
    age: 13,
    info: function() {
        console.log('相信自己')
    }
}
let { name: uname, age, info } = zhao; //解构重命名，也可以给默认值
console.log(uname) //李四
info(); // 相信自己
```



## 6. 模板字符串

> ES6引入新的声明字符串的方式``， 以前拼接字符串和标识符使用""或者''



声明

```js
let str = `我也是一个字符串哦`
console.log(str, typeof str)
```



内容中可以直接出现换行符

```js
let str = `<ul>
				<li>小兰</li>
				<li>张三</li>
				<li>李四</li>
			</ul>`
```



变量拼接`${}`

```js
let lovest = '小兰'
let out = `${lovest}是我心中最帅的男人` // let out = lovest +  '是我心中最帅的男人'; ES5
```



在模板字符串中可以调用函数

```js
const fn = () => {
    return '我是fn函数'
}
let html = `我是模板字符串${fn()}`;
console.log(html); // 我是模板字符串我是fn函数
```



标签模板字符串



## 7.增强对象字面量

> ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更简洁。
>
> 属性的简写：property shorthand 
>
> 方法的简写：method shorthand 
>
> 计算属性名：computed property names



```js
let name = '张三'
let change = function() {
    console.log('我们是最好的')
}

const school = {
    name, //name: name
    change, //change: change
    
    // improve: function() {}
    improve() { 
        console.log('你好啊')
    }
}
```



```js
//区分
improve: () => {}
```



## 8.箭头函数以及声明特点

> 箭头函数没有名字，所有我们需要赋值给一个变量，通过变量名字调用它。



```js
let fn = function() {};
let fn = () => {}; // 调用fn()
```



1.箭头函数是没有显式原型的，所有不能作为构造函数，使用new来创建对象；

```js
let Person = (name, age) => {
    this.name = name;
    this.age = age;
}
let me = new Person('张三', 20)
console.log(me); //报错
```



2.不能使用arguments变量

```js
let fn = () => {
    console.log(arguments);
}
fn(1, 2, 3)
```



3.箭头函数的简写

- 省略小括号，当==形参有且只有一个==的时候

- 省略花括号，当==代码体中只有一条语句==的时候，此时 ==return 必须省略==，而且语句的执行结果就是函数的返回值。

```
let add = (n) => {
	return n + n;
}
console.log(add(9))
```

```js
let add = n => n + n;
console.log(add(9))
```



4.箭头函数中的`this`关键字

> 箭头函数不绑定this关键字，箭头函数中的this指向的是函数定义位置的上下文this。

```js
function fn() {
    console.log(this);
    return () => {
        console.log(this);
    }
}
const obj = { name: '张三' }
fn.call(obj); // {name: '张三'}
```

```js
var age = 100;
var obj = {
    age: 20,
    say: () => {
        console.log(this.age)
    }
}
obj.say(); // 100
```



> 箭头函数适合与this无关的回调。定时器，数组的方法回调。
>
> 箭头函数不适合与this有关的回调。事件回调，对象的方法。





## 9.函数的默认参数

> ES6允许给函数参数赋值初始值



Es5以及之前给参数默认值

缺点： 

- 写起来很麻烦，并且代码的阅读性是比较差的
- 存在bug

```js
function foo(m, n) {
    m = m || 'aaa'
    n = n || 'bbb'
    consloe.log(m, n)
}
foo(); //aaa bbb
foo(0, "")// aaa bbb 0/""会默认被认为false
```



Es6给参数默认值

1.形参初始值，具有默认值的参数，一般位置要靠后（潜规则）

```js
function add(a, b, c=10) {
    return a + b + c;
}
let result = add(1,2)
console.log(result)
```



2.与解构赋值结合

```js
function connect({host='127.0.0.1', username, password, port}) {
    console.log(host)
    console.log(username)
    console.log(password)
    console.log(port)
}
connect({
    host: 'atguigu.com',
    username: 'root',
    password: 'root',
    port: 3006
})
```



## 10.函数剩余参数

> 如果最后一个参数是...为前缀的，那么他会将剩余的参数放在该参数中，并且作为一个数组；



ES5获取实参的方式

```js
function date() {
    console.log(arguments)
}
date('小李', '张三', '李四'); // ['小李', '张三', '李四', callee: ƒ, Symbol(Symbol.iterator): ƒ]
```



rest参数

```js
function date(n, ...args) {
    console.log(args)
}
date('小李', '张三', '李四'); // ['张三', '李四']
```



rest参数必须要放在参数最后

```js
function fn(a, b, ...args) {
    console.log(args)
}
fn('小李', '张三', '李四', '王五'); 
```



剩余参数与解构赋值配合使用

```js
let num = [1, 2, 3];
let [n1, ...n2] = num;
console.log(n1); // 1
console.log(n2); // [2, 3]
```



**剩余参数和arguments的区别**

- 剩余参数只包含那些没有对应形参的实参，而arguments对象包含了传给函数的所有实参；
- arguments不能在箭头函数中使用；
- arguments对象不是一个真正的数组 (伪数组)，而rest参数是一个真正的数组，可以进行数组的所有操作；
- arguments是早期的ECMAscript中为了方便去获取所有的参数提供的一个数据结构，**而rest参数是ES6中提供并且希望以此来代替arguments的**；



## 11.this指向

### 普通函数

```javascript
function fn() {
    console.log(this);
}

fn(); // window.fn() this指向调用方
```



### 箭头函数

```javascript
const person = {
    name: '张三',
    fn() {
        console.log(this); // person
        
        const subFn = () => {
        	console.log(this); // 指向上层作用域fn()中的this
    	}
    }
}
person.fn();
```



### call、apply、bind

```javascript
const fn = () => {
    console.log(this); // window 箭头函数永远不会修改this指向
}

function fn2() {
    console.log(this); // person
}

fn.apply(person);
fn2.call(person);
fn.bind(person)();
```



## 12.扩展运算符

> 扩展运算符能将数组或者对象转换为用逗号分隔的参数序列



函数调用时

```js
const names = ['张三', '李四', '王五']；
const name = 'why';

function foo(x, y, z) {
    console.log(x,y,z)
}
foo(...names); // 张三 李四 王五
foo(...name); // w h y
```



```js
const info = ['张思', '李四', '雄安']

function fn() {
    console.log(arguments)
}
fn(...info); //fn('张思', '李四', '雄安')
```



Array的扩展方法

1.数组的合并

```js
const n1 = ['李白', '李元芳', '李逵']
const n2 = ['小白', '张三', '李四']
const hb = n1.concat(n2); //ES5
const hb = [...n1, ...n2]; //ES6
n1.push(...n2); //这个方法也可以
console.log(hb); //['李白', '李元芳', '李逵', '小白', '张三', '李四']
```



2.数组的克隆

```js
const n1 = ['李白', '李元芳', '李逵']
const kl = [...n1];
console.log(kl); //['李白', '李元芳', '李逵']
```



3.将伪数组转为真正的数组

```js
const divs = document.querySelectorAll('div');
console.log(divs); // NodeList(5) [div, div, div, div, div]
const divArr = [...divs];
console.log(divArr); // (5) [div, div, div, div, div]
```

  

4.返回数组中的最大最小值

```js
const arr = [20, 30, 3, 4]
console.log(Math.min(...arr)); // 3
console.log(Math.max(...arr)); //30
```



## 13.Symbol

> ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型，是一种类似于字符串的数据类型。

  

Symbol的特点

- Symbol 的值是唯一的，用来解决命名冲突的问题。
- Symbol 值不能与其他数据进行运算。
- Symbol 定义的对象属性不能使用 for...in 循环遍历，但是可以使用 Reflect.ownKeys 来获取对象的所有键名。



创建Symbol

```js
let s = Symbol()
let s = Symbol('张三')
let s1 = Symbol.for('张三'); //函数对象
```



## 14.迭代器



### 隐式的迭代器：for-of

数组-数组可迭代

```javascript
const names = ['张三', '李四', '王五'];
for (const iterator of names) {
	console.log(iterator); // 张三、李四、王五
}
```

```js
for(let value of xxx) {
    console.log(value)
}
```



对象-普通对象默认不可迭代

```javascript
const person = {
    name: '张三',
    age: 30
}

// Uncaught TypeError: person is not iterable
for (const iterator of person) {
    console.log(iterator);
}
```



### 显示的迭代器：Symbol.iterator

```javascript
const names = ['张三', '李四', '王五'];
const it = names[Symbol.iterator]()
console.log(it); // Array Iterator {}
console.log(it.next()); // {value: '张三', done: false}
console.log(it.next()); // {value: '李四', done: false}
console.log(it.next()); // {value: '王五', done: false}
console.log(it.next()); // {value: undefined, done: true}
```



## 15.生成器

```javascript
function* simple() {
    
}
```



## 16.Promise

> Promise是Es6引入的异步编程的解决方案。语法上Promise是一个==构造函数==，用来封装异步操作并可以获取其成功和失败的结果。

 

- Prommise构造函数：`Promise（excutor）{}`

- Promise.prototype.then方法
- Promise.prototype.catch方法



可以改变Promise对象的状态

then方法的返回值是一个Promise对象，对象状态由回调函数的执行结果决定。

```js
const p = new Promise((resolve, reject) => {
    //接收一个异步函数
})
p.then(function(value) {}, function(reason) {}); //成功失败的回调
```



## 17.Set数据结构

>  `Set` (集合) 。他类似于数组，但成员的值都是唯一的，集合实现了 `iterator1` 接口，所以可以使用扩展运算符和for..of...进行遍历，本质上也是一个对象。



构造函数

```js
let s = new Set();
let s2 = new Set(['大事儿', '小事儿', '好事儿', '坏事儿', '小事儿']);
```

```js
//元素个数
s2.size
//添加新的元素
s2.add('喜事儿')
//删除元素
s2.delete('坏事儿')
//检测
s2.has('糟心事') //返回一个布尔值
//清空
s2.clear()
//遍历
for(let v of s2) {
    console.log(v)
}
// forEach()也可以
```



数组去重

```js
let s2 = new Set(['大事儿', '小事儿', '好事儿', '坏事儿', '小事儿']);
const ary = [...s2];
console.log(ary); // ['大事儿', '小事儿', '好事儿', '坏事儿']
```



## 18.Map数据结构

> 以键值对的形式存储数据，其中键值对可以是任何值



创建

```javascript
const m = new Map();
```

增

```javascript
m.set('name', '张三')
m.set('age', '30')
```

删

```javascript
m.delete('name')
```

改

```javascript
m.set('name', '李四')
```

查

```javascript
m.get('name')
```

获取长度

```javascript
m.size
```

迭代

```javascript
for (const [key, value] of m) {
    console.log(key, value);
}
```





## 19.ES6模块化



> ES6模块化规范是浏览器端与服务器端通用的模块化开发规范。它的出现极大的降低了前端开发者的模块化学习成本，开发者不需要再额外学习AMD:recycle:， CMD:recycle:或者CommonJS等模块化规范。



ES6模块化规范中定义：



- 每个JS文件都是一个独立的模块
- 导入其他模块成员使用`import`关键字
- 向外共享模块成员使用`export`关键字



**在node.js中体验ES6模块化**



> node.js中默认仅支持CommonJS模块化规范，若想基于node.js体验与学习ES6的模块化语法



需要以下步骤配置：

- node.js > v14.15.1 或更高版本
- package.json的根节点中添加`"type": "module"`节点 



**ES6模块化的基本语法**



:one: 默认导出与默认导入



> :warning: 每个模块中，只允许使用唯一的一次export default , 否则会报错



```js
export default {}
```

```js
import xxx from ''
```



:two: 按需导出与按需导入



```js
export let s1 = 'aaa'
export let s2 = 'ccc'
export function say() {}
```

```xml
import { s1, s2 as str2, say } from ''
```



:three: 直接导入并执行模块中的代码



```xml
import ''
```



## 20.类和对象

- `constructor`构造器
- `extends类`继承
- `super`关键字

- new.target



创建类 class 创建一个明星类

```js
class Star {
    constructor(uname) {
        this.uname = uname
    }
}
```



利用类创建对象

```js
var ldh = new Star('刘德华');
console.log(lds.uname);
```



类中添加方法

```js
// 我们类里面所有的函数不需要写function
// 多个函数方法之间不需要添加逗号分隔
class Star {
    constructor(uname) {
        this.uname = uname
    }
    sing() {
        
    }
}
```



## 21.对象的新增方法

1. [Object.is()](https://es6.ruanyifeng.com/#docs/object-methods#Object.is())
2. [Object.assign()](https://es6.ruanyifeng.com/#docs/object-methods#Object.assign())
3. [Object.getOwnPropertyDescriptors()](https://es6.ruanyifeng.com/#docs/object-methods#Object.getOwnPropertyDescriptors())
4. [__proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf()](https://es6.ruanyifeng.com/#docs/object-methods#__proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf())
5. [Object.keys()，Object.values()，Object.entries()](https://es6.ruanyifeng.com/#docs/object-methods#Object.keys()，Object.values()，Object.entries())
6. [Object.fromEntries()](https://es6.ruanyifeng.com/#docs/object-methods#Object.fromEntries())
7. [Object.hasOwn()](https://es6.ruanyifeng.com/#docs/object-methods#Object.hasOwn())



## 22.正则表达式



1.什么是正则表达式

> 正则表达式（Regular Expression）是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也是对象。：匹配，替换，提取。



2.创建正则表达式

:warning:正则表达式里面不需要加引号，不管是数字型还是字符串型



:one:通过调用RegExp对象的构造函数创建

```js
var 变量名 = new RegExp(/表达式/);
```



:two:通过字面量创建

```js
var 变量名 = /表达式/;
```



3.测试正则表达式 test

> `test()`正则对象方法，用于检测字符串是否符合该规则，该对象会返回true或false，其参数是测试字符串。



4.正则表达式中的特殊字符



边界符

> 正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符。

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| ^      | 表示匹配行首的文本（以谁开始） |
| $      | 表示匹配行尾的文本（以谁结束） |

如果^和$在一起，表示必须是精确匹配



字符类

> 字符类： []表示有一系列字符可供选择，只要匹配其中一个就可以了



[-]方括号内部范围符-

```js
/^[a-z]$/; // 26个小写英文字母任何一个字母返回true
```



 字符组合

```js
/^[a-zA-Z]$/; // 26个大小写英文字母任何一个字母返回true
```

```js
/^[a-zA-Z0-9_-]$/;
```



如果中括号里面有^表示取反的意思

```js
/^[^a-zA-Z0-9_-]$/;
```



量词符

> 设定某个模式出现的次数

| 量词  | 说明                                 |
| ----- | ------------------------------------ |
| *     | 重复零次或更多次  >=0                |
| +     | 重复一次或更多次  >=1                |
| ？    | 重复零次或一次  1 \|\| 0             |
| {n}   | 重复n次                              |
| {n,}  | 重复n次或更多次  大于等于n           |
| {n,m} | 重复n到m次  大于等于n 并且 小于等于m |



预定义类

```js
\d,\w,\s; \D,\W,\S
```



正则表达式参数

```js
/表达式/[switch];
```

- g：全局匹配
- i：忽略大小写
- gi：全局匹配 + 忽略大小写



# 三、ECMAScript7

## 1.Array.prototype.includes

> includes方法用来检测数组中是否包含某个元素，返回布尔类型值。区分indexOf，返回下标。



```js
const s1 = [ '张三', '李四', '王五'];
console.log(s1.includes('张三')); //true
```



## 2.指数操作符

>  幂运算

```log
console.log(2 ** 10);
console.log(Math.pow(2, 10));
```



# 四、ECMAScript8

## 1.async函数







## 2.await表达式









## 3.对象方法扩展

Object.keys() 获取对象所有的键

Object.values() 获取对象所有的值

Object.entries() 返回一个数组，每个键值对都是一个元素

Object.getOwnPropertyDescriptors() 对象属性的描述







# 五、ECMAScript9

> Rest参数与spread扩展运算符咋ES6中已经引入，不过ES6中只针对于数组。在ES9中为对象提供了像数组一样的rest参数和扩展运算符。



rest参数

```js
function connect({host, port, ...user}) {
	console.log(host);
    console.log(port);
    console.log(user);
}
connect({
    host: '127.0.0.1',
    port: 8080,
    username: 'root',
    password: 'root',
    type: 'master'
})

```



扩展运算符

对象的合并

```js
```



正则扩展-命名捕获分组

正则扩展-反向断言

正则扩展-dotAll模式





# 六、ECMAScript10



## 1.对象扩展方法Object.fromEntries

二维数组

```javascript
const result = Object.fromEntries([
    ['name', '守航人'],
    ['kemu', 'java,大数据,前端,云计算']
])
console.log(result); // {name: '守航人', kemu: 'java,大数据,前端,云计算'}
```



Map

```javascript
const m = new Map();
m.set('name', 'Lzh');
const result = Object.fromEntries(m);
console.log(result); // {name: 'lzh'}
```



## 2. 字符串方法扩展-trimStart与trimEnd

- trimStart：去掉字符串前面的空格

- trimEnd：去掉字符串后面的空格

```javascript
let str = ' iloveyou ';
console.log(str);
console.log(str.trimStart()); // 'iloveyou '
console.log(str.trimEend()); // ' iloveyou'

```



## 3. 数组方法扩展-flat与flatMap

### flat

将多维数组转化为低维数组，降低数组的维度

```javascript
const arr = [1, 2, 3, 4, [5, 6]];
console.log(arr.flat()); // [1, 2, 3, 4, 5, 6]
```

```javascript
const arr = [1, 2, 3, 4, [5, 6, [7, 8, 9]]];
console.log(arr.flat()); // [1, 2, 3, 4, 5, 6, [7, 8, 9]]
// 参数：深度
console.log(arr.flat(2)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```



### flatMap

```javascript
const arr = [1, 2, 3, 4];
const result = arr.flatMap(item => [item * 10]);
console.log(result); // [10, 20, 30 , 40]
```



## 4.Symbol.prototype.description

```javascript
let s = Symbol('守航人');
console.log(s.description); // 守航人
```



# 七、ECMAScript11

## 1.私有属性



## 2.Promise.allSettled方法



## 3.String.prototype.matchAll方法



## 4.可选链操作符



前面的属性存在再读取后面的属性，免去了层层判断的问题

```java
function main(config) {
    // const dbHost = config && config.db && config.db.host;
    const dbHost = config?.db?.host;
    console.log(dbHost); // 192.168.1.100
}

main({
    db: {
        host: '192.168.1.100',
        username: 'root'
    },
    cache: {
        host: '192.168.1.1',
        username: 'admin'
    }
})
```





## 5.动态import

用到加载不用不加载

```javascript
import('./hello.js').then(module => {
    module.hello();
})
```



## 6. Bigint类型

大整形

```javascript
let n = 521n;
console.log(n, typeof(n));// 521n "bigint"
```



函数

```javascript
let n = 123;
console.log(BigInt(n)); // 123n
console.log(Bigint(1.2)); // 报错不能加浮点型
```



## 7.绝对全局对象globalThis

始终指向全局对象window



## 8.EventLoop



**同步任务和异步任务**



>同步任务（synachronous）又叫做非耗时任务，指的是在主线程上排队执行的那些任务。只有前一个任务执行完毕，才能执行后一个任务。



> 异步任务（asynchronous）又叫做耗时任务，异步任务由JavaScript委托给宿主环境（node.js，浏览器）进行执行。当异步任务执行完成后，会通知JavaSctript主线程执行异步任务的回调函数。



**宏任务和微任务**



> JavaSctipt把异步任务又做了进一步的划分，异步任务又分为两类，分别为宏任务和微任务



:one: 宏任务（maccrotask）



- 异步Ajax请求
- serTimeout, setInterval
- 文件操作
- 其他宏任务



:two: 微任务（microtask）



- Promise.then, .catch和.finally
- process.nextTick
- 其他微任务





