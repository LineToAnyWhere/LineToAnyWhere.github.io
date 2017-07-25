# LVM #
> # LVM简介 #

LVM（Logical Volume Manager）主要用于对挂载点空间大小的弹性管理，它是在普通的磁盘分区之上又进行一层抽象，组成一个逻辑磁盘进行弹性管理。  
LVM涉及的主要概念有如下几个：
* **PV(Physical Volume-实体卷轴)**  
  我们实际的 partition 需要调整系统识别码 (system ID) 成为 8e (LVM 的识别码)，然后再经过 pvcreate 的命令将他转成 LVM 最底层的实体卷轴 (PV) ，之后才能够将这些 PV 加以利用！ 调整 system ID 的方是就是通过fdisk。
* **PE(Physical Extend-实体延伸区块)**  
  LVM 默认使用 4MB 的 PE 区块，而 LVM 的 VG 最多仅能含有 65534 个 PE ，因此默认的 LVM VG 会有 4M*65534/(1024M/G)=256G。
* **VG(Volume Group-卷轴群组)**  
  所谓的 LVM 大磁碟就是将许多 PV 整合成 VG 。所以 VG 就是 LVM 组合起来的大磁碟！因为每个 VG 最多仅能包含 65534 个 PE 。 如果使用 LVM 默认的参数，则一个 VG 最大可达 256GB 的容量。
* **LV(Logical Volume-逻辑卷轴)**  
  最终的 VG 还会被切成 LV，这个 LV 就是最后可以被格式化使用的分割槽！为了方便使用者利用 LVM 来管理其系统，因此 LV 的装置档名通常指定为『 /dev/vgname/lvname 』的样式！

> # LVM安装 #

LVM在新版的CentOS中已经默认安装，如果需要安装，则安装如下两个包：  
lvm2-2.02.166-1.el7.x86_64  
lvm2-libs-2.02.166-1.el7.x86_64
> # LVM配置 #

### LVM创建流程 ###
* 创建PV
* 创建VG
* 创建LV
* 创建文件系统

### LVM关闭流程 ###
* 先卸载系统上面的 LVM 文件系统 (包括快照与所有 LV)；
* 使用 lvremove 移除 LV ；
* 使用 vgchange -a n VGname 让 VGname 这个 VG 不具有 Active 的标志；
* 使用 vgremove 移除 VG：
* 使用 pvremove 移除 PV；
* 最后，使用 fdisk 修改 ID 回来啊！

### LVM扩容 ###
* 用 fdisk 配置新的具有 8e system ID 的 partition
* 利用 pvcreate 创建 PV
* 利用 vgextend 将 PV 加入我们的 vg1
* 利用 lvresize 将新加入的 PV 内的 PE 加入 lv1 中
* 透过 resize2fs 将文件系统的容量确实添加！

### LVM缩容 ###

LVM命令图表如下：  

|任务|PV阶段|VG阶段|LV阶段|
|::|::|::|::|
|搜索(scan)|pvscan|vgscan|lvscan|
|创建(create)|pvcreate|vgcreate|lvcreate|
|列出(display)|pvdisplay|vgdisplay|lvdisplay|
|添加(extend)||vgextend|lvextend|
|减少(reduce)||vgreduce|lvreduce|
|删除(remove)|pvremove|vgremove|lvremove|
|改变容量(resize)|||lvresize|
|改变属性(attribute)|pvchange|vgchange|lvchange|


> # LVM使用 #

```
pvcreate /dev/sdb1                            //将sdb1创建为pv
vgcreate -s 4M vg1 /dev/sda1 /dev/sdb1        //将sda1和sdb1创建为vg
vgextend vg1 /dev/sda2                        //将sda2扩容到vg1
lvcreate -l 100 -n lv1 vg1                    //在vg1中创建lv1，分配100个PE；L后可以接容量（M,G,T）
lvresize -l +179 /dev/vg1/lv1                 //为vg1中的lv1增加179个PE
resize2fs /dev/vg1/lv1                        //文件系统重新加载大小
pvmove /dev/sda1 /dev/sdb1                    //将sda1上的数据搬移到sdb1上
lvcreate -l 60 -s -n clpic /dev/vg1/lv1       //创建名为clpic的快照，被快照的内容是/dev/vg1/lv1

```
