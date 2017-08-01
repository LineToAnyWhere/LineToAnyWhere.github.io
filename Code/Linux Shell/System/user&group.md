# 用户及群组 #
> # 命令描述 #

* **useradd** 用户新增
* **usermod** 用户修改
* **userdel** 用户删除
* **passwd** 密码修改
* **chage** 口令详细参数显示
* **** 重启
* **** 重启
* **** 重启
* **** 重启
* **** 重启
* **** 重启
* **groups** 有效群组
* **newgrp** 有效群组切换（该命令将会启动一个新的以切换群为默认群组的shell）
* **** 切换运行等级

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
* **passwd**  
* **passwd**  
* **passwd**  
* **passwd**  
* **passwd**  


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

###  ###

> # 使用示例 #

```
[root@www ~]# useradd -u 700 -g users jt  //创建UID为700的jt账户，默认群组为users
[root@www ~]# passwd -x 60 -i 10 jt       //jt账户必须每60天修改一次密码，10天不改则口令失效
[root@www ~]# chage -d 0 agetest          //强制用户首次登录后修改密码
```
