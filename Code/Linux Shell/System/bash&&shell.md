# LINUX shell #
> ## shell简介 ##  

在linux中，管理整个计算机硬件的其实是操作系统的内核（kernel），内核是需要被保护的，因此我们需要使用shell来跟内核通信。此处我们说的shell为广义的shell，凡是跟操作系统通信的接口都可以称为shell。目前一般的linux系统使用的shell是bash，我们可以使用的shell有很多种，比如Sun默认的C Shell、K SHell、TCSH、Bourne Again SHell(简称bash)。我们可以通过查询`/etc/shells`文件来查询我们当前系统所支持的shell。

> ## shell 变量 ##

在shell变量中的一些细节：
* **单引号一般用于纯文本输出，而双引号一般会将引用的变量输出出来**
* **变量引用的方式有两种$var或者${var}**
* **执行命令的方式有两种``或者$(command)**
* **取消一个变量可以用`unset var`来取消**
* **$RANDOM是shell中的随机数**
* **执行命令时使用`!21`将执行历史记录第21条命令**
* **执行命令时使用`!cp`将执行最近一条以cp开头的命令**

在shell中对变量的一些处理：
```
[root@www ~]# read [-pt] variable                                 //p后跟提示字符，t后跟等待的秒数
[root@www ~]# declare [±aixr] variable                            //a为数组类型，i为整数类型，x与export一样，r是只读类型。+为取消动作，-为执行动作
[root@www ~]# read -p "Please keyin your name: " -t 30 named      //提示使用者 30 秒内输入自己的名字，输入的内容将被赋给named变量
[root@www ~]# declare -i sum=100+300+50                           //声明sum为整数则会运算
[root@www ~]# stty -a                                             //列出当前快捷键内容
[root@www ~]# stty erase ^h                                       //使用ctrl+h 进行删除
```

在shell中对变量的内容的处理：

|变量配置方式|说明|
|:-:|:-:|
|${变量#关键词}|若变量内容从头开始的数据符合『关键词』，则将符合的最短数据删除|
|${变量##关键词}|若变量内容从头开始的数据符合『关键词』，则将符合的最长数据删除|
|${变量%关键词}|若变量内容从尾向前的数据符合『关键词』，则将符合的最短数据删除|
|${变量%%关键词}|若变量内容从尾向前的数据符合『关键词』，则将符合的最长数据删除|
|${变量/旧字符串/新字符串}|若变量内容符合『旧字符串』则『第一个旧字符串会被新字符串取代』|
|${变量//旧字符串/新字符串}|若变量内容符合『旧字符串』则『全部的旧字符串会被新字符串取代』|

|变量配置方式|str没有设置|str为空字符串|str已经设置为非空字符串|
|:-:|:-:|:-:|:-:|
|var=${str-expr}|var=expr|var=|var=$str|
|var=${str:-expr}|var=expr|var=expr|var=$str|
|var=${str+expr}|var=|var=expr|var=expr|
|var=${str:+expr}|var=|var=|var=expr|
|var=${str=expr}|str=expr, var=expr|str 不变, var=|str 不变, var=$str|
|var=${str:=expr}|str=expr, var=expr|str=expr, var=expr|str 不变, var=$str|
|var=${str?expr}|expr 输出至 stderr|var=|var=$str|
|var=${str:?expr}|expr 输出至 stderr|expr 输出至 stderr|var=$str|

> ## linux配置文件 ##

|配置文件|作用|
|:-:|:-:|
|/etc/profile|存放全局的环境变量配置，用户登录后第一个被加载的文件|
|/etc/inputrc|该文件主要存放bash的热键配置，包括tab有无声音之类|
|/etc/profile.d/*.sh|拥有r权限的sh会被加载，主要配置bash颜色，语系，别名等|
|/etc/sysconfig/i18n|只要用于配置bask语系|
|~/.bash_profile|个人环境变量配置文件|
|~/.bash_login|个人环境变量配置文件（在~/.bash_profile不存在时才会读取）|
|~/.profile|个人环境变量配置文件（在~/.bash_login不存在时才会读取）|
|~/.bashrc|个人环境变量配置文件（non-login时也会读取此配置文件）|
|/etc/bashrc|全局环境变量配置文件|

> ## 在线帮助man&info ##  

常见的帮助文件都在**/usr/share/doc**下  
**帮助文档级别**

|标号|含义|
|:--------:|:--------:|
|1|使用者在shell环境中可以操作的命令或可运行文件|
|2|系统核心可调用的函数与工具|
|3|一些常用的function与library，大部分为C的libc|
|4|装置文件的说明，通常在/dev下的文件|
|5|配置文件或者是某些文件的格式|
|6|游戏|
|7|惯例与协议等，例如Linux文件系统、网络协议、ASCII code等的说明|
|8|系统管理员可用的管理命令|
|9|跟kernel有关的文件|

**帮助文档内容**

|标号|含义|
|:--------:|:--------:|
|NAME|简短的命令、数据名称说明|
|SYNOPSIS|简短的命令下达语法(syntax)简介|
|DESCRIPTION|较为完整的说明，这部分最好仔细看看！|
|OPTIONS|针对 SYNOPSIS 部分中，有列举的所有可用的选项说明|
|COMMANDS|当这个程序(软件)在运行的时候，可以在此程序(软件)中下达的命令|
|FILES|这个程序或数据所使用或参考或连结到的某些文件|
|SEE ALSO|可以参考的，跟这个命令或数据有相关的其他说明！|
|EXAMPLE|一些可以参考的范例|
|BUGS|是否有相关的bug！|
