## Think about a question?

一个问题：淘宝、京东、微信、抖音都有各自的功能，那么当我们退出系统的时候，下次再访问时，为什么信息还在？

解决之道：文件、数据库

为了解决上述问题，使用更加利于管理数据的东西-数据库，它能更有效的管理数据。

举一个生活化的案例说明：如果说图书馆是保存书籍的，那么数据库就是保存数据的。



## MySQL installation and configuration

:link: [CSDN的安装教程](https://blog.csdn.net/SoloVersion/article/details/123760428?ops_request_misc=&request_id=&biz_id=102&utm_term=mysql%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-123760428.nonecase&spm=1018.2226.3001.4187)

安装的端口一般默认3306



**启动mysql**

> 一定要在管理员窗口运行，要不然权限不够执行失败，这里的服务名根据MySQL版本不同服务名称不同，Win+R输入services.msc 查看服务名。

```mysql
net start mysql80;
```

停止mysql

```mysql
net stop mysql80;
```



## Database

连接数据库

```mysql
mysql -u root -p;
```

```mysql
mysql -h localhost -P 3306 -u root -p123456; //-p和密码没有空格，密码可以没有
```



创建数据库

```mysql
create database [if not exists] 数据库名 [default charset 字符集] [collate 排列规则]; 
```

删除数据库

```mysql
drop database [if exists] 数据库名;
```

查看所有数据库

```mysql
show databases;
```
 切换数据库

```mysql
use 数据库名;
```

查看当前处于哪个数据库

```mysql
select database();
```

查询数据库的定义信息

```mysql
show create database lzh_db01;
```

 备份数据库，在终端中执行

```mysql
mysqldump -u root -p -B 数据库 > d:\\bak.sql;
```

```mysql
mysqldump -u root -p密码 数据库 表1 表2 表n > d:\\文件名.sql;
```

恢复数据库，进mysql中执行

```mysql
source d:\\bak.sql;
```



## Engines

查看所有存储引擎

```mysql
show engines;
```

修改存储引擎

```mysql
alter table 表名 engine = 存储引擎;
```



**特点**

1.MYISAM不支持事务、也不支持外键，但其访问速度快，对事务完整性没有要求。
2.InnoDB存储引擎提供了具有提交、回滚和崩溃恢复能力的事务安全。但是比起MyISAM存储引擎，InnoDB写的处理效率差一些并且会占用更多的磁盘空间以留
数据和索引。
3.MEMORY存储引擎使用存在内存中的内容来创建表。每个MEMORY:表只实际对应一个磁盘文件。MEMORY类型的表访问非常得快，因为它的数据是放在内存中的，并且默认使用HASH索引。但是一旦MySQL服务关闭，表中的数据就会丢失掉，表的结构还在。



**如何选择？**

1.如果你的应用不需要事务，处理的只是基本的CRUD操作，那么MyISAM是不二选择，速度快
2.如果需要支持事务，选择InnoDB。
3.Memory存储引擎就是将数据存储在内存中，由于没有磁盘l./O的等待，速度极快。但由于是内存存储引擎，所做的任何修改在服务器重启后都将消失。（经典用法用户的在线状态0）



## Table

创建表

表的字符集，校验规则，存储引擎

```mysql
create table `user` (
    id int,
    `name` varchar(255),
    `password` varchar(32),
    birthday date
) character set utf8 collate utf8_bin engine innodb;
```



查看表的字段

```mysql
desc 表名;
```



## Data Type

### 数值类型

> 如果没有指定unsinged,则TINYINT.就是有符号
> 如果指定unsinged,则TINYINT就是无符号0-255

整形：tinyint[1] smallint[2] mediumint[3] int[4] bigint[8]

小数类型：float[单精度4] double[双精度8] decimal[M, D]



### 文本类型/字符串类型

char(0~255)  varchar(0~2^16-1) text(0~2^16-1) longtext(0~2^32-1)



### 二进制数据类型

blob(0~2^16-1) longblob(0~2^32-1)



### 日期类型

date(年月日) time(时分秒) datetime(YYYY-MM-DD HH:mm:ss) timestamp(时间戳) year(年)



## Data Definition Language

表操作

添加字段

```mysql
alter table 表名 add 字段名 类型（长度）[comment注释] [约束] ;
```

修改数据类型

```mysql
alter table 表名 modify 字段名 新数据类型（长度）;
```

修改字段名和字段类型

```mysql
alter table 表名 change 旧字段名 新字段名 类型（长度）[comment 注释] [约束];
```

修改表名

```mysql
alter table 表名 rename to 新表名;
rename table 表名 to 新表名;
```

删除字段

```mysql
alter table 表名 drop 字段名;
```

删除表

```mysql
drop table [if exists] 表名；
```



## Data Manipulation Language

### insert

给指定字段添加数据

```mysql
insert into 表名 (字段名1，字段名2，.....) values（值1，值2，......);
```

给全部字段添加字段

```mysql
insert into 表名 values (值1，值2，......);
```

批量添加数据

```mysql
insert into 表名 values (值1，值2，......)，(值1，值2，......), (值1，值2，......);
```



### update

```mysql
update 表名 set 字段1 = 值1，字段名2 = 值2，......[where 条件];
```



### delete

```mysql
delete from 表名 [where 条件];
```



## Data Query Language

### 单表查询

```mysql
select * from 表名; 
```





### 多表查询

> 笛卡尔集：多表查询的条件不能少于表的个数-1，否则会出现笛卡尔集。

> 自连接：指在同一张表的连接查询[将同一张表看做两张表]。





### 子查询

> 子查询：指嵌入在其它sql语句中的select语句，也叫嵌套查询。

> 单行子查询：指只返回一行数据的子查询语句。

> 多行子查询：指返回多行数据的子查询，使用关键字in。

> 多列子查询：则是指查询返回多个列数据的子查询语句



**合并查询**

```mysql
select ename,sal,job from emp where sal>2500 union all Select ename,sal,job from emp where job='MANAGER';
```

```mysql
select ename,sal,job from emp where sal>2500 union Select ename,sal,job from emp where job='MANAGER'; //去重
```



## Data Control Language

创建用户

```mysql
create user '用户名' @ '主机名'identified by '密码';
```



删除用户

```mysql
drop user '用户名' @ '主机名';
```





## Function

### 合计和统计函数

count(*)  count(column) sum()  avg()  max()  min()



### 分组统计

group by column having......



### 字符串函数

charset(str)  concat(string[,...])  instr(string, substring)  ucase(string)  lcase(string)  left(string, length)  length(string)  replace(str, search_str, replace_str) strcmp(string1, string2)  substring(str, position [, length])  ltrim(string)  rtrim(string)  trim(string)



### 数学函数

abs(num)  round(number)  bin (decimal_number)  ceiling (number)  floor (number)  conv(number, from_base, to_base)  format (number, decimal_places)

hex(DecimalNumber)  least (number,number [,..])  mod (numerator,denominator)  rang([seed])



### 时间日期函数

current_date()  current_time ()  current_timestamp()  date(datetime)  date_add(date2, INTERVAL d_value d_type)  date_sub(date2, INTERVAL d_value 

d_type)  datediff(date1,date2)  timediff (date1,date2)  now()  year|month|date(datetime)  from_unixtime()  last_date()



### 加密和系统函数

user()  datebase()  md5(str)  password(str)



### 流程控制函数

if(expr1,expr2,expr3)  ifnull(expr1,expr2)  select case when expr1 then expr2 when expr3 then expr4 else expr5 end;[类似多重分支，]



## External connection

左外

```mysql
表1 left join 表2 on
select dname,ename,job from dept left join emp on emp.deptno = dept.deptno;
```

右外

```mysql
表1 right join 表2 on
select dname,ename,job from emp right join dept on emp.deptno = dept.deptno;
```



## constraint

> 约束用于确保数据库的数据满足特定的商业规则。在mysql中，约束包括：not null、unique、primary key、foreign key、check五种。



**主键**

```mysql
create table t1(
    id int primary key ,
    `name` varchar(32),
    email varchar(32)
);
```

1.primary key不能重复而且不能为null。
2.一张表最多只能有一个主键，但可以是复合主键

```mysql
create table t2(
    id int,
    `name` varchar(32),
     primary key(id, name)
);
```

3.主键的指定方式有两种

- 直接在字段名后指定：字段名 primakry key
- 在表定义最后写primary key(列名)

4.使用desc表名，可以看到primary key的情况.

5.在实际开发中，每个表往往都会设计一个主键



**外键**

```mysql
```







## Indexes

主键索引

唯一索引

普通索引

全文索引





## Transaction

手动提交事务

```mysql
setAutoCommit(false);
```

开启事务

```mysql
start transaction;
```

设置保存点

```mysql
savepoint 保存点;
```

回退事务

```mysdql
rollback to 保存点;
```

回退全部事务

```mysql
rollback;
```

提交事务

```mysql
commit;
```



### 隔离

查看会话隔离级别

```mysql
select @@tx_isolation;
```

查看系统隔离级别

```mysql
select @@global.tx_isolation;
```

设置会话级别

```mysql
set session transaction isolation level 隔离级别;
```

设置会话级别

```mysql
set global transaction isolation level 隔离级别;
```




## View

> 视图是一个虚拟表，其内容由查询定义。同真实的表一样，视图包含列，其数据来自对应的真实表（基表）。



创建视图

```mysql
create view emp_view01 as select empno,ename,job,deptno from emp;
```

更新视图

```mysql
alter view emp_view01 as select xxx,xxx.... from emp;
```

查看创建视图的指令

```mysql
show create view emp_view01;
```

删除视图

```mysql
drop view emp_view01;
```



**视图最佳实践**

1.安全。一些数据表有着重要的信息。有些字段是保密的，不能让用户直接看到。这时就可以创建一个视图，在这张视图中只保留一部分字段。这样，用户就可以查询自己需要的字段，不能查看保密的字段。
2.性能。关系数据库的数据常常会分表存储，使用外键建立这些表的之间关系。这时，数据库查询通常会用到连接(JON)。这样做不但麻烦，效率相对也比较低。如果建立一个视图，将相关的表和字段组合在一起，就可以避免使用JON查询数据。
3.灵活。如果系统中有一张旧的表，这张表由于设计的问题，即将被废弃。然而，很多应用都是基于这张表，不易修改。这时就可以建立一张视图，视图中的数据直接映射到新建的表。这样，就可以少做很多改动，也达到了升级数据表的目的。



多表联合创建一个视图

> 针对emp,dept,和salgrade张三表，创建一个视图emp_view03，可以显示雇员编号，雇员名，雇员部门名称和薪水级别[即使用三张表，构建一个视图。

```mysql
create view emp_view03 as select empno,ename,dname,grade from emp,dept,salgrade
where emp.deptno dept.deptno and (sal between losal and hisal);
```



























































