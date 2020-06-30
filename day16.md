# 单臂路由

1.VLAN控制广播域
2.不同的VLAN间无法通信
3.1个VLAN=1个网段

conf t
int f0/0.1
  encapsulation trunk dot1q 10
  ip add 10.1.1.254 255.255.255.0
  no shut
  exit
init f0/0.2
  encapsulation trunk dot1q 20
  ip add 20.1.1.254 255.255.255.0
  no shut
  exit
int f0/0
  no shut

子接口出现后父接口无作用

VLAN之间要靠路由通信

# 单臂路由 （已被淘汰）

单臂路由缺点：
1.网络瓶颈
2.容易发生单点物理故障
  （所有的子接口依赖于总物理接口）
3.VLAN间通信的每一个帧都进行单独路由

# ICMP

1.ICMP没有端口号
2.ICMP协议 网络探测与回馈机制
  1.网络探测
  2.路由跟踪 windows:tracert IP地址 linux或路由：traceroute IP地址
  3.错误反馈

ICMP的封装格式：
  ICMP头 数据
  ICMP头：ICMP类型、代码
  ICMP类型字段：
  8：ping请求
  0：ping应答

  错误回馈
  3：目标主机不可达
  11：TTL超时

# 三层交换机：
1.三层交换机 = 三层路由+二层交换机
2.三层路由引擎是可以关闭或开启的
  conf t
  ip routing   开启三层路由功能
  no ip routing  关闭三层路由功能
3.三层交换机的优点：
  与单臂路由相比：
  1）解决了网络瓶颈问题
  2）解决了单点故障（虚拟接口不再依赖任何的物理接口）
  3）一次路由，永久交换

4.三层交换机上起虚接口（配置VLAN的网关）
  int vlan 10
    ip  add  10.1.1.254  255.255.255.0
    no shut
    exit

5.二层端口升级为三层端口
  int f0/x
    no switchport
    ip add ...
    no shut

在三层路由器上部署DHCP服务器：
conf t
 ip dhcp excluded-address 10.1.1.1 10.1.1.99
 ip dhcp pool v10
   network 10.1.1.0 255.255.255.0
   default-router 10.1.1.254
   dns-server 40.1.1.1

配置DHCP中继：
int f0/0.1 （该接口需要被帮助）
  ip  helper-address   DHCP服务器的IP
  exit

删除配置：
no ip dhcp excluded-address 10.1.1.1 10.1.1.99
no ip dhcp pool v10