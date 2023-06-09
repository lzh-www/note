## 1.Java的概述

-  Java 语言是面向对象的(oop)
- Java 语言是健壮的。Java 的强类型机制、异常处理、垃圾的自动收集等是 Java 程序健壮性的重要保证
- Java 语言是跨平台性的。[即: 一个编译好的.class 文件可以在多个系统下运行，这种特性称为跨平台]
- Java 语言是解释型的[了解] 解释性语言：javascript,PHP, java 编译性语言: c / c++ 区别是：解释性语言，编译后的代码，不能直接被机器执行,需要解释器来执行, 编译性语言, 编译后的代码, 可 以直接被机器执行, c /c++



## 2.变量

> 变量相当于内存中一个数据存储空间的表示，你可以把变量看做是一个房间的门牌号，通过门牌号我们可以找到房 间，而通过变量名可以访问到变量(值)。





### 2.1数据类型

> 每一种数据都定义了明确的数据类型，在内存中分配了不同大小的内存空间(字节)。

![](E:\Typora笔记\images\屏幕截图 2022-11-08 153257.png)



### 2.2基本数据类型



#### 2.2.1整数类型

##### 1.基本介绍

> Java 的整数类型就是用于存放整数值的，比如 12 , 30, 3456 等



#### 2.2.2浮点类型

##### 1.基本介绍

> Java 的浮点类型可以表示一个小数，比如 123.4 ，7.8 ，0.12 等等



#### 2.2.3字符类型

##### 1.基本介绍

> 字符类型可以表示单个字符,字符类型是 char，char 是两个字节(可以存放汉字)，多个字符我们用字符串 String。



##### 2.字符类型使用细节

