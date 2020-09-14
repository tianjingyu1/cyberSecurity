# kali简介

kali是一款安全测试工具，使用其主要做渗透测试、安全审计等

## linux

Redhat linux、Centos、redflag(红旗)、debian、opensuse、ubuntu、arch、freeBSD、kali等等

其中kali linux主要用于黑客攻防、渗透测试、安全审计

特点：安全、稳定 占资源少
缺点：操作复杂，需要专业工程师

## windows

windows server2003 、windows server 2008、 windows server 2012、 windows server 2016

特点：图形界面 简单易用
缺点：占用资源较高、安全性差、稳定性差

## unix

solaris:AIX(IBM)  HP-UX

# kali linux介绍

早期：back track(BT3 BT4 BT5)基于Ubuntu
现在：kali linux 基于debian (2014年改名)
kali官网 www.kali.org
中国 www.kali.org.cn

# 几个常用的简单命令

列出目录下的文件  ls
列出目录下文件的详细信息  ls -l
列出目录下所有文件的详细信息  ls -a
更换工作目录  cd
显示当前所在目录  pwd
返回上级目录  cd ..
返回上一次操作的目录  cd -
返回家目录  cd ~

- linux的命令结构 command option arguments(命令 选项 内容)

创建新的空白目录 mkdir dir-name
复制文件或目录 cp -r dir destination
删除空目录 rmdir dir-name
删除目录或文件 rm dir
删除全部 rm -rf *（慎用）
移动格式 mv dir/file destination
重命名格式 mv dir/file-name newname

## 文件查看

查看文件 cat file
看头几行 head file
看后头几行 tail file
反向查看 tac file
带行号查看 nl file
一页一页显示 more file
类似more,可往前翻 less file

查看文件的大小 du / du -h filename
检查文件系统的磁盘空间占用情况 df / df -hss filename

## 使用文档

命令 -h
man 命令(有时当某命令不适用时可试一下其他两个)
命令 --help(完整单词前加--)

## 查看和结束系统进程

ps -aux |grep root(|grep==检索)
- -a all
- -u userlist
- -x 和a选项共用时，列出所有进程

kill PID / kill -9 PID(级别更高)

## vi编辑器

三种模式：一般(查看)，输入(IAO)，命令(:)

- touch file 新建一个文件
- vi file 如果文件不存在，创建后并打开

1. 普通模式
2. 英文输入法下，按I/A/O进入插入模式
3. 按ESC退出插入模式，进入命令模式， shift :wq保存退出

## 查看用户信息

cat /etc/passwd

用户名：密码(不再使用 x占位)：UID：GID;用户全名：home目录：shell 全部

## 增加组和用户/给用户指定组(组可以方便管理)

useradd username  增加用户
userdel username 删除用户
groupadd groupname 增加组
groupdel groupname 删除组

### 查看组

查看组 cat /etc/group
查看组的最后修改时间 ls -al /etc/group
查看用户个数 cat /etc/passwd |wc -l

## 查看密码文件/修改用户密码

查看用户密码 cat /etc/shadow
查看指定用户密码 cat /etc/shadow |grep username
修改用户密码 passwd username

## 文件权限

4=read 2=wrute 1=excute

配置权限 chmod 777 file
递归更改权限 chmod -R 777 file
加减权限 chmod +/-x file
更改文件的属主 chown -r 属主名：属组名 文件名

## 几个符号的含义

.  代表当前所在路径
.. 代表上一级目录
-  代表上一个工作的目录
~  代表家目录
./ 代表执行

## find命令查找文件

find 范围 -类型 查找的内容
find -name file-name 找文件
find path -user file-name 某路径下用户的文件
find path -empty 查找空文件和空目录
find /nouser 作废用户的文件
find path -perm 权限数 显示某路径下权限数为N的文件

find path -amin -minute 最后n分钟访问的文件
find / user username 查找某一用户所属文件
find path -atime -days 最后N天访问的文件
find path -mmin -minute 最后N分钟修改的文件
find path -mtime -days 最后N天修改的文件

## 计划任务

crontab -e 进入编辑模式，设定计划任务
格式：分 时 日月 周  命令

ctrl + x 退出
crontab -l 查看计划任务

## Nessus 漏洞扫描软件

## rpm套餐

rpm -qa 查看安装过的软件包
rpm -qa |grep 安装包名 把相关的包都会列出来
rpm -q 安装包名 查询某个软件包全名
rpm -ql 安装包名 查询安装包在哪里目录下写入文件，不跟后缀
rpm -qlp 安装包名 查看没有安装过的包会写入哪些文件
rpm -af 文件路径 查看文件是哪个包写入的
rpm -evh 软件名 卸载软件

## 安装httpd

yum install httpd 安装httpd 
启动httpd
查看状态
启动

## systemctl套餐

