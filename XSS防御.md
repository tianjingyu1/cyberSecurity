# XSS防御

- 使用XSS Filter
 XSS Filter的作用过滤用户(客户端)提交的有害信息，从而达到防范XSS攻击的效果。
 @ 输入过滤
 "永远不要相信用户的输入"是网站开发的基本常识，对于用户输入一定要有过滤，过滤，再过滤。

## 输入验证

 简单的说，输入验证就是对用户提交的信息进行有效验证，仅接受指定长度范围内的，采取适当格式的内容提交，阻止或者忽略除此之外的其他任何数据。
   输入是否仅包含合法的字符
   输入字符是否超过最大长度限制
   输入如果为数字，数字是否在指定的范围
   输入是否符合特殊的格式要求，如E-mail地址、IP地址等。

## 数据消毒

过滤和净化掉有害的输入。

@ 输出编码
HTML编码主要是用对应的HTML、实体代替字符。

@ 黑白名单
不管是采用输入过滤还是输出编码，都针对数据信息进行黑|白名单式的过滤。
黑名单，非允许数据
白名单，允许的数据

# 防御DOM-XSS

避免客户端文档重写、重定向或其他敏感操作。

beef
  XSS神器
  XSS漏洞的利用平台
beef的启动
  kali里
  工具  /usr/share/beef-xss
  配置文件 config.yaml
  启动beef 工具的方法
       beef-xss
       /usr/share/beef-xss/beef
  修改默认用户名和密码
  web 界面管理控制台
    http://172.16.132.128:3000/ui/panel

  Shellcode
    http://172.16.132.128:3000/hook.js
  
  测试页面
    http://172.16.132.128:3000/demos/butcher/index.html

  1. 浏览器劫持
  2. Cookie窃取欺骗  固定会话攻击
    data:cookie=username=admin;userid=1
```
document.cookie="username=admin";
document.cookie="userid=1";
```
  3. 利用浏览器漏洞getshell
  msf
  ms10002  xp
  ms12063  win7

  4. XSS平台
    XSS盲打