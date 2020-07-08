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