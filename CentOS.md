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
