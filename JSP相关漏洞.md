# JSP相关漏洞

ST2漏洞
反序列化漏洞

## Struts2漏洞

Struts是Apache基金会Jakarta项目组的一个开源项目，Struts通过采用Java Servlet/JSP技术，实现了基于Java EE Web应用的Model-View-comtroller(MVC)设计模式的应用框架，是MVC经典设计模式中的一个经典产品。目前，Struts广泛应用于大型互联网企业、政府、金融机构等网站建设，并作为网站开发的底层模板使用，是应用最广泛的Web应用框架之一

### 漏洞挖掘

单个目标站进行测试

工具爬行
找到存在漏洞地址例如：xx.action
用相关工具进行测试即可

批量查找利用

url采集相关关键字
批量探测及利用

## java反序列化漏洞

2015年的1月28号，Gabriel Lawrence（@gebl）和Chris Frohoff(@frohoff)在AppSecCali上给出了一个报告，报告中介绍了Java反序列化漏洞可以利用Apache Commons Collections这个常用的Java库来实现任意代码执行，当时并没有引起太大的关注

2015年11月6日，FoxGlove Security安全团队的@breenmachine发布的一篇博客中介绍了如何利用java反序列化漏洞，来攻击最新版的WebLogic、WebSphere、JBoss、Jenkins、OpenNMS这些大名鼎鼎的Java应用，实现元尘代码执行

## Java反序列化漏洞简介

序列化就是把对象转换成字节流，便于保存在内存、文件、数据库中；反序列化即逆过程，由字节流还原成对象。Java中的ObjectOutputStream类de writeObject()方法可以实现序列化，类ObjectInputStream类的readObject()方法用于反序列化

# 其他漏洞

tomcat部署漏洞

访问tomcat manager页面
尝试弱口令爆破
登录管理页面
部署war文件
得到shell

# weblogic攻击

批量扫描WebLogic缺省的WEB管理端口(http为7001，http为7002),开放这两个端口的一般都是安装有WebLogic的主机

Google搜索关键字"WebLogic Server Administration Console inurl:console",URL后面是console结尾的，一般为目标

在找到的目标URL后面加上console，回车就会自动跳转到管理登录页面
尝试弱口令登录
1. 用户名密码均为:weblogic
2. 用户名密码均为:system
3. 用户名密码均为:portaladmin
4. 用户名密码均为:guest

