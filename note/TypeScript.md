# 简介

typescript是js的超集，主要学习ts里面的原始类型、字面量类型、数组类型、函数类型、类类型、接口类型、类型别名、联合与交叉类型、枚举类型、泛型等类型

元素，以及类型推断、类型断言、类型缩小、类型放大等特性。

更加严谨，编写代码的时候静态类型的校验。



# 准备工作

安装编译TS的工具包

```js
npm i -g typescript; //tsc
```

```js
tsc -v; //查看typesctipt版本
```

初始化

```bash
tsc -init;
```

```base
tsc -p tsconfig.json --watch
```



# 原始类型

默认全局的变量都是块作用域，可以在ts中`export { }`让每个文件独立



```typescript
//根据初始的赋值来推导出变量的类型。以后str的类型不能改了
let str = "3"; 
//str = 2; // 报错原因：变量在定义的时候，类型已经确定下来了，不能修改
```

```typescript
// 常量不能改变指向（不能被修改），所以它的值就是它的类型
const num = 1;
//num = "2”;//报错原因：常量不能改变指向（不能被修改）
```



```js
let nub: number = 12
let str: string = '张三'
let isLoading: boolean = true
let nu: null = null
let unde: undefined = undefined
let sy: symbol = Symbol()
let vo:void = undefined;
```



```typescript
// 在ts中函数没有返回值，函数类型就是void
function a(): void {}

// 写undefined，需要返回undefined
function a(): undefined { return undefined }
```



# object和Object类型

object(常用)不包含基础数据类型

```typescript
let obj: object = {a:1};
let arr: object = [1];

// let num: object = 20; //报错不能将类型“number”分配给类型“object”。
// let str: object = "hello"; //报错
```



Object包含基础数据类型

{} === Object

```typescript
let obj1: Object = {b:1);
let arr1: Object = [2,3];
let num1: Object = 2;
let str1: Object = "2";
let bool1: Object = true;
```



# 数组类型

```js
let a: number[] = [1,2] <====> let a: Array<number> = [1,2]
let b: string[] = ['a', 'b']
let d: boolean[] = [true, false]
let c: (number | string)[] = [1, 'a']
```



# 联合类型

```js
let c: (number | string)[] = [1, 'a']
```



# 交叉类型

不会有任何值满足这个类型， 一般不会这么写

```typescript
let a:number & string;
```

如果一个属性出现多次类型的设置，需要都满足

```typescript
let obj: {name: string, age: number} & {height: number, age: 18};
obj = {name: "张三", age: 18, height: 1.80}
```



#  函数类型

```js
function add(num1: number, num2: number): number {
    return num1 + num2
}
add(1,2)
```



函数类型void

```js
function add(name: string): void {
    console.log('hello', name)
}
add('张三')
```



函数类型可选参数

```js
function add(num1?: number, num2?: number): number {
    return num1 + num2
}
add(1,2)
```



# 对象类型

```js
let obj:{name: string; age: number; sayHi(): void} = {
    name: '张三'，
    age: 19,
    sayHi() {}
}
```



对象类型可选属性

```js
function myAxios(config: { url: string; method?: string }) {}
myAxios({
  url: ''
})
```



接口继承extends

```js
interface Point2 { x: number; y: number }

interface Point3 extends Point2 { z: number }
```



元组

```js
let position: [number, number] = [1, 2]
```



# 接口



接口 =》对象：属性名、属性值

```typescript
interface IPerson {
    name: string,
    age: number,
    sex: string
}
let p: IPerson = {
    name: "张三",
    age: 18,
    sex: "男"
}
```



接口 =》数组：索引、元素

```typescript
interface INewArray {
    [index: number]: number
}
let p: INewArray = [1, 2, 3];
```



接口 =》函数：参数、返回值

```typescript
interface ISearchFunc {
    (a: string, b: string): boolean
}
const fun1: ISearchFunc = function(a: string, b: string): boolean {
    return a.search(b) !== -1;
}
console.log(fun1('123','1'));
```



可选属性：?

```typescript
interface IPerson {
    name: string,
    age: number,
    sex?: string
}
let p: IPerson = {
    name: "张三",
    age: 18
}
```



只读属性 readonly

```typescript
interface IPerson {
    readonly id: number,
    name: string,
    age: number,
    sex: string
}
let p: IPerson = {
    id: 1,
    name: "张三",
    age: 18,
    sex: "男"
}
```



任意属性：[]

```typescript
interface IPerson {
    name: string,
    age: number,
    sex?: string
    [propName: string]: any 任意属性和值
}
let p: IPerson = {
    name: "张三",
    age: 18,
    say: "我会跳舞"
}
```



# 类型断言

二种方式

- <类型>变量
- 变量 as 类型



# 类型别名

类型别名type，常用于联合类型

```js
type CustomArray = (number | string)[]

let arr: CustomArray = [1, 'a']
let arr1: CustomArray = [2, 'b']
```



# 字符串字面量类型

字符串字面量类型用来约束取值只能是某几个字符串中的一个

```typescript
type stringType = "张三" | "李四" | "王五"
let names: stringType = "张三"
```



举一反三：

```typescript
type numberType = 1 | 2 | 3;
let nms: numberType = 1;
```



# 元组

数组合并了相同类型的对象，而元组`Tuple`合并了不同类型的对象

- 对应类型的值
- 添加内容的时候要是元组中的类型

```typescript
let Tarr: [number, string] = [123, "张三"];
```



# 枚举

枚举(Eum)类型用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。



## 普通枚举



## 常数枚举



## 外部枚举





# 类



## 类的属性和方法



```typescript
class Person{
  name: string;
  age: number;
  constructor(name: string, age: number) {
    this.name = name,
    this.age = age
  }
  sayHi(str: string) {
    console.log(str);
  }
}
```



