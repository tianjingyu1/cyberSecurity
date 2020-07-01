# ACL 
1. Access Control List
2.  ACL是一种包过滤技术。
3.  ACL基于IP包头的IP地址、四层TCP/UDP头部的端口号、[5层数据]
           基于三层和四层过滤
4.  ACL在路由器上配置，也可以在防火墙上配置（一般称为策略）防火墙主要过滤三层四层网络流量
5.  ACL主要分为2大类：
    1）标准ACL
    2）扩展ACL
6. 标准ACL：
    表号：1-99
    特点：只能基于源IP对包进行过滤
    命令：
    conf  t
    access-list  表号  permit/deny   源IP或源网段  反子网掩码
    注释：反子网掩码：将正子网掩码0和1倒置
              255.0.0.0  --  0.255.255.255
              255.255.0.0  --  0.0.255.255
              255.255.255.0  --  0.0.0.255
             反子网掩码作用：用来匹配条件，与0对应的需要严格匹配，与1对应的忽略！

    例如： access-list   1   deny   10.0.0.0   0.255.255.255
               解释：该条目用来拒绝所有源IP为10开头的！

                         access-list   1   deny   10.1.1.1  0.0.0.0
               解释：该条目用来拒绝所有源IP为10.1.1.1的主机
               简写： access-list   1   deny   host  10.1.1.1

                access-list   1   deny   0.0.0.0  255.255.255.255
               解释：该条目用来拒绝所有所有人
               简写： access-list   1   deny   any

完整的案例：
conf t
acc 1 deny host 10.1.1.1
acc 1 deny 20.1.1.0 0.0.0.255
acc 1 permit any


查看ACL表：
show  ip  access-list  [表ID]

将ACL应用到接口：
int  f0/x
   ip  access-group  表号  in/out
   exit

sh run

7. 扩展ACL：
    表号：100-199
    特点：可以基于源IP、目标IP、端口号、协议等对包进行过滤
    命令：
acc 100 permit/deny  协议  源IP或源网段  反子网掩码  目标IP或源网段  反子网掩码  [eq 端口号]
注释：协议：tcp/udp/icmp/ip

案例：
acc 100 permit tcp host 10.1.1.1 host 20.1.1.3 eq 80
acc 100 permit icmp host 10.1.1.1 20.1.1.0 0.0.0.255
acc 100 deny ip host 10.1.1.1 20.1.1.0 0.0.0.255
acc 100 permit ip any any

8. ACL原理
1）ACL表必须应用到接口的进或出方向才生效！
2）一个接口的一个方向只能应用一张表！
3）进还是出方向应用？取决于流量控制总方向
4）ACL表是严格自上而下检查每一条，所以要主要书写顺序
5）每一条是由条件和动作组成，当流量完全满足条件当某流量没有满足某条件，则继续检查下一条
6）标准ACL尽量写在靠近目标的地方
7）wencoll小原理：
     1）做流量控制，首先要先判断ACL写的位置（那个路由器？那个接口的哪个方向？）
     2）再考虑怎么写ACL。
     3）如何写？
          首先要判断最终要允许所有还是拒绝所有
          然后写的时候要注意：将严格的控制写在前面
8）一般情况下，标准或扩展acl一旦编写号，无法修改某一条，也无法删除某一条，也无法修改顺序，也无法往中间插入新的条目，只能一直在最后添加新的条目
     如想修改或插入或删除，只能删除整张表，重新写！
     conf t
     no  access-list  表号

9.命名ACL：
  作用：可以对标准或扩展ACL进行自定义命名
  优点：自定义命名更容易辨认，也便于记忆！
            可以任意修改某一条，或删除某一条，也可以往中间插入某一条

命令：
conf t
ip  access-list  standard/extended   自定义表名
      开始从deny或permit编写ACL条目
      exit

删除某一条：
ip  access-list  standard/extended   自定义表名
      no  条目ID
      exit

插入某一条：
ip  access-list  standard/extended   自定义表名
      条目ID   动作   条件
      exit

