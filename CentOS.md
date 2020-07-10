安装CentOS

# 安装界面介绍

1. 安装或者升级一个已存在的操作系统
2. 安装操作系统用基本图形显卡驱动
3. 进入救援模式
4. 从本地磁盘引导进入系统
5. 内存检测

打开终端后显示
[root@hkjhk Desktop]#
[当前登录用户名称@主机名称 当前所在路径]#
#用户身份为超级管理员
$用户身份为普通用户

## 信息查询
先了解当前系统信息
硬盘大小

fdisk -l  //查看当前系统硬盘大小
/dev/sda 操作系统中第一块硬盘的名称以及所在路径
linux系统中一切皆文件（文件名）sd (硬盘类型) a(第一块)
操作系统中硬盘进制使用1000

内存大小

cat /proc/meminfo  //
MemTotal 内存总大小

cpu型号

cat /proc/cpuinfo
model name

关机和重启的命令

reboot 重启
poweroff 关机

## 目录结构与文件属性

linux操作系统树状结构

目录 == 文件夹

cd change directory  ..返回上一级目录
pwd 列出当前所在的目录路径
ls list 列出当前所在目录中的路径
/ --操作系统的起始路径根路径
/bin  --普通用户和管理员都可以执行的命令字
/sbin --只有管理员才能执行的命令 关机重启
/boot --引导 主引导目录 独立的分区 启动菜单 内核
/dev  --device设备 设备文件存放目录
/etc  --配置文件存放目录
/home --普通用户的家目录
/root --管理员的家目录
/media --光驱的挂载目录
/mnt  --临时设备的挂载目录
/proc --里面的数据都在内存中，进程的所在目录
/tmp  --临时文件存放目录
/usr  --软件的安装目录
/var  --常变文件存放目录

## 快捷键与文件分类

安装VMwaretools 实现虚拟机和真实机之间的文件复制

快捷键功能
1. Tab键功能 命令字和以存在的文件名称补齐的作用
2. 清除屏幕内容 ctrl+l
3. 终止快捷键 ctrl+c

linux系统中如何分辨文件类型
蓝色       --目录
黑色       --普通文件
浅蓝色     --符号链接（快捷方式）
黑底黄字   --设备文件 硬盘 sda
绿色       --带有执行权限的文件
红色       --压缩包
紫色       --图片 模块文件

## 增删改查基础命令

查询 查看目录下有哪些内容，查看文件中的内容
     ls命令 cat命令

创建： 创建文件 创建目录
     touch 文件名
     echo "hello!" > 文件
     mkdir 目录名 make directory

改：剪切和复制
     mv 重命名和剪切
     cp 拷贝文件
     符号链接
     ln -s 绝对路径源文件 建立的连接文件

删除
     rm remove 移除
     rm -f 文件 强制删除
     rm -fr 目录 删除目录

## 命令字的帮助信息查询

linux 命令字格式
命令字 【选项】 【文件或者目录】

1. 如何查看一个命令字的帮助手册
man 命令字  

man ls
-a 显示隐藏文件
-l 显示文件的详细信息
-lh 显示文件大小
-R 递归显示目录中的子目录的内容

内部命令 命令解释器自带的命令 
外部命令 安装的第三方软件带的命令字 基本都有帮助手册

help 命令字

## 压缩与解压缩

dd if=/dev/zero of=/tmp/bigfile bs=1M count=100
if inputfile输入文件
of outputfile 输出文件
bs 单位
count 计数器

gzip 文件名称 --压缩文件
gunzip 压缩包 --解压缩

bzip2 文件名称 --压缩
bunzip2 压缩包 --解压缩

du -sh 目录 --查看目录大小

如何对目录进行打包压缩

将目录转化为文件
tar -jcf /tmp/allfile.tar /tmp/allfile
create
tar -jxf /tmp/allfile.tar -C /root
-x 解包 -C 指定解压路径
-z gzip
-j bzip

## vi编辑器 vim升级器

