# VLAN(Virtual LAN 虚拟局域网)

1.广播/广播域

2.广播的危害：增加网络/终端负担，传播病毒，安全性降低

3.如何控制广播？
 
 控制广播=隔离广播域
 路由器隔离广播（物理隔离广播）
 路由器隔离广播缺点：成本高、不灵活

4.采用新的技术VLAN来控制广播
VLAN技术是在交换机上实现的且是通过逻辑隔离划分的广播域

5.VLAN是干什么的？

控制广播，逻辑隔离广播域

6.一个VLAN=一个广播域=一个网段

7.VLAN的类型：
 1.静态VLAN
  手工配置
  基于端口划分的VLAN

 2.动态VLAN
  手工配置
  基于MAC地址划分的VLAN/采用802.1X端口认证基于账号

8.静态VLAN命令
 1.创建VLAN
conf t
 vlan ID,ID,ID-ID
   [name 自定义名称]
   exit
 2.查看VLAN表：
   show vlan b
 3.将端口加入到VLAN：
   int f0/x
     switchport access vlan ID
     exit
默认VLAN 1 1002-1005 5个