systemctl start 启动
systemctl restart 重启
systemctl stop 停止
systemctl status 查看状态
systemctl enable 开机自动启动

## yum套餐

yum -y install 软件名 下载安装
yum -y localinstall 软件包名 安装软件
yum -y localinstall *.rpm 本地批量安装
yum update 全部更新
yum check-update 检查可更新的包
yum grouplist 列举系统中以组安装的包
yum remove  软件包名 卸载软件
yum groupremove 组名 删除程序组
yum deplist 包名 查看依赖关系
yum clean all 清除全部缓存
yum makecache 更新源
yum list |grep 包名 查看有没有对应的包

## debian套餐

dpkg -i 包名 安装软件
dpkg -L 软件全名 软件安装到什么地方
dpkg -l 软件全名 该安装包的版本
dpkg -r 软件名 删除软件但保留配置文件
dpkg -P 软件名 删除软件并且清空配置文件
dpkg -s 软件全名 查看软件的详细信息
dpkg -c 安装包 查看安装该软件会在哪写入数据（要到哪个安装包的路径下）

## apt-get套餐

apt-get update 更新源
apt-get upgrade 更新系统
apt-get install 包名 安装软件
apt-get remove 包名 删除软件
apt-cache search 某个关键字 搜索需要的软件包含在哪个包里
apt-get clean 清空缓存包

## httpd

/etc/httpd/conf/httpd.conf httpd的主配置文件
/etc/httpd/   配置文件的目录
/var/www/     默认存放网页的目录

DNS解析
搜索栏后缀

## 文本套餐

cat 文件名 |grep 要检索的字 检索关键字
cat 文件名 |grep -v 要去除的字 检索去除了字之后的文本
cat 文件名 |sort 文本排序 数字按照123字母按照abc
cat 文件名 |uniq 文本去重
cat 文件名 wc -l 计算行数
旧的文本>>新的文本 文本重定向
diff 文本1的名字 文本2的名字 比较文本的差异
split -l 要分割成多少的个数 被分割的文本的名字

# kali

kali Linux前身是BackTrack(基于ubuntu)，是一个基于Debian的Linux发行版，包含很多安全和取证的相关工具。支持ARM架构

kali Linux是基于Debian的Linux发行版，设计用于数字取证和渗透测试和黑客攻防。由Offensive Security Ltd维护和资助。最先由Offensive Security的Mati Aharoni和Devon Kearns通过重写BackTrack来完成，BackTrack是他们之前写的用于取证的Linux发行版。
Kali Linux预装了许多渗透测试软件，包括nmap(端口扫描器)、Wireshark(数据包分析器)、John the Ripper(密码破解器)，以及Aircrack-ng(一套用于对无线局域网进行渗透测试的软件)，用户可通过硬盘、Live CD或live USB运行Kali Linux。Metasploit的Metasploit Framework支持Kali Linux，Metasploit一套针对远程主机进行开发和执行Exploit代码的工具

## 敏感目录

robots.txt文件
whois查询
DNS查询

## 端口检测

整站识别
waf探测
工具网站及Google hacker

- nmap
nmap -sF 192.168.1.1 过防火墙扫描
nmap -sL 192.168.1.1 192.168.1.6 伪造自己真实ip改为1.1扫描
nmap -O -PN 192.168.1.1/24 探测网络系统及不用ping探测，可过防火墙拦截

### robots.txt

获取网站隐藏敏感目录活文件 比如：安装目录，上传目录，编辑器目录，管理目录，管理页面等

### whois搜集

搜集注册人信息，电话，邮箱，姓名，地址，等相关有用的敏感信息 常用工具：whois和站长工具

### DNS搜集

搜集网站域名信息，如子域名，其他域名，解析服务器，区域传送漏洞等
常用工具：dnsenum、dig、fierce

- dnsenum可以通过字典或者谷歌猜测可能存在的域名，并对一个网段进行反查

dnsenum --enum cracer.com 获取其他域名
-r 允许用户设置递归查询
-w 允许用户设置whois请求
-o 允许用户指定输入文件位置

- fierce工具主要是对子域名进行扫描和收集信息的。使用fierce工具获取一个目标主机上所有ip地址和主机信息。还可以测试区域传送漏洞

fierce -dns baidu.com 获取其他域名
--wordlist 指定字典
fierce -dns ns9.baidu.com --wordlist host.txt /tmp/12.txt

- dig工具也是一款比较流行的dns侦查工具

dig www.cracer.com 查询dns
dig -t ns cracer.com 找解析域名的授权dns
dig axfr@ns1.dns.net cracer.com

## 目录扫描

### 暴力破解
### 目录爬行
目录爬行原理是通过一些自带网络蜘蛛爬行的工具对网站链接进行快速爬行

暴力破解的方法就是需要一个强大的目录名称字典，用来尝试逐个匹配，如果存在通过响应码的回显来确定目录或者页面是否存在

