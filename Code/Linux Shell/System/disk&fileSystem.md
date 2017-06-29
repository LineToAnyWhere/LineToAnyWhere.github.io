# 磁盘和文件系统 #
> # 命令描述 #

此处要介绍的相关命令共有18个，分别是**dumpe2fs**、**df**、**du**、**ln**、**fdisk**、**mkfs**、**mke2fs**、**fsck**、**badblocks**、**mount**、**umount**、**mknod**、**e2label**、**tune2fs**、**hdparm**、**free**、**mkswap** 、**swapon**、**parted**
* **dumpe2fs**用于查看superblock信息
* **df**用于列出当前挂载的文件系统信息
* **ln**用于实体链接和符号链接
* **fdisk**用于磁盘分区
* **mkfs**用于磁盘格式化
* **mke2fs**用于详细得进行磁盘格式化
* **fsck**用于磁盘检查
* **badblocks**用于检查磁盘坏道
* **mount**用于挂载文件系统
* **umount**用于卸载文件系统
* **mknod**用于
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
  -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已  
  -h ：以人们较易读的容量格式 (G/M) 显示  
  -s ：列出总量而已，而不列出每个各别的目录占用容量  
  -S ：不包括子目录下的总计，与 -s 有点差别  
  -k ：以 KBytes 列出容量显示  
  -m ：以 MBytes 列出容量显示  
* **ln**  
  
* **fdisk**
* **mkfs**
* **mke2fs**
* **fsck**
* **badblocks**
* **mount**
* **umount**
* **mknod**
* **e2label**
* **tune2fs**
* **hdparm**
* **free**
* **mkswap**
* **swapon**
* **parted**

> # 应用示例 #

```
[root@www ~]# dumpe2fs /dev/sda1                          //查看/dev/sda1/磁盘的superblock信息

```
> # 概念简介 #
