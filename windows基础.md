密码存放 C：/Windows/System32/config/SAM

perflogs是windows7的日志信息，如磁盘扫描 错误信息，删掉可以，但不建议删，删掉反而会降低系统速度，Perflogs是系统自动生成的

## 常见的服务

win+r service.msc

- 服务

服务是一种应用程序类型，它在后台运行

服务应用程序通常可以在本地和通过网络为用户提供一些功能，例如客户端/服务器应用程序、Web应用程序、数据库服务器以及其他基于服务器的应用程序

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

### 端口分类

知名端口即众所周知的端口号，范围从0-1023，这些端口号一般固定分配给一些服务。比如21端口分配给FTP服务，25端口分配给SMTP服务（简单邮件传输协议）服务，80端口分配给HTTP服务，135端口分配给RPC（远程过程调用）服务等等

动态端口（Dynamic Ports）

动态端口的范围从1024到65535，这些端口号一般不固定分配给某个服务，也就是说许多服务都可以使用这些端口。只要运行的程序向系统提出访问网络的申请，那么系统就可以从这些端口号中分配一个供该程序使用，就会释放所占用的端口号

不过，动态端口也常常被病毒木马程序所占用，如冰河默认连接端口是7626、WAY 2.4是8011、Netspy是7306、YAI病毒是1024等等

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
netstat -a 查看开启了哪写端口，常用netstat -an
netstat -n 查看端口的网络连接情况，常用netstat -an
netstat -v 查看正在进行的工作
at id号 开启已注册的某个计划任务
at /delete 停止所有计划任务，用参数/yes则不需要确认就直接停止
at id号 /delete 停止某个已注册的计划任务
at 查看所有的计划任务
attrib 文件名（目录名） 查看某文件（目录）的属性
attrib 文件名 -A -R -S -H 或 +A +R +S +H去掉（添加）某文件的存档，只读，系统，隐藏属性；用+则是添加为某属性

## 批处理文件

批处理文件是dos命令的组合文件，写在批处理文件的命令会被逐一执行
后缀名为.bat

新建批处理文件
新建一个文本文档保存时把后缀名改为bat
也可以用命令
copy con 123.bat
net user crecer 123123 /add
net localgroup administrator cracer /add
Ctrl+z
回车

## windows快捷键的使用

F1      显示当前程序或者windows的帮助内容
F2      当你选中一个文件的话，这意味着“重命名”
F3      当你在桌面上的时候是打开“查找：所有文件”对话框
Ctrl+F4  关闭当前应用程序中的当前文本（如word中）
F5      刷新
Ctrl+F5  强行刷新
Ctrl+F6  切换到当前应用程序中的下一个文本（加shift可以跳到前一个窗口）
F10或ALT  激活到当前程序的菜单栏
windows键或Ctrl+ESC  打开开始菜单
Ctrl+ALT+DELETE  在win9x中打开关闭程序对话框
DELETE  删除被选择的选择项目，如果是文件，将被放入回收站
SHIFT+DELETE  删除被选择的选择项目，如果是文件，将被直接删除而不是放入回收站
Ctrl+N   新建一个新的文件
Ctrl+O   打开“打开文件”对话框
Ctrl+P   打开“打印”对话框
Ctrl+S   保存当前操作的文件
Ctrl+X   剪切被选择的项目到剪切板
Ctrl+insert 或Ctrl+C  复制被选择的项目到剪切板
shift+insert 或 Ctrl+V   粘贴剪切板中的内容
ALT+BACKSPACE 或Ctrl+Z   撤销上一步的操作
ALT+SHIFT+BACKSPACE   重做上一步被撤销的操作
windows+M    最小化所有被打开的窗口
windows+Ctrl+M   重新将恢复上一项操作前窗口的大小和位置
windows+E   打开资源管理器
windows+F   打开“查找：所有文件”对话框
windows+R   打开“运行”对话框
windows+BREAK 打开“系统属性”对话框
windows+Ctrl+F   打开“查找：计算机”对话框
shift+F10或鼠标右击 打开当前活动项目的快捷菜单
shift   在放入CD的时候按下不放，可以跳过自动播放CD。在打开word的时候按下不放，可以跳过自启动的宏
ALT+F4   关闭当前应用程序
ALT+SPACEBAR  打开程序最左上角的菜单
ALT+TAB   切换当前程序
ALT+ESC   切换当前程序
ALT+ENTER   将windows下运行的MSDOS窗口在窗口和全屏幕状态间切换
PRINT SCREEN   将当前屏幕以图象方式拷贝到剪切板
ALT+PRINT SCREEN   将当前活动程序窗口以图象方式拷贝到剪贴板
在IE中：
ALT+PRINT ARROW   显示前一页（前进键）
ALT+LEFT ARROW  显示后一页（后退键）
Ctrl+TAB   在页面上的各框架中切换（加shift反向）

### 执行菜单上相应的命令 ALT+菜单上带有下划线的字母
关闭多文档界面程序中的当前窗口 Ctrl+ F4
关闭当前窗口或退出程序  ALT+F4
复制 Ctrl+ C
剪切 Ctrl+ X
粘贴 Ctrl+ V
删除 DELETE
### 在任务栏上的按扭间循环windows+TAB
显示“查找：所有文件”windows+F
显示“查找：计算机”Ctrl+windows+F
显示“帮助” windows+F1
显示“运行” 命令 windows +R
显示“开始”菜单 windows
显示“系统属性”对话框 windows+break
显示“windows资源管理器” windows+E
最小化或还原所有窗口 windows+D
撤销最小化所有窗口 shift+windows+M
### 使用对话框中的快捷键
目的快捷键
取消当前任务 esc
在选项上向后移动 shift+tab
在选项卡上向后移动 ctrl+shift+tab
在选项上向前移动tab
在选项卡上向前移动 ctrl+tab

## 系统优化

### 修改启动项

windows+r菜单在搜索框中输入“msconfig”命令打开系统配置窗口后找到“启动”选项

### 加快系统启动速度

windows+r菜单在搜索程序框中输入msconfig命令，打开系统配置窗口后找到“引导”选项（英文系统是Boot）
点击“高级选项”此时可以看到我们将要修改的设置项了

### 提高窗口切换提速

右击计算机属性--性能信息和工具--调整视觉效果
先点击让windows选择计算机的最佳设置--再点击自定义--把最后的勾选去掉--确定

### 使用工具优化

360安全卫士
魔方注册表清理工具
鲁大师
系统优化大师

## 登录密码破解

### 使用启动U盘破解

下载“电脑店U盘启动制作工具”
安装
备份U盘工具
再制作U盘启动过程中会删除U盘上所有数据，且不可恢复，故此需备份U盘数据
破解密码

### 使用工具对hash值破解

lc5

## 手动清除木马

### 查找开机启动项

通过msconfig查找启动项 开始 程序 启动

### 查询服务

service.msc打开

### 查看网络端口连接

netstat -anp

常见木马端口 4444 8888 9527

## 配置黑客桌面

雨滴桌面