- dirb工具是一款非常好用的目录暴力破解工具，自带强大字典

dirb http://www.cracer.com
dirb https://www.cracer.com
dirb http://www.cracer.com /usr/wordlist.txt

- FOCA网站元素搜集工具，一款不错的利器，可以在渗透测试中搜集下网站工具中一些敏感文件，用法简单实用

- dirbuster工具是一款非常好用的目录暴力猜解工具，自带强大字典
图形界面
输入httos://www.cracer.com
配置字典

## cms识别

- whatweb 用来识别网站cms及平台环境的工具

whatweb http://www.cracer.com
whatweb -v https://www.cracer.com

# 工具网站

searchdns.netcraft.com netcraft.com
站长工具 http://tool.chinaz.com/
http://www.aizhan.com/ 爱站网
Google hacker 谷歌搜索
...

- waf识别

wafw00f
用来识别网站waf的一款工具
wafw00f http://www.cracer.com

shodan.io  主要搜设备

# 综合扫描

- DMitry(Deepmagic Information Gathering Tool)是一个一体化的信息收集工具。它可以用来收集以下信息：
1.端口扫描
2.whois主机IP和域名信息
3.从Netcraft.com获取主机信息
4.子域名
5.域名中包含的邮件地址
尽管这些信息可以在kali中通过多种工具获取，但是使用DMitry可以将收集的信息保存在一个文件中，方便查看

dmitry -wnpb cracer.com
dmitry -winse cracer.com 扫描网站注册信息
dmitry -p cracer.com -f -b 查看主机开放端口

- REcon-ng
与MSF的使用方法非常类似，插播一下msf使用基础流程
第一步，search name模块
第二步：use name模块
第三步：info 查看模块信息
第四步：show payloads 查看该模块可以使用的攻击载荷(为scanner的时候不需要)
第五步：set payload 载荷
第六步：show targets 查看该攻击载荷使用的系统类型(为scanner的时候不需要)
第七步：set targets num 设置目标的系统类型

启动命令recon-ng

# 服务器漏洞扫描

针对于web服务器的各种漏洞扫描工具的使用展开学习

- webshag

webshag是一个用于对web服务器进行安全审计的跨平台多线程攻击

功能：端口扫描、URL扫描和文件模糊测试
他可以凭借IDS规避能力，使请求之间的相关性变得更复杂

- skipfish

shipfish是一款web应用安全侦查工具。skipfish会利用递归去重和基于字典的探针生成一副交互式网站地图。最终生成的地图绘制通过安全检测后输出

使用方法：
skipfish -o(输出位置) -w/-s (字典文件位置) (目标网站)
扫描结束后查看输出文件即可

- vega

vega是一个安全测试工具，用来爬起一个网站，并分析页面内容来找到链接和表单参数

- w3af

w3af是web application attack and audit framework(web应用攻击和安全审计框架)的缩写
它是一个开源的web应用安全扫描器和漏洞利用工具

两种使用方式：
一种图形界面
二种是命令行

- nikto

nikto是一款开放源代码的、功能强大的web扫描评估软件，能对web服务器多种安全项目进行测试的扫描软件，去寻找已知有名的漏洞，能在230多种服务器上扫描出2600多种有潜在危险的文件、CGI及其他问题，它可以扫描指定主机的web类型、主机名、特定目录、COOKIE、特定CGI漏洞、返回主机允许的http模式等等。他也使用LibWhiske库，但通常比Whisker更新的更为频繁。Nikto是网管安全人员必备的web审计工具之一

-h 指定扫描的目标-p 端口
nikto -h www.xiaojin.org -T 9
nikto -h www.xiaojin.org -p 80,8080,8081
-o 指定输入结果
-C 指定CGI目录 -all表示猜解CGI目录
nikto -h www.xiaojin.org -o result.txt
nikto -h www.xiaojin.org -C all
-T 选项包含很多小选项 -T 9 表示扫描SQL注入漏洞

- wfuzz

是一款用来进行web应用暴力猜解的工具，支持对网站目录、登录信息、应用资源文件等暴力猜解，还可以进行get及post参数的猜解，sql注入、xss漏洞的测试等，该工具所有功能都依赖于字典文件

用法：
猜解www.cracer.com/目录下有哪些页面和目录，通过加载字典文件进行猜解，并且排除404页面，将结果以整齐的格式保存放到0k.html
wfuzz -c -z file,字典文件(pass) --hc 404 -o html
www.cracer.com/FUZZ 2>0k.html

猜解登录表单的密码：
wfuzz -c -z file,字典 -d "login=admin&pwd=FUZZ" --hc 404 http://www.cracer.com/admin/index.php

- websploit

websploit是一个用来扫描和分析远程系统以找到漏洞的开源项目

使用方法：
websploit
show modules
use xxx/xx
show options
set http://123..
run