## 类的继承



```typescript
class Father{
  name: string;
  age: number;
  constructor(name: string, age: number) {
    this.name = name,
    this.age = age
  }
  sayHi(str: string) {
    console.log(str);
  }
}
class Son extends Father {
  constructor(name: string, age: number) {
    super(name, age);
  }
}
```



## 类-存取器

使用getter和setter可以改变属性的赋值和读取行为

```typescript
class Father{
  name: string;
  age: number;
  constructor(name: string, age: number) {
    this.name = name,
    this.age = age
  }
  get getName() {
    return this.name;
  }
  set setName(name: string) {
    this.name = name;
  }
}
```



## 类-静态成员

- 静态方法：使用static修饰符修饰的方法称为静态方法，它们不需要实例化，而是直接通过类来调用
- 静态属性：使用static修饰符修饰的属性称为静态属性，它们不需要实例化，而是直接通过类来调用

 ```typescript
 class Father{
   static name1: string = "张三"
   static sayHi() {
     console.log("hello");
     
   }
 }
 Father.name1;
 Father.sayHi;
 ```



## 类-public、private、protected修饰符

- public：默认就是public 

- private：私有的，只有本类可以访问

- protected：受保护的，本类和子类都可以访问



## 类-readonly以及参数属性



定义在属性上

```typescript
class Son {
    readonly name: string; // 只读属性，但是在构造器上是可以修改的
    constructor(name: string) {
        this.name = name
    }
}
```



readonly以及三个修饰符定义在参数上，会自动创建并且初始化参数

```typescript
class Son {
    constructor(readonly name: string) {
        // this.name = name
    }
}
```



## 类-抽象类和类的类型

为子类服务，就是让子类去继承实现它

- 不能被实例化

```typescript
abstract class A {
  abstract name: string; // 抽象属性
  abstract sayHi(); // 抽象方法
}

class B extends A {
  name: string;
  sayHi() {
    
  }
}
```



类的类型

- 向上转型
- 向下转型

```typescript
class A {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class B extends A {
  name: string;
  constructor(name: string) {
    super(name);
  }
}
const a: A = new A ("");
const b: B = new B (""); // const b: A = new B ("");
```



## 类实现接口以及接口继承接口

类实现接口：要实现接口中的方式

```typescript
interface IBase1 {
  a ();
}

interface IBase2 {
  b ();
}

class A  implements IBase1,IBase2{
  a () {}
  b () {}
}
```



```typescript
interface IBase1 {
  a ();
}

interface IBase2 {
  b ();
}
interface extends IBase1,IBese2 {
    
}
```



## 接口继承类

```typescript
class Person{
    name: string;
    sayHi() {
        console.log("hello");
    }
}

interface IP extends Person {
	age: number;
}

let person: IP = {
    name: "张三",
    age: 19,
    sayHi() {
        console.log("hello");
    }
}
```



# 声明合并

如果定义了两个相同名字的函数、接口或类，那么它们会合并成一个类型

- 合并的属性类型必须是唯一的

接口的合并

```typescript
interface IBase1 {
  name: "李四"
}

interface IBase1 {
  name: "李四",
  age: 3
}
const cat: Cat = {
    name: "李四",
    age: 3
}
```



# 泛型

泛型(Generics)是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。



## 基本使用

需求：定义一个函数，传入两个参数，第一个参数是数据，第二个参数是数量
函数的作用：根据数量产生对应个数的数据，存放在一个数组中
(123,3)-->[123,123,123]

- T表示任意输入的类型
- 原则上不推荐使用any
- 如果没有确定就会进行类型推断

```typescript
function getArr<T>(value: T, count: number): T[] {
    const arr: T[] = [];
    for(let i = 0; i < count; i++) {
        arr.push(value);
    }
    return arr;
}
console.log(getArr(123, 3));
console.log(getArr<string>("李四", 3));
```



## 多个泛型参数

[123, "123"] ===> ["123", 123]

```typescript
function updateArr<T,U>(t: [T, U]): [U, T] {
    return [t[1], t[0]];
}
console.log(updateArr<string, number>("123", 123));
console.log(updateArr<number,string>(123, "123"));
```



## 泛型约束

在函数内部使用泛型变量的时候，由于事先不知道它是哪种类型，所以不能随意的操作它的属性或方法



获取一个参数的长度
泛型约束，约束这个任意输入的类型，必须要有length属性

```typescript
interface ILength {
    length: number
}
function getLength<T extends ILength>(x: T): number {
    return x.length
}
console.log(getLength("lan"))
```



## 泛型接口和泛型类



泛型接口

```typescript
interface IArr<T> {
    name: T
}
let p: IArr<string> = {
	name: ""
}
let p1: IArr<number> = {
	name: 123
}

```

```typescript
// 定义一个泛型接口
interface IArr {
    <T>(value: T, count: number): Array<T>
}

let getArr: IArr = function <T>(value: T, count: number): T[] {
    const arr: T[] = [];
    for(let i = 0; i < count; i++) {
        arr.push(value);
    }
    return arr;
}
```

```typescript
// 定义一个泛型接口
interface IArr<T> {
    (value: T, count: number): Array<T>
}

let getArr: IArr<string> = function <T>(value: T, count: number): T[] {
    const arr: T[] = [];
    for(let i = 0; i < count; i++) {
        arr.push(value);
    }
    return arr;
}
```



泛型类

```typescript
class Person<T> {
    name: string;
    age: T;
    constructor(name: string, age: T) {
        this.name = name;
        this.age = age;
    }
}
const person1 = new Person<string>("张三", "18");
const person2 = new Person<number>("张三", 18);
```

































































