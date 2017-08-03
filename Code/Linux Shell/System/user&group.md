# 用户及群组 #
> # 命令描述 #

* **useradd** 用户新增
* **usermod** 用户修改
* **userdel** 用户删除
* **passwd** 密码修改
* **chage** 口令详细参数显示
* **finger** 查看用户信息
* **chfn** change finger
* **chsh** change shell
* **id** 查询UID/GID等信息
* **groupadd** 新增群组
* **groupmod** 修改群组
* **groupdel** 删除群组
* **gpasswd** 群组管理
* **groups** 有效群组
* **newgrp** 有效群组切换（该命令将会启动一个新的以切换群为默认群组的shell）
* **su** 切换用户
* **sudo** 以root权限运行程序
* **visudo** 编辑/etc/sudoers

> # 常用参数 #

* **useradd**  
  -u: 后面接UID，指定特定UID给这个帐号  
  -g: 后面接组名，也就是该账户的初始群组  
  -G: 后面接组名，标识该用户还要加入的其他群组  
  -M: 强制不创建家目录（系统帐号默认值）  
  -m: 强制创建家目录（一般帐号默认值）  
  -c: 配置该账户的说明信息  
  -d: 指定某个目录成为家目录（必须为绝对目录）  
  -r: 创建一个系统帐号（UID会小于500）  
  -s: 指定该账户使用的shell，默认为/bin/bash  
  -e: 后面接日期，格式为YYYY-MM-DD，致命帐号失效日期  
  -f: 后接口令失效日期，0为立即失效，-1为永不失效  
  -D: 显示useradd默认配置（/etc/default/useradd和/etc/login.defs另外新建用户时家目录的默认数据是从/etc/skel全部拷贝过去的）
* **usermod**  
  -c: 后面接账号的说明，即 /etc/passwd 第五栏的说明栏，可以加入一些账号的说明  
  -d: 后面接账号的家目录，即修改 /etc/passwd 的第六栏  
  -e: 后面接日期，格式是 YYYY-MM-DD 也就是在 /etc/shadow 内的第八个字段数据  
  -f: 后面接天数，为 shadow 的第七字段  
  -g: 后面接初始群组，修改 /etc/passwd 的第四个字段，亦即是 GID 的字段  
  -G: 后面接次要群组，修改这个使用者能够支持的群组，修改的是 /etc/group  
  -a: 与 -G 合用，可添加次要群组的支持而非配置  
  -l: 后面接账号名称。亦即是修改账号名称，/etc/passwd 的第一栏  
  -s: 后面接 Shell 的实际文件，例如 /bin/bash 或 /bin/csh 等等  
  -u: 后面接 UID 数字，即 /etc/passwd 第三栏的数据  
  -L: 暂时将用户的口令冻结，让他无法登陆。其实仅改 /etc/shadow 的口令栏  
  -U: 将 /etc/shadow 口令栏的 ! 拿掉，解锁账户  
* **userdel**  
  -r: 连同用户家目录一起删除  
* **passwd**  
  --stdin: 可以通过来自前一个管道的数据作为口令输入  
  -l: Lock的意思，会将/etc/shadow第二栏加上！号，使口令失效  
  -u: unlock的意思  
  -S: 列出shadow内的信息  
  -n: 后面接天数，多久不可以修改口令  
  -x: 后面接天数，多久内必须修改口令  
  -w: 后面接天数，口令过期前的警告天数  
  -i: 后面接日期，口令失效日期
* **chage**  
  -l: 列出该账号的详细口令参数  
  -d: 后面接日期，修改 shadow 第三字段,格式 YYYY-MM-DD  
  -E: 后面接日期，修改 shadow 第八字段，格式 YYYY-MM-DD  
  -I: 后面接天数，修改 shadow 第七字段  
  -m: 后面接天数，修改 shadow 第四字段  
  -M: 后面接天数，修改 shadow 第五字段  
  -W: 后面接天数，修改 shadow 第六字段  
* **finger**  
  -s: 仅列出用户的账号、全名、终端机代号与登陆时间等等  
  -m: 列出与后面接的账号相同者，而不是利用部分比对
