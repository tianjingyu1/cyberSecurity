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
left()             从左侧开始取指定字符个数的字符串
