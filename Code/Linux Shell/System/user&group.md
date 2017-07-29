# 用户及群组 #
> # 命令描述 #

* **** 关机
* **** 重启
* **** 关机
* **** 关机
* **** 切换运行等级

> # 常用参数 #


> # 概念简介 #

### /etc/passwd数据结构 ###
`root:x:0:0:root:/root:/bin/bash`  
`账户名:口令:UID:GID:用户信息:家目录:SHELL`
### /etc/shadow数据结构 ###
`root:$6$HI6I1Hu2$z12cxg8//PkjVPhtUbiG.cQ3nY1OAJ1eSeJ2dcd./9WmxTgYCHE1.5DSONfFLv0umobqe/x7IQUvquM0FmRQS.:17163:0:99999:7:::`  
`账户名:口令:最近修改口令时间:口令不可被改动的天数:口令需要变更的天数:口令需要更改前的警告天数:口令过期后的失效时间:帐号失效日期:保留`
