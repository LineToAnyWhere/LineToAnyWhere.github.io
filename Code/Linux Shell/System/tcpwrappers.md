# tcp wrappers #
> # tcp wrappers简介 #

tcp wrappers 是linux系统上的防火墙软件，其主要基于进程名来对访问的请求进行控制。主要的配置文件是/etc/hosts.allow,/etc/hosts.deny。受此文件管理的软件必须是由super daemon（xinetd）所管理的服务（即在etc/xinetd.d里面的服务），同时有支持libwrap.so模块的服务（即有libwrap.so.0的服务）。
tcp wrappers的优先级：
* **先以hosts.allow为优先对比，如果符合就放行**
* **再以hosts.deny对比，如果符合就抵挡**
* **若两个档案里都没有匹配项，则放行**

> # tcp wrappers安装 #

tcp wrappers的安装程序是如下两个rpm包：  
tcp_wrappers-libs-7.6-58.el6.x86_64  
tcp_wrappers-7.6-58.el6.x86_64
> # tcp wrappers配置 #

tcp wrappers配置规则有几个重点：
* 它不支持192.168.1.0/24这种形式的子网书写形式，只支持具体的netmask书写方式
* 多个网络之间使用空格分割，如果要写多行，需要在每行带上进程名

> # tcp wrappers使用 #
```
ALL: 127.0.0.1    //这就是本机全部的服务都接受！
rsync: 192.168.1.0/255.255.255.0 10.0.0.100
```
