# 单臂路由

1.VLAN控制广播域
2.不同的VLAN间无法通信
3.1个VLAN=1个网段

conf t
int f0/0.1
  ip add 10.1.1.254 255.255.255.0
  no shut
  exit
init f0/0.2
  ip add 20.1.1.254 255.255.255.0
  no shut
  exit
int f0/0
  no shut

子接口出现后父接口无作用