命令模式 ->i->输入模式
输入模式-> Esc->命令模式->:->末行模式
:wq 保存并退出
:q! 不保存
:set nu 显示行号
:% s/old/new/g 每一行中的old替换成new
:50,56 d 删除50-56行的数据

命令模式有非常多的快速编辑快捷键
2yy 复制当前行及下一行
p 粘贴到当前行下
dd 删除当前行
gg 回到第一行
G 到最后一行
50G 快速跳转到第50行

## linux下软件分类

源码包 封装后的软件包

源码包：GNU社区 github
特点：
1. 以压缩包的形式提供给用户
2. 开源

安装的注意事项
以httpd为例
1. 解包
2. 进入解压路径了解软件的作用以及安装方法
  $ ./configure --prefix=PREFIX
  $ make
  $ make install
  $ PREFIX/bin/apachectl start
3. 通过配置脚本指定安装路径和功能，并且生成makefile编译脚本文件
./configure --prefix=/usr/local/webserver
4. 通过make命令控制makefile文件进行顺序编译
5. 将编译好的文件拷贝到安装路径下

编译 可以指定安装的路径和编译所需要的功能

封装后的软件包
安装便捷
特点 后缀 
rpm red hat package manager
deb Debian 
源码包 不考虑系统的版本

centos 安装系统的时候装过
/media 

| 管道符 将前一命令的输出结果作为后一命令的输入

针对tree-1.5.3-3.el6.x86_64.rpm安装的注意事项
1. 有没有装过
rpm -qa 列出所有已装过的rpm软件包
2. 确认该软件的作用
rpm -qpi tree-1.5.3-3.el6.x86_64.rpm
3. 确认该软件的安装路径
rpm -qpl tree-1.5.3-3.el6.x86_64.rpm
4. 安装软件
rpm -ivh tree-1.5.3-3.el6.x86_64.rpm
5. 使用软件
6. 软件卸载
rpm -e tree

卸载vim编辑器工具
1. 该软件的名称
rpm -qa|grep "vim"
2. 卸载(依赖关系)
rpm -e vim-enhanced
rpm -e vim-common
3. 安装
rpm -ivh vim-common-7.4.629-5.el6_8.1.x86_64.rpm
rpm -ivh vim-enhanced-7.4.629-5.el6_8.1.x86_64.rpm

根据光盘中的依赖关系列表进行软件安装卸载（yum源安装）
1. 要告诉操作系统依赖关系列表的位置
vim /etc/yum.repos.d/dvd.repo
[dvdrom] 标签
name="yum dvd rom" 描述
baseurl=file:/media/CentOS_6.9_Final
gpgvheck=0 是否做密钥对
2. 通过yum工具进行软件的卸载与安装

## linux操作系统中的用户分类

普通用户 比管理员低，也可以登录系统
超级管理员

用户的分类和组
/etc/passwd 保存了操作系统中所有用户的信息

root : x : 0 : 0 : root : /root : /bin/bash
xiyangyang : x : 500 : 500 : : /home/xiyangyang : /bin/bash
字段1：用户名
字段2：密码占位符
字段3：用户的uid 0 表示超级用户，500-60000表示普通用户，1-499 程序用户
字段4：基本组的gid，先有组才有用户
字段5：用户信息记录字段
字段6：用户的家目录
字段7：用户登录系统后使用的命令解释器

/etc/shadow 保存了用户密码信息
字段1：用户名
字段2：用户的密码加密后的字符串，sha-512加密混合salt值方式加密
字段3：距离1970/1/1密码最近一次的修改时间
字段4：密码的最短有效期
字段5：密码的最长有效期建议时间90天
字段6：密码过期前7天警告
字段7：密码的不活跃期
字段8：用户的失效时间

/etc/group 记录了系统中所有组信息

## 建立和调整用户属性

