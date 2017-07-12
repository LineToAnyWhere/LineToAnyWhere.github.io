# 磁盘和文件系统 #
> # 命令描述 #

此处要介绍的相关命令共有18个，分别是**dumpe2fs**、**df**、**du**、**ln**、**fdisk**、**mkfs**、**mke2fs**、**fsck**、**badblocks**、**mount**、**umount**、**mknod**、**e2label**、**tune2fs**、**hdparm**、**free**、**mkswap** 、**swapon**、**parted**
* **dumpe2fs**用于查看superblock信息
* **df**用于列出当前挂载的文件系统信息
* **ln**用于实体链接和符号链接
* **fdisk**用于磁盘分区
* **partprobe**强制内核刷新分区表，直接使用无需参数
* **mkfs**用于磁盘格式化
* **mke2fs**用于详细得进行磁盘格式化
* **fsck**用于磁盘检查
* **badblocks**用于检查磁盘坏道
* **mount**用于挂载文件系统
* **umount**用于卸载文件系统
* **mknod**用于修改设备的编号
* **e2label**用于修改文件系统label
* **tune2fs**用途比较广泛，可直接查看参数来使用其功能
* **hdparm**用于配置IDE接口的一些参数
* **free**用于查看当前内存使用量
* **mkswap**用于用于创建swap格式分区
* **swapon**用于将swap启动
* **parted**用于处理2TB以上的磁盘分区


> # 常用参数 #

* **dumpe2fs**  
  -b ：列出保留为坏道的部分  
  -h ：仅列出 superblock 的数据，不会列出其他的区段内容！
* **df**  
  -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统  
  -k ：以 KBytes 的容量显示各文件系统  
  -m ：以 MBytes 的容量显示各文件系统  
  -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示  
  -H ：以 M=1000K 取代 M=1024K 的进位方式  
  -T ：连同该 partition 的 filesystem 名称 (例如 ext3) 也列出  
  -i ：不用硬盘容量，而以 inode 的数量来显示  
* **du**  
  -a ：列出所有的文件与目录容量，默认仅统计目录底下的文件量而已  
  -h ：以人们较易读的容量格式 (G/M) 显示  
  -s ：列出总量而已，而不列出每个各别的目录占用容量  
  -S ：不包括子目录下的总计，与 -s 有点差别  
  -k ：以 KBytes 列出容量显示  
  -m ：以 MBytes 列出容量显示  
* **ln**  
  -s ：如果不加任何参数就进行连结，那就是hard link(实体连接不能跨文件系统，不能link目录)，至于 -s 就是symbolic link(快捷方式)
  -f ：如果目标文件存在时，就主动的将目标文件直接移除后再创建！
* **fdisk**  
  -l ：输出后面接的磁盘内所有的 partition 内容。若仅有 fdisk -l 时，则系统将会把整个系统内能够搜寻到的装置的 partition 均列出来。
* **mkfs**  
  -t ：可以接文件系统格式，例如 ext3, ext2, vfat 等(系统有支持才会生效)，该命令同样可接mke2fs的详细参数
* **mke2fs**  
  -b ：可以配置每个 block 的大小  
  -i ：多少容量给予一个inode  
  -c ：检查磁盘错误，仅下达一次 -c 时，会进行快速读取测试；如果下达两次 -c -c 的话，会测试读写(read-write)  
  -L ：后面可以接标头名称 (Label)  
  -j ：本来 mke2fs 是 EXT2 ，加上 -j 后，会主动加入 journal 而成为 EXT3
* **fsck**  
  -t ：如同 mkfs 一样，fsck 也是个综合软件而已！因此我们同样需要指定文件系统。不过由于现今的 Linux 太聪明了，他会自动的透过 superblock 去分辨文件系统，因此通常可以不需要这个选项的啰！请看后续的范例说明  
  -A ：依据 /etc/fstab 的内容，将需要的装置扫瞄一次。/etc/fstab 于下一小节说明，通常启动过程中就会运行此一命令了  
  -a ：自动修复检查到的有问题的扇区，所以你不用一直按 y 啰  
  -y ：与 -a 类似，但是某些 filesystem 仅支持 -y 这个参数  
  -C ：可以在检验的过程当中，使用一个直方图来显示目前的进度  
EXT2/EXT3 的额外选项功能：(e2fsck 这支命令所提供)  
  -f ：强制检查！一般来说，如果 fsck 没有发现任何 unclean 的旗标，不会主动进入细部检查的，如果您想要强制 fsck 进入细部检查，就得加上 -f 旗标啰  
  -D ：针对文件系统下的目录进行优化配置  
* **badblocks**  
  -s ：在屏幕上列出进度  
  -v ：可以在屏幕上看到进度  
  -w ：使用写入的方式来测试，建议不要使用此一参数，尤其是待检查的装置已有文件时
