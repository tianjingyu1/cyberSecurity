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

# Burpsuite Spider介绍

Burp Spider的功能主要使用大型的应用系统测试，它能在很短的时间内帮助我们快速地了解系统的结构和分布情况

## Burpsuite Spider Control介绍

具有开关爬虫的功能，以及设置爬取目标。默认在Target设置

## Burpsuite Spider Option选项

Spider可选项设置由抓取设置、抓取代理设置、表单提交设置、应用登陆设置、蜘蛛引擎设置、请求消息头设置六个部分组成

被动抓取，不与服务器发生交互

表单提交，用来匹配和自动提交表单内容

设置应用程序登录与蜘蛛爬虫引擎

设置爬虫HTTP消息头

# Burpsuite Scanner介绍

Burp Scanner的功能主要是用来自动检测web系统的各种漏洞，我们可以使用Burp Scanner代替我们手工去对系统进行普通漏洞类型的渗透测试，从而能使得我们把更多得精力放在那些必须要人工去验证得漏洞上

扫描队列中包含了扫描进度

扫描配置live scanning

issue definitions 查看支持得漏洞扫描

设定探测位置

加快主动扫描速度

设定静态代码分析

## 主动扫描漏洞

针对存在漏洞得web应用程序进行主动扫描，分析漏洞，并导出漏洞报告

# Burpsuite Intruder模块介绍

再渗透测试过程中，我们经常请求Burp Intruder,它的工作原理是：Intruder在原始请求数据的基础上，通过修改各种请求参数，以获取不同的请求应答。每一次请求中，Intruder通常会携带一个或多个有效攻击载荷（Payload），在不同的位置进行攻击重放，通过应答数据的比对分析来获得需要的特征数据

## Burpsuite Intruder模块使用场景

1. 标识符枚举Web应用程序经常使用标识符来引用用户、账户、资产等数据信息

2. 提取有用的数据 在某些场景下，而不是简单地识别有效标识符，你需要通过简单标识符提取一些其他的数据

3. 模糊测试 很多输入型漏洞，如SQL注入，跨站点脚本和文件路径遍历可以通过请求参数提交各种测试字符串，并分析错误信息和其他异常情况，来对应用程序进行检测。由于应用程序的大小和复杂性，手动执行这个测试是一个耗时且繁琐的过程。这样的场景，您可以设置Payload，通过Burp Intruder自动化地对Web应用程序进行模糊测试

## Burpsuite Intruder模块使用步骤

设置代理，开启Burpsuite截断需要测试的HTTP请求

将截断的请i去发送到Burpsuite Intruder，设置Payload测试

筛选Intruder结果，选取有用信息

## 暴力破解用户密码

针对用户名和密码的破解，可以有以下方式：
1. 已知用户名，未知密码
2. 用户名和密码都未知
3. 已知密码，未知用户名

利用Burpsuite Intruder模块进行暴力破解