groupmod 对组进行修改
groupadd 创建组 -g 指定配置
useradd -g 指定基本组
useradd -G 指定附加组
usermod -u 修改uid
建立什么修改什么什么放最后
useradd -u 250 -M -s /sbin/nologin testuser -M 不要家目录 -s 指定不让登录
passwd 用户 超级管理员给用户设置密码
chage -M 时间 用户 修改密码最长有效期
passwd -l 用户 锁定用户
passwd -u 用户 解锁用户
userdel -r 删除用户连同家目录
groupdel 删除组

## 权限

文件或者目录属于谁，属于哪个组
不同的用户能对该文件进行何种操作

-rw-r--r--,1 root(所属者) root(所属组) test.txt 文件
drwxr-xr-x,2(子文件数) root root testdir/ 目录

-rw- r-- r--
d rwx r-x r-x
字段1： 文件类型 -普通文件 d目录 l符号链接 b块设备
字段2：文件所属者对该文件的权限
         r              w                x
文件   read读取文件   write写入文件   可执行权限
目录   可以查看目录内容  可以增删文件   可以进入目录
字段3：文件所属组的权限
字段4：其他用户的权限（既不是文件的所有者，也不是文件所属组中的用户）

chmod 用户 算数运算符 权限 文件
用户：u(所属者) g(所属组) o(其他用户的权限) a(all)
算术运算符：-+=
权限：rwx

chown 用户 文件
chgrp 组 文件

        rwx
0  000  ---
1  001  --x
2  010  -w-
3  011  -wx
4  100  r--
5  101  r-x
6  110  rw-
7  111  rwx

粘滞位 sgid suid 权限
粘滞位针对目录赋权，目录中创建的文件只有建立者可以删除
chmod o+t 目录

sgid 针对目录建立的权限 在该目录中建立的文件所属组继承父目录的属组
chmod g+s 目录

suid 针对可执行文件建立 谁运行该文件 具有该文件所属者的权限
chmod u+s

撤销 chmod o-t g-s u-s

查询权限 find 路径 -perm 4755（4：suid 2:sgid 1:粘滞位）

1. 不再允许添加新用户的请求
/etc/group
/etc/passwd
/etc/shadow
/home/xxxx
chattr +i

2. rwxr-xr-x 755
目录的最高权限0777-0022=0755
文件666-022=644
027

/etc/profile
/etc/bashrc
umask

/etc/login.defs
设置最长有效期

## 网络地址配置

IP地址 子网掩码 网关 dns

1. 确认系统的网卡信息和ip地址
ip addr
ethernet 0 表示第一个网卡 1表示第二个网卡
lo 本地回环地址
eth0 MAC0
eth1 MAC1

2. 关闭networkmanager服务
service NetworkManager stop 关闭网络管理
chkconfig --level 345 NetworkManager off 在345级别不启用

3. 配置网络地址
ip link set eth0 up
ip addr add 192.168.0.100/24 dev eth0
ip route add default via 192.168.86.1 dev eth0
nslookup 
vim /etc/resolv.conf
nameserver 202.106.0.20  或114.114.114.114

通过配置文件配置网络地址（永久生效）
/etc/sysconfig/network-script
vim ifcfg-eth0
DEVICE=eth0 网卡设备
TYPE=Ethernet 类型
ONBOOT=yes 是否允许network服务管理该文件
BOOTPROTO=static 静态获取
IPADDR=192.168.1.254
NETMASK=255.255.255.0
GATEWAY=xxxxx
DNS1=
DNS2=

service network restart

关闭防火墙 setup

## 日志文件
/var/log
日志分类
  系统日志messages
  登录日志secure
  程序日志

日志的管理服务
/etc/rsyslog.conf

## 日志的异地备份

## web服务

lamp平台
linux apache mysql php
发帖留言 提交 php把发言提交 数据库中
php 登录数据调用所有的留言，将留言生成html语句，显示到主页上

对外服务
ip地址 端口号 80 443
1. 启动服务
service httpd start
2. 验证
ss -antpl|grep 80
3. 主页建立
/var/www/html
index.html
4. 主配置文件分析
share 

## 访问控制设定

