密码存放 C：/Windows/System32/config/SAM

## 常见的服务

web服务
dns服务
dhcp服务
邮件服务
telnet服务
ssh服务
ftp服务
smb服务

## 端口

计算机“端口”是英文port的义译，可以认为是计算机与外界通讯交流的出口。按端口号可分为三大类：公认端口(Well Known Ports);注册端口(Registered Ports);动态和/私有端口(Dynamic and/or Private Ports)

### 端口的作用

IP地址与网络服务的关系是一对多的关系。实际上是通过“IP地址+端口号”来区分不同的服务的

端口并不是一一对应的

### 常见的端口

HTTP协议代理服务器常用端口号：80/8080/3128/8081/9080
FTP（文件传输）协议代理服务器常用端口号：21
Telnet(远程登录)协议代理服务器常用端口：23
TFTP（Trivial File Transfer Protocol）,默认的端口号为69/udp
SSH(安全登录)、SCP(文件传输)、端口重定向，默认端口号为22/tcp
SMTP Simple Mail Transfer Protocol (E-mail),默认的端口号为25/tcp (木马Antugen、EmailPassword Sender、Haebu Coceda、Shtrilitz Stealth、WinPC、WinSpy都开放这个端口)
POP3 Post Office Protocol(E-mail),默认的端口号为110/tcp
TOMCAT,默认的端口号为8080
WIN2003远程登录，默认的端口号为3389
Oracle数据库，默认的端口号为1521
MS SQL*SERVER数据库server，默认的端口号为1433/tcp 1433/udp
QQ，默认的端口号为1080/udp

### 黑客可以通过端口干什么

信息搜集
目标探测
服务判断
系统判断
系统角色分析

## 注册表

注册表(Registry,繁体中文版Windows称之为登录档)是Microsoft Windows中的一个重要的数据库，用于存储系统和应用程序的设置信息。早在Windows3.0推出OLE技术的时候，注册表就已经出现。随后推出的Windows NT是第一个从系统级别广泛使用注册表的操作系统。但是，从Windwos 95 开始，注册表才真正成为Windows用户经常接触的内容，并在其后的操作系统中继续沿用至今

### 打开注册表 regedit

### 注册表的作用

注册表是windows操作系统中的一个核心数据库，其中存放着各种参数，直接控制着windows的启动、硬件驱动程序的装载以及一些windows应用程序的运行，从而在整个系统中起着核心作用。这些作用包括了软、硬件的相关配置和状态信息，比如注册表中保存有应用程序和资源管理器外壳的初始条件、首选项和卸载数据等，联网计算机的整个系统的设置和各种许可，文件扩展名与应用程序的关联，硬件部件的描述、状态和属性，性能记录和其他底层的系统状态信息，以及其他数据等

### 注册表结构

1. HKEY_CLASSES_ROOT
管理文件系统。根据在windows中安装的应用程序的扩展名，该跟键指明其文件类型的名称，相应打开该文件所要调用的程序等等信息

2. HKEY_CURRENT_USER
管理系统当前的用户信息。在这个跟键中保存了本地计算机中存放的当前登录的用户信息，包括用户登录用户名和暂存的密码。在用户登录windows 98时，其信息从HKEY_USERS中相应的项拷贝到HKEY_CURRENT_USER中

3. HKEY_LOCAL_MACHINE
管理当前系统硬件配置。在这个跟键中保存了本地计算机硬件配置数据，此跟键下的子关键字包括在SYSTEM.DAT中，用来提供HKEY_LOCAL_MACHINE所需的信息，或者在远程计算机中可访问的一组键中

4. HKEY_USERS
管理系统的用户信息。在这个跟键中保存了存放在本地计算机口令列表中的用户标识和密码列表。同时每个用户的预配置信息都存储在HKEY_USERS跟键中。HKEY_USERS是远程计算机中访问的跟键之一

5. HKEY_CURRENT_CONFIG
管理当前用户的系统配置。在这个跟键中保存着定义当前用户桌面配置（如显示器等等）的数据，该用户使用过的文档列表（MRU），应用程序配置和其他有关当前用户的windows 98中文版的安装的信息

## 黑客常用的DOS命令

color 改变cmd颜色
ping -t -l 65500 ip 死亡之PingI(发送大于64K的文件并一直ping就成了死亡之ping)
ipconfig 查看ip
ipconfig /release 释放ip
ipconfig /renew 重新获得ip
systeminfo 查看系统信息
arp -a 查看同一网段下其他ip地址即物理地址
net view 查看局域网内其他计算机名称
shutdown -s -t 180 -c "你被黑了，系统马上关机" -r 重启 -a 取消
dir 查看目录
cd 切换目录
start www.cracer.com 打开网页
start 123.txt 打开123.txt
conpy con c:\123.txt 创建123.txt
hello cracer
ctrl+z 回车
md 目录名 创建目录
rd 123 删除文件夹
ren 原文件名 新文件名 重命名文件名
del 删除文件
type 文件名  查看文件内容
copy 复制文件
move 移动文件
tree 树形列出文件夹结构
telnet
net use k:\\192.168.1.1\c$  将对应ip的主机的c盘拿来做k盘
net use k:\\192.168.1.1\c$ /del
net start 查看开启了哪些服务
net start 服务名 开启服务
net stop 服务名 停止某服务
net user 用户名 密码 /add 建立用户
net user guest /active:yes 激活guest用户
net user 查看有哪些用户
net user 账户名 查看账户的属性
net locaLGroup administrators 用户名 /add 把“用户”添加到管理员中使其具有管理员权限，注意：administrator 后加s用复数
net user guest 12345 用guest用户登录后将密码改为12345
net password 密码 更改系统登录密码
net share 查看本地开启的共享
ney share ipc$ 开启ipc$共享
net share ipc$ /del 删除ipc$共享
net share c$ /del 删除C;共享
