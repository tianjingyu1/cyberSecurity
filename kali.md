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

