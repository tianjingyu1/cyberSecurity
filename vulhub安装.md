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
修改PermitRootLogin 为yes 28
PasswordAuthentication yes 52

service ssh start/stop/restart/status

查看端口号 netstat -anptl
加入开机自启动
update-rc.d ssh enable
ifconfig 查看ip
poweroff 关机
快照

本地ssh登录 ssh 用户名@Ip

dnsmq 53端口
去除53端口占用
cd /etc/NetworkManager
ls
su root
cp NetworkManager.conf NetworkManager.conf.bak
vim NetworkManager
#dns=dnsmasq
reboot

安装docker
  curl -s https://get.docker.com/ | sh
  vim installDocker.sh
  复制粘贴
  chmod +x installDocker.sh
  ./运行

  测试：
    docker

安装docker-compose//快速启动器
  sudo apt-get install python-pip
  sudo pip install docker-compose
  测试
  docker-compose -v

下载源代码
github vulhub
shell或vmware tools 或虚拟机下载

启动环境
参考vulhub官网
进入漏洞环境目录
tomcat/tomcat8
sudo docker-compose build
sudo docker-compose up -d
Docker加速器