* **mount**  
  -a ：依照配置文件 /etc/fstab 的数据将所有未挂载的磁盘都挂载上来  
  -l ：单纯的输入 mount 会显示目前挂载的信息。加上 -l 可增列 Label 名称  
  -t ：与 mkfs 的选项非常类似的，可以加上文件系统种类来指定欲挂载的类型，常见的 Linux 支持类型有ext2, ext3, vfat, reiserfs, iso9660(光盘格式),nfs, cifs, smbfs(此三种为网络文件系统类型)  
  -n ：在默认的情况下，系统会将实际挂载的情况实时写入 /etc/mtab 中，以利其他程序的运行。但在某些情况下(例如单人维护模式)为了避免问题，会刻意不写入。此时就得要使用这个 -n 的选项了  
  -L ：利用文件系统的标头名称(Label)来进行挂载  
  -o ：后面可以接一些挂载时额外加上的参数！比方说账号、密码、读写权限等：  
  ———ro, rw: 挂载文件系统成为只读(ro) 或可擦写(rw)  
  ———async, sync: 此文件系统是否使用同步写入 (sync) 或异步 (async) 的内存机制，请参考文件系统运行方式。默认为 async  
  ———auto, noauto: 允许此 partition 被以 mount -a 自动挂载(auto)  
  ———dev, nodev: 是否允许此 partition 上，可创建装置文件？ dev 为可允许  
  ———suid, nosuid: 是否允许此 partition 含有 suid/sgid 的文件格式  
  ———exec, noexec: 是否允许此 partition 上拥有可运行 binary 文件  
  ———user, nouser: 是否允许此 partition 让任何使用者运行 mount ？一般来说，mount 仅有 root 可以进行，但下达 user 参数，则可让一般 user 也能够对此 partition 进行 mount  
  ———defaults: 默认值为：rw, suid, dev, exec, auto, nouser, and async  
  ———remount: 重新挂载，这在系统出错，或重新升级参数时，很有用  
* **umount**  
  -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下  
  -n ：不升级 /etc/mtab 情况下卸除  
* **mknod**  
  装置种类：  
   b ：配置装置名称成为一个周边储存设备文件，例如硬盘等  
   c ：配置装置名称成为一个周边输入设备文件，例如鼠标/键盘等  
   p ：配置装置名称成为一个 FIFO 文件  
   Major ：主要装置代码  
   Minor ：次要装置代码  
* **e2label**  
  e2label 装置名称 新的Label名称
* **tune2fs**  
  -l ：类似 dumpe2fs -h 的功能～将 superblock 内的数据读出来  
  -j ：将 ext2 的 filesystem 转换为 ext3 的文件系统  
  -L ：类似 e2label 的功能，可以修改 filesystem 的 Label 喔  
* **hdparm**  
  鉴于目前IDE接口设备很少，因此不再介绍此命令
* **free**
  查看当前内存使用状况，直接使用即可
* **mkswap**
* **swapon**
* **parted**

> # 应用示例 #

```
[root@www ~]# dumpe2fs /dev/sda1                          //查看/dev/sda1/磁盘的superblock信息
[root@www ~]# ln -s /etc/crontab crontab2                 //在跟目录创建名为crontab2的符号连接，指向/etc/crontab
[root@www ~]# fdisk -l                                    //列出所有的分区
[root@www ~]# fdisk /dev/sda                              //操作sda磁盘进行分区
[root@www ~]# mkfs -t ext4 /dev/sda1                      //为sda1分区格式化为ext4
[root@www ~]# mke2fs -j -L "C" -b 2048 -i 8192 /dev/sda1  //将sda1分区按指定参数格式化
[root@www ~]# fsck -C -f -t ext3 /dev/sda2                //检查sda2分区
[root@www ~]# mount /dev/sdb1 /mnt/                       //挂载sdb1到/mnt/
[root@www ~]# mount -t iso9660 /dev/cdrom /media/cdrom    //挂载光盘
[root@www ~]# mount -o remount,rw,auto /                  //以读写方式重新挂载
[root@www ~]# mount -L "vbird_logical" /mnt/hdc6          //使用label名进行挂载
[root@www ~]# mount -o loop /root/test.iso /media/        //挂载镜像文件
[root@www ~]# umount /dev/sda1                            //取消挂载sda1
[root@www ~]# mknod /dev/hdc10 b 22 10                    //创建块装置
[root@www ~]# mknod /tmp/testpipe p                       //创建FIFO装置
[root@www ~]# e2label /dev/hdc6 "my_test"                 //将hdc6的label修改为my_test
[root@www ~]# tune2fs -l /dev/sda1                        //列出/dev/sda1的superblock内容
[root@www ~]# free -g                                     //以方便读取的方式查看内存使用情况
[root@www ~]# 
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
[root@www ~]#
```
> # 概念简介 #

## 新增磁盘 ##
新增磁盘总共分以下三个步骤：
* 磁盘分区
* 分区格式化
* 分区挂载

## 分区挂载 ##
分区挂载需要满足如下三点：
* 单一文件系统不应该被重复挂载在不同的挂载点(目录)中
* 单一目录不应该重复挂载多个文件系统
* 要作为挂载点的目录，理论上应该都是空目录