1. 仅允许192.168。1.2主机访问主页
Order allow,deny 白名单
  Allow from 192.168.1.网段
Order deny,allow 黑名单
  Deny from 192.168.1.2

2. 对页面进行加密，先输入用户名再输入密码才可以进入
用户名 密码 自己配置
htpasswd -c /etc/httpd/conf/httpuser tom

yum install mysql-server -y 下载安装mysql
下载php

index.php

phpinfo()

## lnmp
n:nginx web 支持庞大的并发访问
linux Nginx MySQL PHP/Perl/Python
继apache之后的另一款linux下被大量使用的web服务软件
Nginx的优势在于，稳定性和低系统资源损耗，并发连接的高处理能力
一台物理服务器可处理30000-50000个并发请求

nginx安装
编译安装之前确保已存在开发环境软件包
-yum -y install pcre-devel zlib-devel
创建运行用户和组
-useradd -M -s /sbin/nologin nginx
编译安装
-tar zxf nginx-1.6.0.tar.gz
-./configure ==prefix=/usr/local/nginx --user=nginx --group=nginx
- make && make install

/usr/local/nginx/conf/nginx.conf 该文件包括三大部分
- 全局配置、I/O事件、HTTP配置
全局配置
- #user nobody;运行用户如果未指定
- worker_processes 1;工作进程数（根据cpu核心数设定）
- #error_log logs/error.log; 错误日志的文件位置
- #pid logs/nginx.pid; pid文件位置
I/O事件配置
- events{
     use epoll; 使用模型类型
     worker_connections 4096; 每个进程处理4096连续
}

## 安装php解析环境
- tar xf php-5.3.28
- yum install -y libxml2-devel libjpeg-devel libpng-devel
- ./configure --prefix=/usr/local/php5 --with-gd --with-zlib --with-config-file-path=/usr/local/php5 --enable-mbstring --enable-fpm --with-jpeg-dir=/usr/lib && make && make install
  
--enable-fpm FastCGI 进程管理器用来对php解析实例进行管理优化解析效率

建立配置文件以及命令路径优化
- yum remove php-cli
- cp php.ini-development /usr/local/php5/php.ini
- vim php.ini
  short_open_tag=On 修改文件内短标记功能为On
