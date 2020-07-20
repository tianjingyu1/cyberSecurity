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

