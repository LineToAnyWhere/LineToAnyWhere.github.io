# 用户及群组 #
> # 命令描述 #

* **useradd** 用户新增
* **usermod** 用户修改
* **userdel** 用户删除
* **passwd** 密码修改
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
  -u:后面接UID，指定特定UID给这个帐号  
  -g:后面接组名，也就是该账户的初始群组  
  -G:后面接组名，标识该用户还要加入的其他群组  
  -M:强制不创建家目录（系统帐号默认值）  
  -m:强制创建家目录（一般帐号默认值）  
  -c:配置该账户的说明信息  
  -d:指定某个目录成为家目录（必须为绝对目录）  
  -r:创建一个系统帐号（UID会小于500）  
  -s:指定该账户使用的shell，默认为/bin/bash  
  -e:后面接日期，格式为YYYY-MM-DD，致命帐号失效日期  
  -f:后接口令失效日期，0为立即失效，-1为永不失效
  -D:显示useradd默认配置（/etc/default/useradd和/etc/login.defs另外新建用户时家目录的默认数据是从/etc/skel全部拷贝过去的）
* ****  


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
