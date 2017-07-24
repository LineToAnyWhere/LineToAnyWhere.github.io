# iptables #
> # iptables简介 #

iptables 主要用于配置Linux上的Netfilter防火墙，Netfilter是一种封包过滤机制的防火墙，主要作用于OSI七层模型的二三四层，他是由内核提供的功能。
> # iptables安装 #

iptables的安装程序是如下两个rpm包：  
iptables-1.4.7-16.el6.x86_64  
iptables-ipv6-1.4.7-16.el6.x86_64
> # iptables关键概念 #

### iptables表格与链 ###
iptables预设了三种表格，分别如下：
* **filter(过滤器)**  
  主要跟进入 Linux 本机的封包有关
  * INPUT:主要与想要进入我们 Linux 本机的封包有关
  * OUTPUT:主要与我们 Linux 本机所要送出的封包有关
  * FORWARD:主要与数据包转发有关
* **nat(地址转换)**  
  主要在进行来源与目的之 IP 或 port 的转换
  * PREROUTING：在进行路由判断之前所要进行的规则(DNAT/REDIRECT)
  * POSTROUTING：在进行路由判断之后所要进行的规则(SNAT/MASQUERADE)
  * OUTPUT：与发送出去的封包有关
* **mangle(破坏者)**  
  主要是与特殊的封包的路由旗标有关

iptables各个表格与链的选系如图：  
![iptables表格与链关系](/Code/Img/Linux/iptables_relation.gif)

### iptables参数说明 ###
* **-t** 后面接 table ，例如 nat 或 filter ，若省略此项目，则使用默认的 filter
* **-L** 列出目前的 table 的规则
* **-n** 不进行 IP 与 HOSTNAME 的反查
* **-v** 列出更多的信息，包括通过该规则的封包总位数、相关的网络接口等
* **-F** 清除所有的已订定的规则
* **-X** 杀掉所有使用者自定义的 chain (应该说的是 tables ）
* **-Z** 将所有的 chain 的计数与流量统计都归零
* **-P** 定义策略( Policy ) 后跟[INPUT,OUTPUT,FORWARD]\[ACCEPT,DROP]
* **iptables [-A/I 链名] [-i/o 网络接口] [-p 协议][-s 来源IP/网域] [--sport 端口范围] [-d 目标IP/网域] [--dport 埠口范围] -j [ACCEPT|DROP|REJECT|LOG]**  
  A为新增一条规则；I为插入一条规则；链名有INPUT,OUTPUT,FORWARD；i为数据包进入的网卡；o为数据包出去的网卡；p的协议有tcp,udp,icmp和all；s为来源IP；sport为来源端口号；d为目标IP；dport为目标端口号；j为动作，有ACCEPT,DROP,REJECT,LOG。
* **iptables -A INPUT [-m state/mac] [--state 状态][--mac-source 物理地址]**  
  -m后可以跟state（状态模块）和mac（网卡物理地址）；--state后可以跟INVALID，ESTABLISHED，NEW，RELATED；--mac-source后可以跟主机物理地址。
* **iptables -A INPUT [-p icmp] [--icmp-type 类型] -j ACCEPT**  
  --icmp-type后可以跟ICMP封包类型。

> # iptables使用 #

```
iptables -A INPUT -i lo -j ACCEPT                               //开放环回接口
iptables -A INPUT -i eth1 -s 192.168.100.0/24 -j ACCEPT         //信任100.0网段所有进来的数据
iptables -A INPUT -i eth1 -s 192.168.100.10 -j ACCEPT           //信任所有来自100.10的数据
iptables -A INPUT -i eth1 -s 192.168.100.230 -j DROP            //所有来自100.230的数据丢弃
iptables -A INPUT -i eth0 -p tcp --dport 21 -j DROP             //连到本机21的请求全部丢弃
iptables -A INPUT -i eth0 -p udp --dport 137:138 -j ACCEPT      //允许通过udp连到本机137，138端口的数据
iptables -A INPUT -i eth0 -p tcp --dport 139 -j ACCEPT          //允许通过tcp连到本机139端口的数据
iptables -A INPUT -i eth0 -p tcp --dport 445 -j ACCEPT          //允许通过tcp连到本机445端口的数据
iptables -A INPUT -i eth0 -p tcp -s 192.168.1.0/24 --sport 1024:65534 --dport ssh -j DROP
//丢弃来自192.168.1.0网段通过tcp1024-65534端口访问ssh的所有数据
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
//只要已建立或相关封包就予以通过
iptables -A INPUT -m state --state INVALID -j DROP
//只要是不合法封包就丢弃
iptables -A INPUT -m mac --mac-source aa:bb:cc:dd:ee:ff -j ACCEPT
//针对局域网络内的 aa:bb:cc:dd:ee:ff 主机开放其联机
```
### 一个基本的客户端iptables配置 ###
```
#!/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin; export PATH

# 1. 清除规则
iptables -F
iptables -X
iptables -Z

# 2. 设定策略
iptables -P   INPUT DROP
iptables -P  OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

# 3~5. 制订各项规则
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -i eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
#iptables -A INPUT -i eth0 -s 192.168.1.0/24 -j ACCEPT

# 6. 写入防火墙规则配置文件
/etc/init.d/iptables save
```
