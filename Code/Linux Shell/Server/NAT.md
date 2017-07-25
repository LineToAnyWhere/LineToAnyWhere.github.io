# NAT #
> # NAT简介 #

NAT 的全名是Network Address Translation，字面上的意思是网络地址的转换,主要用于解决IPV4地址资源不足的问题。一般在家庭/企业办公上网时，做IP地址分享使用。
> # NAT安装 #

对于linux的NAT功能，是包含在iptables中的，一般无需额外安装。如果没有iptables，可以下载安装如下两个包：  
iptables-1.4.7-16.el6.x86_64  
iptables-ipv6-1.4.7-16.el6.x86_64
> # NAT配置 #

### SNAT ###
SNAT主要用于将内部IP的请求，转换成公网IP的请求，进而实现内网主机通过共享IP上网。
### DNAT ###
DNAT类似于端口映射，即将连接公网服务器的部分端口映射到内网，当公网的设备访问路由器上的端口时，通过端口转发即可实现访问到内网服务器的资源。
> # NAT使用 #

### SNAT ###
```
//启用Linux的router功能
echo "1" > /proc/sys/net/ipv4/ip_forward
//就是加入 nat table 封包伪装！
iptables -t nat -A POSTROUTING -s 192.168.100.0/24 -o eth0 -j MASQUERADE
//将本地地址转换为192.168.1.100
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.1.100
//将本地地址转换为192.168.1.210-192.168.1.220中的一个地址
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.1.210-192.168.1.220
```
### DNAT ###
```
//将外部访问80的端口，转向内网192.168.100.10的80端口
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to-destination 192.168.100.10:80
//将本地访问80端口的数据转向8080
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8080
```
