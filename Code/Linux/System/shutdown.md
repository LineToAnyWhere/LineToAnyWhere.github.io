# 关机相关 #
> # 命令描述 #

* **shutdown**    关机
* **reboot**      重启
* **halt**        关机
* **poweroff**    关机
* **init**        切换运行等级

> # 常用参数 #

* **shutdown**  
  -t sec ： -t 后面加秒数，亦即『过几秒后关机』的意思   
  -k     ： 不要真的关机，只是发送警告信息出去！  
  -r     ： 在将系统的服务停掉之后就重新启动(常用)  
  -h     ： 将系统的服务停掉后，立即关机。 (常用)  
  -n     ： 不经过 init 程序，直接以 shutdown 的功能来关机  
  -f     ： 关机并启动之后，强制略过 fsck 的磁盘检查  
  -F     ： 系统重新启动之后，强制进行 fsck 的磁盘检查  
  -c     ： 取消已经在进行的 shutdown 命令内容。  
* **reboot**  
  -n     ： 不经过sync，直接进行reboot或halt  
  -f     ： 强制reboot或halt，不调用shutdown  
  -p     ： 关机并且调用halt   
* **halt**  
  -n     ： 不经过sync，直接进行reboot或halt  
  -f     ： 强制reboot或halt，不调用shutdown  
  -p     ： 关机并且调用halt   
* **poweroff**  
  -n     ： 不经过sync，直接进行reboot或halt  
  -f     ： 强制reboot或halt，不调用shutdown  
  -p     ： 关机并且调用halt   
* **init**  
  init 0 关机  
  init 3 纯文本模式  
  init 5 含有图形接口模式  
  init 6 重新启动  

> # 应用示例 #

* **shutdown**
```
[root@www ~]# shutdown -h now  
立刻关机，其中 now 相当于时间为 0 的状态  
[root@www ~]# shutdown -h 20:25
系统在今天的 20:25 分会关机，若在21:25才下达此命令，则隔天才关机
[root@www ~]# shutdown -h +10
系统再过十分钟后自动关机
[root@www ~]# shutdown -r now
系统立刻重新启动
[root@www ~]# shutdown -r +30 'The system will reboot'  
再过三十分钟系统会重新启动，并显示后面的信息给所有在在线的使用者
[root@www ~]# shutdown -k now 'This system will reboot'  
仅发出警告信件的参数！系统并不会关机啦！吓唬人！
```