- 字符常量是用单引号`('')`括起来的单个字符。
- Java中还允许使用转义字`\`来将其后的字符转变为特殊字符型常量。例如：char c3 = '\n'; '\n'表示换行符
- 在java中，==char的本质是一个整数==，在输出时，是unicode码对应的字符。
- 可以直接给char赋一个整数，然后输出时，会按照对应的unicode字符输出[97-》a]。
- char类型是可以进行运算的，相当于一个整数，因为它都对应有Unicode码。





#### 2.2.4布尔类型

##### 1.基本介绍

> boolean类型数据只允许取值true和false，无null。boolean类型适用于逻辑运算，一般用于程序流程控制。





#### 2.2.4ASCII





#### 2.2.5Unicode







### 2.3基本数据类型的转换

#### 2.3.1自动类型转换

> 当java程序在进行赋值或者运算时，精度小的类型自动转换为精度大的数据类型，这就是自动类型转换。

![](E:\Typora笔记\images\屏幕截图 2022-11-08 232108.png)



#### 2.3.2自动类型转换注意和细节

1. 有多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的那种数据类型，然后再进行计算。
2. 当我们把精度（容量）大的数据赋值给精度（容量）小的数据类型时，就会报错，反之就会进行自动类型转换。
3. (byte,short) 和 (char)之间不会相互自动转换。
4. byte，short，char他们三者可以计算，在计算时首先转换为int类型。
5. boolean不参与转换。
6. 自动提升原则：表达式结果的类型自动提升为操作数中最大的类型。



#### 2.3.3强制类型转换

> 自动类型转换的逆过程，将容量大的数据类型转换为容量小的数据类型。使用时要加上强制转换符 ( )，但可能造成 精度降低或溢出,格外要注意。

```java
int j = 100;
byte b = (byte)j;
```



#### 2.3.4强制类型转换注意和细节

1. 当进行数据的大小从 大 ----》小，就需要使用到强制转换。
2. 强转符号只针对于最近的操作数有效，往往会使用小括号提升优先级。
3. char类型可以保存int的常量值，但不能保存int的变量值，需要强转。
4. byte和short，char类型再进行运算时，当做int类型处理。



### 2.4基本数据类型和String类型的转换

> 在程序开发中，我们经常需要将基本数据类型转成String类型。获取将String类型转成基本数据类型。



#### 2.4.1 基本数据类型转String类型

> 将基本类型的值 + ""即可；



#### 2.4.2 String类型转基本数据类型

> 通过基本类型的包装类调用parseXX方法即可；





## 3.运算符



### 3.1运算符介绍

> 运算符是一种特殊的符号，用以表示数据的运算、赋值和比较等。


- 算术运算符
- 赋值运算符
- 关系运算符 [比较运算符] 
- 逻辑运算符
- 位运算符 [需要二进制基础]
- 三元运算符



### 3.2基本运算符



#### 3.2.1算术运算符

> 算术运算符是对数值类型的变量进行运算的，在 Java 程序中使用的非常多。



#### 3.2.2赋值运算符

> 赋值运算符就是将某个运算后的值，赋给指定的变量。



#### 3.2.3关系运算符 [比较运算符] 

> 关系运算符的结果都是 boolean 型，也就是要么是 true，要么是false; 关系表达式，经常用在if结构的条件中或循环结构的条件中。



#### 3.2.4逻辑运算符

> 用于连接多个条件（多个关系表达式），最终的结果也是一个 boolean 值。



#### 3.2.5位运算符 [需要二进制基础]

> java 中有 7 个位运算(&、|、 ^ 、~、>>、<<和 >>>



#### 3.2.6三元运算符

> 条件表达式 ? 表达式 1: 表达式2；





**运算符优先级**
1.运算符有不同的优先级，所谓优先级就是表达式运算中的运算顺序。如右表，上一行运算符总优于下一行。
2.只有单目运算符、赋值运算符是从右向左运算的梳理小结：小伙伴有一个大致印象，使用多了，就熟悉
1)() , {} 等

2)单目运行 ++ --
3)算术运算符
4)位移运算符
5)比较运算符
6)逻辑运算符
7)三元运算符
8)赋值运算符





### 3.3标识符的命名规则和规范

- 标识符概念

1. Java对各种变量、方法和类等命名时使用的字符序列称为标识符
2. 凡是自己可以起名字的地方都叫标识符int num1=90:

- 标识符的命名规则（必须遵守）

1.  由26个英文字母大小写，0-9，_或$组成
2. 数字不可以开头。int 3ab = 1; //错误
3. 不可以使用关键字和保留字，但能包含关键字和保留字。
4. Java中严格区分大小写，长度无限制。int totalNum=10;int n = 90;
5. 标识符不能包含空格。int a b=90;

- 标识符命名规范
  1.包名：多单词组成时所有字母都小写：aaa.bbb.ccc/比如com.hsp.crm
  2.类名、接口名：多单词组成时，所有单词的首字母大写：XxxYyyZzz
  比如：TankShotGame==大驼峰==
  3.变量名、方法名：
  多单词组成时，第一个单词首字母小写，第二个单词开始每个
  单词首字母大写：xxxYyyZzz
  比如：tankShotGame ==小驼峰==
  4.常量名：所有字母都大写。多单词时每个单词用下划线连接：XXX_YYY _ZZZ
  比如：定义一个所得税率TAX_RATE
  5.后面我们学习到类，包，接口，等时，我们的命名规范要这样遵守，更加详细的看文档.



### 3.4关键字

> 被 Java 语言赋予了特殊含义，用做专门用途的字符串



### 3.5保留字

> Java保留字：现有Java版本尚未使用，但以后版本可能会作为关键字使用。自己命名标识符时要避免使用这些保留字
> byValue、cast、future、generic、inner、operator、outer、rest、var、goto、const





### 3.6键盘输入语句

>  在编程中，需要接收用户输入的数据，就可以使用键盘输入语句来获取。
> Input.java，需要一个扫描器（对象），就是Scanner

```java
import java.util.Scanner;