* **chfn**  
  -f: 后面接完整的名字  
  -o: 办公室的房间号  
  -p: 办公室的电话号  
  -h: 家里的电话号
* **chsh**  
  -l: 列出目前系统上面可用的 shell ，其实就是 /etc/shells 的内容  
  -s: 修改要配置的shell
* **groupadd**  
  -g: 后面接特定GID  
  -r: 创建系统群组
* **groupmod**  
  -g: 修改现有GID  
  -n: 修改现有群组名字
* **gpasswd**  
    : 没有参数则表明给groupname一个口令  
  -A: 将群组的管理权交给其他用户  
  -M: 将帐号加入该群组  
  -r: 将groupname的口令移除  
  -R: 让groupname的口令栏失效  
  -a: 将某个使用者加入到这个群组  
  -d: 将某个使用者移出这个群组
* **su**  
   -: 单纯使用 - 代表使用login-shell的变量文件读取方式来登陆系统,不使用则是切换到root用户
  -l: 与 - 类似，但后面需要加欲切换的使用者账号！也是 login-shell 的方式
  -m: 与 -p 一样，表示使用目前环境配置，而不读取新使用者的配置文件
  -c: 仅进行一次命令
* **sudo**
  -b: 将后序命令放到后台运行  
  -u: 后面接预切换的用户，若无此选项则代表root


> # 概念简介 #

### /etc/passwd数据结构 ###
`root:x:0:0:root:/root:/bin/bash`  
`账户名:口令:UID:GID:用户信息:家目录:SHELL`
### /etc/shadow数据结构 ###
`root:$6$HI6I1Hu2$z12cxg8//PkjVPhtUbiG.cQ3nY1OAJ1eSeJ2dcd./9WmxTgYCHE1.5DSONfFLv0umobqe/x7IQUvquM0FmRQS.:17163:0:99999:7:::`  
`账户名:口令:最近修改口令时间:口令不可被改动的天数:口令需要变更的天数:口令需要更改前的警告天数:口令过期后的失效时间:帐号失效日期:保留`
### /etc/group数据结构 ###
`bin:x:1:root,bin,daemon`  
`组名:群组口令:GID:在此群组中的账户`
### /etc/gshadow数据结构 ###
`daemon:::root,bin,daemon`
`组名:口令栏（如果为!则表示无群组管理员）:群组管理员帐号:群组的用户`
### /etc/sudoers配置规范 ###
```
#定义用户别名
User_Alias ADMPW = user1,user2,user3,jt
#定义命令别名
Cmnd_Alias ADMPWCOM = !/usr/bin/passwd,!/usr/bin/passwd root,/usr/bin/passwd [A-Za-z]*
#用户     登录来源=(可切换身份)      可执行命令
root          ALL=(ALL)               ALL
jt            ALL=(root)           /usr/bin/passwd
ADMPWCOM      ALL=(root)            ADMPWCOM
#禁止用户切换/提升至root账户，禁止修改root密码
jt            ALL=(root)            NOPASSWD:ALL,!/usr/bin/su,!/usr/bin/su -,!/usr/bin/passwd,!/usr/bin/passwd root
#组       登录来源=(可切换身份)      可执行命令
%jiutian      ALL=(root)            NOPASSWD:ALL
```
> # 使用示例 #

```
[root@www ~]# useradd -u 700 -g users jt                //创建UID为700的jt账户，默认群组为users
[root@www ~]# passwd -x 60 -i 10 jt                     //jt账户必须每60天修改一次密码，10天不改则口令失效
[root@www ~]# chage -d 0 agetest                        //强制用户首次登录后修改密码
[root@www ~]# usermod -e "2009-12-31" jt                //修改jt用户失效日期
[root@www ~]$ finger                                    //列出目前在系统上登录的用户与时间
[root@www ~]$ finger root                               //列出root账户的信息
[root@www ~]# chfn -f sfh                               //修改当前用户finger信息
[root@www ~]# groupadd [-g gid] [-r] 组名
[root@www ~]# groupmod [-g gid] [-n group_name] 群组名
[root@www ~]# groupdel [groupname]
[root@www ~]# gpasswd groupname
[root@www ~]# su - -c "head -n 3 /etc/shadow"            //以root权限执行一次命令
```
