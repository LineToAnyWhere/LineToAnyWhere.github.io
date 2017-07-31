# Quota #
> # Quota简介 #

Quota用于做操作系统上的磁盘配额，以此来限制用户对磁盘空间的使用，使得每个用户可以按照预设的空间进行使用，防止资源不合理占用。
### Quota的使用限制 ###
* **仅能针对整个 filesystem**
* **内核必须支持 quota**
* **Quota 的记录档 aquota.user, aquota.group**
* **只对一般身份使用者有效**

> # Quota安装 #

Quota的安装程序是如下两个rpm包：  
quota.x86_64  
quota-nls.noarch
> # Quota命令 #  

* **quotacheck** 扫瞄文件系统并创建 Quota 的记录档，该命令不适用于xfs的文件系统  
  -a :扫瞄所有在 /etc/mtab 内，含有 quota 的 filesystem  
  -u :针对使用者扫瞄文件与目录的使用情况，会创建 aquota.user  
  -g :针对群组扫瞄文件与目录的使用情况，会创建 aquota.group  
  -v :显示扫瞄过程的资讯  
  -f :强制扫瞄文件系统，并写入新的 quota 配置档 (危险)  
  -M :强制以读写的方式扫瞄文件系统，只有在特殊情况下才会使用
* **quotaon** 启动quota服务  
  -a :根据 /etc/mtab 内的 filesystem 配置启动有关的 quota  
  -v :显示启动过程的相关信息  
  -u :针对使用者启动 quota (aquota.user)  
  -g :针对群组启动 quota (aquota.group)
* **quotaoff** 停止quota服务  
  -a :根据 /etc/mtab关闭全部的 quota  
  -u :仅针对后面接的那个 /mount_point 关闭 user quota  
  -g :仅针对后面接的那个 /mount_point 关闭 group quota
* **edquota** 编辑帐号/群组的限值与宽限时间  
  -u :后面接帐号名称。可以进入 quota 的编辑画面 (vi) 去配置 username 的限制值  
  -g :后面接群组名称。可以进入 quota 的编辑画面 (vi) 去配置 groupname 的限制值  
  -t :可以修改宽限时间  
  -p :从旧账户复制配置好的策略给新用户
* **quota** 单一用户的quota报表  
  -u :后面可以接 username ，表示显示出该使用者的 quota 限制值  
  -g :后面可接 groupname ，表示显示出该群组的 quota 限制值  
  -v :显示每个用户在 filesystem 的 quota 值  
  -s :使用 1024 为倍数来指定单位，会显示如 M 之类的单位
* **repquota** 针对文件系统的限额做报表  
  -a :直接到 /etc/mtab 搜索具有 quota 标志的 filesystem ，并报告 quota 的结果  
  -v :输出的数据将含有 filesystem 相关的详细信息  
  -u :显示出使用者的 quota 限值 (这是默认值)  
  -g :显示出个别群组的 quota 限值  
  -s :使用 M, G 为单位显示结果  
* **warnquota** 对超过限额者发出警告信（/etc/warnquota.conf）  
* **setquota** 直接使用命令配置quota  
  setquota [-u|-g] 名称 block(soft) block(hard) inode(soft) inode(hard) 文件系统

> # Quota使用 #

```
quotacheck -avug                                  //扫描整个文件系统
quotaon -auvg                                     //启动user/group的quota
quotaoff -a                                       //关系所有quota
edquota -u myquota1                               //编辑myquota1用户的quota
edquota -p myquota1 -u myquota2                   //复制myquota1的配置给myquota2
quota -gvs myquotagrp                             //显示myquotagrp群组的quota
repquota -auvs                                    //显示所有使用者的quota
setquota -u myquota5 100000 200000 0 0 /home      //设置myquota5的配额为10W,20W
```