Scanner myScanner = new Scanner(System.in);
System.out.println("请输入名字")；
String name = myScanner.next();
System.out.println("请输入年龄")；
int age = myScanner.nextInt();
System.out.println("请输入薪水")；
double sal = myScanner.nextDouble();
```



### 3.7进制

进制介绍

对于整数，有四种表示方式：
二进制：0,1，满2进1.以0b或0B开头。
十进制：0-9，满10进1。
八进制：0-7，满8进1. 以数字0开头表示。
十六进制：0-9及A(10)F(15),满16进1.以0x或0X开头表示。此处的A-F不区分大小写。






## 4.程序控制结构



### 4.1程序流程控制介绍

> 在程序中，程序运行的流程控制决定程序是如何执行的，是我们必须掌握的，主要有三大流程控制语句。
- 顺序控制
- 分支控制
- 循环控制
- 多重循环控制



### 4.2顺序控制

> 程序从上到下逐行地执行，中间没有任何判断和跳转。



### 4.3分支控制

#### 4.3.1if-else

- 单分支
- 双分支
- 多分支





#### 4.3.2switch

##### 1.基本语法

```java
switch(表达式) {
    case 常量1:
        语句块1;
        break;
    case 常量2:
        语句块2;
        break;
        ...
    case 常量n:
        语句块n;
        break;
    default:
        default语句块;
        break;
}
```



### 4.4循环控制

#### 4.4.1for





#### 4.3.2while

##### 1.基本语法

```java
循环变量初始化;
while(循环条件) {
    循环体(语句);
    循环变量迭代;
}
```



#### 4.3.3do-while

##### 1.基本语法

```java
循环变量初始化;
do {
    循环体(语句);
    循环变量迭代;
}while(循环条件);
```





### 4.5多重循环控制





## 5.数组-排序-查找



### 5.1数组

> 数组可以存放多个同一类型的数据。数组也是一种数据类型，是引用类型。即：数组就是一组数据

 

#### 5.1.1数组的使用

##### 1.使用方式1-动态初始化

```java
数据类型 数组名[] = new 数据类型[大小];
```

```java
int a[] = new int[5]; //创建了一个数组，名字a，存放5个int;
```



##### 2.使用方式2-动态初始化

先声明数组，再创建数组

```java
int a[]; // a是Null
int[] a;
```

```java
a = new int[10]; // 分配内存空间
```



##### 3.使用方式3-静态初始化

```java
数据类型 数组名[] = {元素值, 元素值...}; // 适合用在知道数组有多少元素，具体值;
```

```java
double[] hens = {3, 5, 1, 3.4, 2, 50};
```



#### 5.1.2数组使用注意事项和细节

- 数组是多个相同类型数据的组合，实现对这些数据的统一管理
- 数组中的元素可以是任何数据类型，包括基本类型和引用类型，但是不能混用
- 数组创建后，如果没有赋值，有默认值 int 0，short 0,  byte 0,  long 0,  float 0.0,  double 0.0，char \u0000，boolean false，String nul
- 使用数组的步骤 1. 声明数组并开辟空间 2.给数组各个元素赋值 3.使用数组
- 数组的下标(索引)是从 0开始的
- 数组下标必须在指定范围内使用，否则报：下标越界异常，比如 int [] arr = new int[5]; 则有效下标为 0-4
- 数组属引用类型，数组型数据是对象(object)



#### 5.1.3数组赋值机制

> 基本数据类型：值传递/值拷贝
>
> 引用类型： 引用传递/地址拷贝



#### 5.1.4数组拷贝

> 重新开辟一个数据空间，for循环赋值即可



#### 5.1.5数组翻转

> 2种方法。交换，倒序。



#### 5.1.6数组扩容

> 定义一个比原先大一的数组，赋值。



#### 5.1.7数组缩减

> 



#### 5.1.8二维数组



## 6.面向对象编程(基础)



### 6.1类与对象

- 类是抽象的，概念的，代表一类事物，比如人类，猫类，即它是数据类型
- 对象是具体的，实际的，代表一个具体事物，即是实例
- 类是对象的模板，对象是类的一个个体，对应一个实例





```js
class Cat {
    String name;
    int age;
    String color;
}
```

```js
Cat cat1 = new Cat();
cat1.name = "小花";
cat1.int = 4;
cat1.color = "白色";
```



**对象在内存中存在形式**







### 6.2成员方法



### 6.3成员方法传参机制



### 6.4重载(overload)



### 6.5可变参数



### 6.6作用域



### 6.7构造器



### 6.8this







































































