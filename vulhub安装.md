ubuntu 16安装

ubuntu安装软件

sudo passwd root
sudo root

更新源
apt-get 
apt-get update 更新软件列表
apt-get install ssh
cd /etc/ssh

apt-get install vim

开启SSH服务
cd /etc/ssh
备份文件
cp sshd_config sshd_config.bak
vim sshd_config
修改PermitRootLogin 为yes
PasswordAuthentication yes

service ssh start/stop/restart/status

查看端口号 netstat -anptl
加入开机自启动
update-rc.d ssh enable
ifconfig 查看ip
poweroff 关机
