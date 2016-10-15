# Cisco 1941系列路由器密码恢复小记 #
> 今天早上来到公司，想要继续调整昨天的网络设备配置脚本，可是连了半天也没连上路由器，一扭头才发现路由器上接口处的灯全部都没亮，再一看，我的天，谁昨天把电源给我拔了，虽说是测试设备，也不能说拔就拔啊！！！因为只有我一个人在测网络设备，所以做了一些基本的配置并没有执行write命令保存，只是让其在running-config下运行，毕竟测试结束后要拿到公司总部去用，省的再重置了。。无奈，只好接上电源，启动之，console登陆，wait，登陆不了0.0，经过无数次重试（后发现是因为手动删除了设备默认账号，而新建账号又没有执行write，导致系统内没有账号可以登录），万般无奈之下，想起了那一年课本第一章的Cisco设备密码恢复，那就抄家伙干吧，但是在这之前————  
（╯' - ')╯︵ ┻━┻ （掀桌子）  
┬─┬ ノ( ' - 'ノ) （摆好摆好）  
(╯°Д°)╯︵ ┻━┻（再他妈的掀一次)）  
**着急的朋友请跳过前面的鬼畜，直接看后面正文，重点已加粗**  
**分割线--------------------------------------------------------**

## 恢复密码过程 ##
1. **连好Console线，由于我使用的笔记本，所以是一根USB转RS232，接一根RS232转RJ45，再接路由器console口。**（刚买回设备的时候发现有两个console口，跟自己印象中的不一样啊，查了半天最后厚着脸皮问了现在在做机房运维的同学，告诉我说现在新的网络设备console口都是两个，一个RJ45，一个Mini Usb console。瞬间感觉四年大学白上了。。。）

2. **配置好终端协议类型及参数，我使用的是Xshell，配置如下图**  
![Xshell配置](/Code/Img/NetWork/Cisco/Xshell_config1.jpg)  
![Xshell配置](/Code/Img/NetWork/Cisco/Xshell_config2.jpg)  

3. **开启路由器，使用Xshell连接，在路由器启动的过程中按下Fn+b键，发送break信号。（笔记本中没有break键，需要Fn+b键组合来模拟，正常情况下需要使用Ctrl+break键来发送中断信号，而对于Xshell来说使用Break键就会发送中断信号，因此，如果使用Xshell的同学，请按break或者Fn+b来发送中断信号，使用其他终端的同学使用Ctrl+Break或者Ctrl+Fn+b来发送中断信号）进入ROMMON模式如下:**  
![Xshell配置](/Code/Img/NetWork/Cisco/ROMMON_MODE.jpg)

4. **修改寄存器值为0x2142，这样会使引导过程中跳过密码验证。执行命令，并重启路由器，分别执行**
```
  rommon 1 > confreg 0x2142
  rommon 2 > reset
```
**重启过后会询问是否进行初始化配置，一律“no”就好了。过程图如下：**  
![Xshell配置](/Code/Img/NetWork/Cisco/ROMMON_MODE.gif)

5. **进入特权模式，为了不破坏以前的配置，我们先将启动配置加载到运行时配置中**
```
  Route#copy startup-config running-config
```
**然后进入配置模式进行密码的修改**
```
  Route#configure terminal
  Route(config)#enable password yourpasswd
```
**修改完成后将寄存器值归位**
```
  Route(config)#config-register 0x2102
```
**最后保存设置并重启路由器就完成密码的恢复了**
```
  Route(config)#end
  Route#copy running-config startup-config
  Route#reload
```
**所有配置执行的过程如下：**  
![Xshell配置](/Code/Img/NetWork/Cisco/Recovery_passwd.gif)

## 后记 ##
> 至此所有的恢复工作就都完成了，Cisco的路由器密码恢复大部分都适用此方法，当然也有部分设备所修改的寄存器地址不同，Cisco交换机的密码恢复方式与此稍有不同，之后我会另述，当然还会有华为交换机的密码恢复（其实是因为手头就这几个设备，当然网上有很多类似教程，写的也都简单易懂，大家可以择优参考。本文如有不妥之处，欢迎指正）。