- In -s /usr/local/php5/bin/* /usr/bin/
- In -s /usr/local/php5/sbin/* /usr/sbin/

启动php-fpm进程
- cd /usr/local/php5/etc/
- cp php-fpm.conf.default php-fpm.conf 建立启动配置文件
- php-fpm
查看启动状态
- ss -antpl|grep 9000 默认监听端口为9000
停止fpm进程
- killall -s QUIT php-fpm

修改nginx配置文件使其调用php-fpm进程
vim /usr/local/nginx/conf/nginx.conf
server{
     ...
     location ~\.php${
          root /usr/local/nginx/html;  #网页根目录
          fastcgi_pass 127.0.0.1:9000;  #php-fpm的监听地址
          fastcgi_index  index.php;   #php首页文件
          include   fastcgi.conf;  #调用fastcgi配置文件
     }
}

killall 进程  关闭进程

## java web框架
jsp tomcat 
nginx 负载均衡
java -version

安装tomcat
- tar xf apache-tomcat-7.0.54.tar.gz
- mv apache-tomcat-7.0.54 /usr/local/tomcat7

启动tomcat
- /usr/local/tomcat7/bin/startup.sh

验证
- ss -antpl|grep 8080

关闭tomcat
- /usr/local/tomcat7/bin/shutdown.sh

### tomcat目录介绍

cd /usr/local/tomcat7/
- bin   存放启动或关闭tomcat的脚本
- conf  存放tomcat全局配置文件
- lib   存放tomcat需要的库文件
- logs  存放日志文件
- webapps  主页存放目录
  /usr/local/tomcat7/webapps/POOT 默认主页存放目录
- work  jsp编译后产生的class文件

### Nginx+Tomcat负载均衡集群
安装Nginx反向代理两个Tomcat站点实现负载均衡
- ./configure --prefix=/usr/local/nginx --user=nginx --group=nginx --with-file-aio --with-http_stub_status_module --with-http_gzip_static_module --with-http_flv_module --with-http_ssl_module
- user,group 指定用户和组
- with-http_stub_status_module  启用状态统计
- with-http_gzip_static_module  启用gzip静态压缩
- with-http_flv_module  启用flv模块
- with-http_ssl_module  启用SSL模块

配置Nginx
- vim /usr/local/nginx/conf/nginx.conf
- 在http{...}区域中加入
- upstream tomcat_server{
     server 172.16.0.100:8080 weight=1;
     server 172.16.0.200:8080 weight=1;
}
weight为权重值设定为相同来演示实验效果
在location/{...}区域中加入
proxy_pass http://tomcat_server;
启动Nginx验证
注意在两个tomcat上使用不同的主页通过刷新浏览器来观察主页变化

## 包过滤防火墙

iptables 工具
4个功能（表）
raw
mangle
nat  网络地址转换
filter  过滤

iptables -t 表名  查看表
-nvL

每个表都有专门写规则的地方（链）
INPUT  源地址 目标地址 协议tcp 目标端口80
FORWARD 转发规则链（当源地址以及目标地址）
OUTPUT  出站链

### iptables的基本语法

语法构成
- iptables [-t 表名] 选项 [链名][条件][-j 控制类型]

注意事项：
- 不指定表名时，默认指filter表
- 不指定链名时，默认指表内的所有链
- 除非设置链的默认策略，否则必须指定匹配条件
- 选项、链名、控制类型使用大写字母，其余均为小写

数据包的常见控制类型
- ACCEPT：允许通过
- DROP：直接丢弃，不给出任何回应
- REJECT:拒绝通过，必要时会给出提示
- LOG：记录日志信息，然后传给下一条规则继续匹配

iptables的管理选项

添加新的规则
-A： 在链的末尾追加一条规则
-I： 在链的开头（或指定序号）插入一条规则
-L： 列出所有的规则条目
-n:  以数字形式显示地址、端口等信息
-v： 以更详细的方式显示规则信息
--line-number: 查看规则时，显示规则的序号

删除、清空规则
-D： 清空链内指定序号（或内容）的一条规则
-F： 清空所有的规则

设置默认策略
-P: 为指定的链设置默认规则

规则的匹配条件
通用匹配
- 可直接使用，不依赖于其他条件或扩展
- 包括网络协议、IP地址、网络接口等条件
隐含匹配
- 要求以待定的协议匹配作为前提
- 包括端口、TCP标记、ICMP类型等条件
显示匹配
- 要求以“-m扩展模块”的形式明确指出类型
- 包括多端口、MAC地址、IP范围、数据包状态等条件

常见的通用匹配条件
- 协议匹配：-p 协议名
- 地址匹配： -s源地址、-d 目的地址
- 接口匹配： -i入站网卡 -o出战网卡

常见的隐含匹配条件
- 端口匹配： --sport 源端口、--dport目的地址
- TCP标记匹配： --tcp-flags检查范围 被设置的标记
- ICMP类型匹配： --icmp-type ICMP类型

常见的显式匹配条件
- 多端口匹配： -m multiport --sport 源端口列表
-             -m multiport --dport 目的端口列表
- IP范围匹配： -m iprange --src-range IP范围
- MAC地址匹配： -m mac --mac-source MAC地址

导出（备份）规则
iptables-save 工具
可结合重定向输出保存到指定文件

导入
iptables restore < 文件

## nat表 网络地址转换

# 脚本编写

## 规则变量与定义

什么是脚本？作用
.sh
#!/bin/bash
命令行指令

方便使用

变量赋值：
变量$
read -p "please input ipaddr:" IP
给变量IP赋值

### 判断语句

if 条件
then 成立子语句
eg: if [3 -lt 5]
        then echo "yes"
    elif
        then echo "no1"
    else
        echo "no"
    fi
    
缩进无要求