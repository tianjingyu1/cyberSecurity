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

接入层 核心

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