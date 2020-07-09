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