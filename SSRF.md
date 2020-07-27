# SSRF 概述及其危害

## SSRF概述

互联网上的很多Web应用提供了从其他服务器（也可以是本地）获取数据的功能。使用用户指定的URL，Web应用可以获取图片、文件资源（下载或读取）。

用户可以从本地或者URL的方式获取图片资源，交给百度识图处理。如果提交的是URL地址，该应用就会通过URL寻找图片资源。如果Web应用开放了类似于百度识图这样的功能，并且对用户提供的URL和远端服务器返回的信息没有进行合适的验证或者过滤，就可能存在“请求伪造”的缺陷。请求伪造，顾名思义就是攻击者伪造正常的请求，以达到攻击的目的，是常见的Web安全漏洞之一。如果“请求伪造”发生在服务器端，那么这个漏洞就叫做“服务器端请求伪造”，英文名字为Server-Side Request Forgery,简称SSRF。

SSRF（Server-Side Request Forgery，服务器端请求伪造）是一种攻击者发起的伪造由服务器端发起请求的一种攻击，也是常见Web安全漏洞（缺陷或者风险）之一。

## SSRF危害

@ 端口扫描
@ 内网web应用指纹识别
@ 攻击内网web应用
@ 读取本地文件

## SSRF常见代码实现

再服务器端实现通过URL从服务器（外部或者内部）获取资源功能的方法有很多，此处使用PHP语言和curl扩展实现改功能

通过phpinfo()函数查看对curl扩展的支持，现在大部分wamp套件均支持curl扩展

服务器端代码如下

```
<?php
if (isset($_REQUEST['url']))
{
    $link = $_REQUEST['url'];
    $filename = './curled/'.time().'.txt';
    $curlobj = curl_init($link);
    $fp = fopen($filename,"w");
    curl_setopt($curlobj,CURLOPT_FILE,$fp);
    curl_setopt($curlobj,CURLOPT_HEADER,0);
    curl_setopt($curlobj,CURLOPT_FOLLOWLOCATION,TRUE);
    curl_exec($curlobj);
    curl_close($curlobj);
    fclose($fp);
    $fp = fopen($filename,"r");
    $result = fread($fp, filesize($filename));
    fclose($fp);
    echo $result;
}else{
    echo "?url=[url]";
}
?>
```

将以上代码保存成文件[ssrf_curl.php]。该段代码实现了从服务器获取资源的基本功能，
提交
[?url=http://www.baidu.com]
页面就会载入百度首页的资源

同时，获取的资源文件会保存在[./curled]中，并以发起请求时间的unix时间戳命名。

## SSRF利用

- 访问正常文件

访问正常的文件，提交参数[?url=http://www.baidu.com/robots.txt]

- 端口扫描(扫描内网的机器的端口)

当访问未开放端口，脚本会显示空白或者报错。提交参数[?url=dict://127.0.0.1:1234] //字典协议

当访问开放端口时，脚本会显示banner信息。
提交参数[?url=dict://172.16.132.160:22]（有成功率）
提交参数[?url=dict://127.0.0.1:3306]
提交参数[?url=dict://127.0.0.1:21]

- 读取系统本地文件

利用file协议可以任意读取系统本地文件，提交参数
[?url=file://c:\windows\system32\drivers\etc\hosts]

- 内网Web应用指纹识别

识别内网应用使用的框架，平台，模块以及cms可以为后续的渗透测试提供很多帮助。大多数web应用框架都有一些独特的文件和目录。通过这些文件可以识别出应用的类型，甚至详细的版本。根据这些信息就可以针对性的搜集漏洞进行攻击。

比如可以通过访问下列文件来判断phpMyAdmin是否安装以及详细版本
[?url=http://localhost/phpmyadmin/README]

- 攻击内网应用

内网的安全通常都很薄弱，溢出、弱口令等一般都是存在的。通过ssrf攻击，可以实现对内网的访问，从而可以攻击内网应用或者本地主机，获得shell，这里的应用包括服务、Web应用等。

仅仅通过get方法可以攻击的web应用有很多，比如struts2命令执行等。

weblogic 从 ssrf 到 redis 未授权访问到getshell
  redis数据库
    未授权访问        不需要用户名和密码就可以访问数据库，读写文件

## SSRF漏洞的挖掘

对外发起网络请求的地方都可能存在SSRF漏洞，列举图片加载，分享页面，在线翻译，未公开的api（从远程服务器请求资源文件处理，编码处理，属性信息处理等）

## SSRF的防御

@ 限制协议

仅允许http和https请求

@ 限制IP

避免应用被用来获取内网数据，攻击内网

@ 限制端口

限制请求的端口为http常用的端口，比如 80,443,8080,8090

@ 过滤返回信息

验证远程服务器对请求的响应是比较简单的方法

@ 统一错误信息

避免用户可以根据错误信息来判断远端服务器的端口状态