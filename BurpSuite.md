# 功能介绍

Burp Suite是用于攻击web应用程序的集成平台，包含了许多工具。Burp Suite为这些工具设计了许多接口，以加快攻击应用程序的过程。所有工具都共享一个请求，并能处理对应的HTTP消息、持久性、认证、代理、日志、警报。

Burp Suite是由JAVA语言编写，所以Burpsuite是一款跨平台的软件。但是在测试过程中BurpSuite不像其他自动化测试工具不需要输入任何内容即可完成测试，而需要手动配置某些参数触发对应的行为才会完成测试。

BurpSuite 官方网址 https://portswigger.net/burp/

各版本的最主要区别在于web漏洞扫描

# 设置burpsuite字体

user options-> Display

# 配置浏览器代理

## 在浏览器中安装BurpSuite CA证书

1. 使用系统管理员权限打开浏览器
2. 再浏览器中输入http://burp/
3. 安装CA证书

# Proxy模块

Burp Proxy是Burp Suite以用户驱动测试流程功能的核心，通过代理模式，可以让我们拦截、查看、修改所有在客户端和服务端之间传输的数据

## intercept介绍

Forward表示将截断的HTTP或HTTPS请求发送到服务器
Drop表示将截断的HTTP或HTTPS请求丢弃
Intercept is on 和Intercept is off表示开启或关闭代理截断功能
Action表示将代理截断的HTTP或HTTPS请求发送到其他模块或做其他处理
对Intercept进行Raw Hex Params Header切换查看不同的数据格式

## HTTP history介绍

HTTP history用来查看提交过的HTTP请求
Filter可以过滤显示某些HTTP请求。点击FILTER就可以打开。对于指定URL可以选中右键点击，执行其他操作。WebSockets history与HTTP history功能类似

## Options介绍

Options具有的功能：代理监听设置、截断客户端请求、截断服务器响应、截断WebSocket通信服务端响应修改（绕过JS验证文件上传）、匹配与替换HTTP消息中的内容、通过SSL连接Web服务器配置、其他配置选项

### 设置Proxy Listener

通过设置Proxy Listeners来截断数据流量。比如设置监听端口等

### 设置Intercept lient Requests

通过设置Intercept Client Requests来截断符合条件的HTTP请求

### 设置Intercept Server Response

通过设置Intercept Server Response来筛选出符合条件的HTTP响应

### 设置截断Websocket通信以及修改Response的内容

### 匹配以及修改HTTP消息

可以修改HTTP请求和HTTP响应中的内容

### 设置使用SSL连接到Web服务器

设置使用Burp直接通过SSL直连到目标服务器

### 杂项设置

通过杂项设置对应的请求头等信息

# 通过BurpSuite截取WebApp流量

## WebAPP介绍

目前WebApp（手机APP）的通信仍然使用HTTP协议进行对应的通信。可以通过Burp设置代理，然后手机设置网络代理，通过Burp截断手机APP流量

### 手机网络设置

在手机网络设置中，填写对应的代理

# 通过BurpSuite剔除JavaScript脚本，实现JS绕过

## JavaScript脚本介绍

JavaScript一种直译式脚本语言，是一种动态类型、弱类型、基于原型的类型，内置支持类型。它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。
如：对于上传文件进行JS验证

## Burpsuite截断响应Javascript脚本

在Proxy模块中的Option下Response Modification,可以勾选Remove all JavaScript

# Target介绍

Burp Target组件主要包括站点地图、目标域、Target工具三部分组成。他们帮助渗透测试人员更好地了解目标应用的整体状况、当前的工作涉及哪些目标域、分析可能存在的攻击面等信息

## Target 作用域Scope介绍

Target Scope种作用域的定义比较宽泛，通常来说，当我们对某个产品进行渗透测试时，可以通过域名或者主机名去限制拦截内容，这里域名或主机名就是我们说的作用域；如果我们想限制得更为细粒度化，比如，你只想拦截login目录下得所有请求，这时我们也可以在此设置，此时，作用域就是目录

## Target 站点地图 Sitemap介绍

Site Map的左边为访问的URL，按照网站的层级和深度，树形展示整个应用系统的结构和关联其他域的URL情况；右边显示的是某一个URL被访问的明细列表。共访问哪些URL，请求和应答内容分别是什么，都有着详实的记录。基于左边的树形结构，我们可以选择某个分支，对指定的路径进行扫描和抓取

### 站点地图 目标分析

通过对站点地图 Sitemap进行分析，分析其中页面的提交参数等

## 站点地图比较

对于同一Web系统，不登录和登录系统是具有不同的响应的。针对这样的情况可以使用Burpsuite中Sitemap比较两者的区别

