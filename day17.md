# 三层交换技术

conf t
ip routing 开启三层路由功能
int vlan 10
  ip add 10.1.1.254
  no shut
int vlan 20
  ip add 20.1.1.254
  no shut

主板带宽

## 三层交换机：
1.三层交换机 = 三层路由+二层交换机
2.三层路由引擎是可以关闭或开启的
 conf t
 ip routing  开启三层路由功能
 no ip routing 关闭三层路由功能
3.三层交换机的优点：
 与单臂路由相比：
 1）解决了网络瓶颈问题
 2）解决了单点故障（虚拟接口不再依赖任何的物理接口）
 3）一次路由，永久交换

 CEF表 快速转发表
 邻接关系表

4.三层交换机上起虚接口（配置VLAN的网关）
int vlan 10
  ip add 10.1.1.254 255.255.255.0
  no shut
  exit

内部网络规划  接入层 汇聚层（一般会被忽略，大型内网会有） 核心层

5.二层端口升级为三层端口
  int f0/x
    no switchport
    ip add ...
    exit

VTP(vlan trunking protocol) vlan中继协议，虚拟局域网干道协议

## 三层交换机内外网实验步骤:

一、交换部分
1) Trunk
2) VTP
3) 创建vlan
4) 分配端口到vlan
5) 起三层虚接口

二、路由部分
1) 配置IP,并开启
2) 配置路由

# HSRP协议（思科私有）/VRRP协议

热备份路由协议
1.HSRP组号：1-255  没有大小之分
2.虚拟路由器得IP称为 虚拟IP地址
3.HSRP组得成员
  1）虚拟路由器（老大）
  2）活跃路由器
  3）备份路由器
  4）其他路由器
4.HSRP优先级 1-255
  默认为100
5.HSRP组成员通过定时发送hello包来交流，默认每隔3秒
  hello时间3秒，坚持时间10秒
6.占先权preempt
  作用：当检测不到对方或检测到对方优先级比自己低，立即抢占活跃路由的名分
7.配置跟踪track,跟踪外网端口状态，当外网down掉，则自降优先级

R1
int f0/0
  standby 1 ip 192.168.1.254
  standby 1 priority 200
  standby 1 preempt
  standby 1 track f0/1
  exit
R2
  standby 1 ip 192.168.1.254
  standby 1 priority 195
  standby 1 preempt
  standby 1 track f0/1
  exit

查看hsrp状态
show standby br
show standby

win+shift+s 截图