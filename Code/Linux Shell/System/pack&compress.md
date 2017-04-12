# 文件打包&压缩 #
> # 命令描述 #

此处介绍的命令共13个
关于文件压缩的命令有6个，分别是**compress**、**uncompress**、**gzip**、**zcat**、**bzip2**、**bzcat**  
* **compress**用于文件、目录压缩（已经淘汰）  
* **uncompress**用于解压compress压缩的文件、目录  
* **gzip**用于文件、目录压缩、解压(可以解开经由compress、zip、gzip压缩的数据)  
* **zcat**用于查看使用gzip压缩的文件、目录  
* **bzip2**用于文件、目录压缩  
* **bzcat**用于查看使用bzip2压缩的文件、目录

关于文件、目录打包的命令有1个，**tar**  
* **tar**用于文件打包、拆包（上述的压缩程序都仅仅是压缩文件，并不能打包文件、目录）  

关于文件系统备份恢复的命令有4个，分别是**dump**、**restore**、**dd**、**cpio**  
* **dump**用于备份文件系统  
* **restore**用于还原使用dump备份出来的数据
* **dd**可以用来备份文件系统，也可以用来制作空文件
* **cpio**可以用来备份任何文件，包括设备文件（cpio使用是需要配合find等命令找到要备份的数据）

关于光盘映像档创建、光盘烧制的命令有2个，分别是**mkisofs**、**cdrecord**  
* **mkisofs**用于制作ISO映像文件  
* **cdrecord**用于烧制光盘

> # 常用参数 #

* **compress**  
  -r ：可以连同目录下的文件也同时给予压缩呢  
  -c ：将压缩数据输出成为 standard output (输出到萤幕)  
  -v ：可以秀出压缩后的文件资讯以及压缩过程中的一些档名变化  
* **uncompress**  
* **gzip**  
  -c ：将压缩的数据输出到萤幕上，可透过数据流重导向来处理  
  -d ：解压缩的参数  
  -t ：可以用来检验一个压缩档的一致性～看看文件有无错误  
  -v ：可以显示出原文件/压缩文件的压缩比等资讯  
  -# ：压缩等级，-1 最快，但是压缩比最差、-9 最慢，但是压缩比最好！默认是 -6
* **zcat**  
* **bzip2**  
  -c ：将压缩的过程产生的数据输出到萤幕上  
  -d ：解压缩的参数
  -k ：保留原始文件，而不会删除原始的文件喔  
  -z ：压缩的参数
  -v ：可以显示出原文件/压缩文件的压缩比等资讯  
  -# ：与 gzip 同样的，都是在计算压缩比的参数， -9 最佳， -1 最快  
* **bzcat**  
* **tar**  
  -c ：创建打包文件，可搭配 -v 来察看过程中被打包的档名(filename)  
  -t ：察看打包文件的内容含有哪些文件  
  -x ：解打包或解压缩的功能，可以搭配 -C (大写) 在特定目录解开，特别留意的是， -c, -t, -x 不可同时出现在一串命令列中  
  -j ：透过 bzip2 的支持进行压缩/解压缩：此时档名最好为 \*.tar.bz2  
  -z ：透过 gzip  的支持进行压缩/解压缩：此时档名最好为 \*.tar.gz  
  -v ：在压缩/解压缩的过程中，将正在处理的档名显示出来  
  -f filename ：-f 后面要立刻接要被处理的档名！建议 -f 单独写一个选项罗  
  -C 目录 ：这个选项用在解压缩，若要在特定目录解压缩，可以使用这个选项  
  -p(小写) ：保留备份数据的原本权限与属性，常用於备份(-c)重要的配置档  
  -P(大写) ：保留绝对路径，亦即允许备份数据中含有根目录存在之意  
  --exclude=FILE ：在压缩的过程中，不要将 FILE 打包  
  --newer-mtime=DATE : 在压缩的过程中，仅压缩DATE时间之后的数据
* **dump**  
  -S ：仅列出后面的待备份数据需要多少磁碟空间才能够备份完毕  
  -u ：将这次 dump 的时间记录到 /etc/dumpdates 文件中  
  -v ：将 dump 的文件过程显示出来  
  -j ：加入 bzip2 的支持！将数据进行压缩，默认 bzip2 压缩等级为 2  
  -level ：就是我们谈到的等级，从 -0 ~ -9 共十个等级  
  -f ：有点类似 tar 啦！后面接产生的文件，亦可接例如 /dev/st0 装置档名等  
  -W ：列出在 /etc/fstab 里面的具有 dump 配置的 partition 是否有备份过  
* **restore**  
  -t ：此模式用在察看 dump 起来的备份档中含有什么重要数据！类似 tar -t 功能  
  -C ：此模式可以将 dump 内的数据拿出来跟实际的文件系统做比较，最终会列出『在 dump 文件内有记录的，且目前文件系统不一样』的文件  
  -i ：进入互动模式，可以仅还原部分文件，用在 dump 目录时的还原  
  -r ：将整个 filesystem 还原的一种模式，用在还原针对文件系统的 dump 备份  
  -h ：察看完整备份数据中的 inode 与文件系统 label 等资讯  
  -f ：后面就接你要处理的那个 dump 文件罗  
  -D ：与 -C 进行搭配，可以查出后面接的挂载点与 dump 内有不同的文件  
* **dd**  
* **cpio**  
* **mkisofs**  
  -o ：后面接想要产生的映像档档名  
  -r ：透过 Rock Ridge 产生支持 Unix/Linux 的文件数据，可记录较多的资讯  
  -v ：显示建置 ISO 文件的过程  
  -m file ：-m 为排除文件 (exclude) 的意思，后面的文件不备份到映像档中  
  -V vol ：创建 Volume，有点像 Windows 在文件总管内看到的 CD title 的东西  
  -graft-point ：graft有转嫁或移植的意思，相关数据在底下文章内说明  
* **cdrecord**  
  -scanbus ：用在扫瞄磁碟汇流排并找出可用的烧录机，后续的装置为 ATA 介面  
  -v ：在 cdrecord 运行的过程中，显示过程而已  
dev=ATA:x,y,z   ：后续的 x, y, z 为你系统上烧录机所在的位置，非常重要！
blank=[fast|all]：blank 为抹除可重复写入的CD/DVD-RW，使用fast较快，all较完整
  -format ：仅针对 DVD+RW 这种格式的 DVD 而已  
[可用选项功能] 主要是写入 CD/DVD 时可使用的选项，常见的选项包括有：
   -data ：指定后面的文件以数据格式写入，不是以 CD 音轨(-audio)方式写入！
   speed=X ：指定烧录速度，例如CD可用 speed=40 为40倍数，DVD则可用 speed=4 之类
   -eject ：指定烧录完毕后自动退出光盘
   fs=Ym ：指定多少缓冲内存，可用在将映像档先缓存至缓冲内存。默认为 4m，
             一般建议可添加到 8m ，不过，还是得视你的烧录机而定。
针对 DVD 的选项功能：
   driveropts=burnfree ：打开 Buffer Underrun Free 模式的写入功能
   -sao                ：支持 DVD-RW 的格式
> # 应用示例 #

```
[root@www ~]# compress test.data                            //压缩test.data文件（源文件将消失，同时生成压缩文件test.data.Z）
[root@www ~]# compress -c test.data > test.data.Z           //使用-c参数压缩test.data文件，生成新的压缩文件test.data.Z且源文件不消失
[root@www ~]# uncompress test.data.Z                        //解压缩test.data.Z文件
[root@www ~]# gzip -c -9 test.data > test.data.gz9          //使用gzip，等级9压缩test.data文件，将压缩文件输出为test.data.gz9
[root@www ~]# zcat test.data.gz9                            //使用zcat读取压缩文件test.data.gz9的内容
[root@www ~]# bzip2 -k -9 test.data                         //使用bizp2，等级9压缩test.data文件
[root@www ~]# bzcat test.data.bz29                          //使用bzcat读取压缩文件test.data.bz29的内容
[root@www ~]# tar -jcv -f filename.tar.bz2 /etc             //打包并使用bzip2压缩/etc目录下所有文档，输出文件为filename.tar.bz2
[root@www ~]# tar -jtv -f filename.tar.bz2                  //查看压缩文件filename.tar.bz2
[root@www ~]# tar -jxv -f filename.tar.bz2 -C /tmp          //解包并使用bzip2解压缩文件filename.tar.bz2，将解压内容放到/tmp目录
[root@www ~]# tar -jcvf /tmp/back.tar.bz2 --exclude=/root/etc* /etc /root   //压缩打包/etc、/root目录，排除root下etc开头的文件
[root@www ~]# dump -S /dev/sda1                             //测试备份sda1需要多少容量
[root@www ~]# dump -0u -f /root/boot.dump /boot             //备份/boot分区至/root/boot.dump，同时更新这次dump的时间到/etc/dumpdates
[root@www ~]# dump -W                                       //查看当前文件系统备份情况
[root@www ~]# dump -0j -f /root/etc.dump.bz2 /etc           //备份目录时只能使用0级备份
[root@www ~]# restore -t -f /root/boot.dump                 //用来察看 dump 档
[root@www ~]# restore -C -f /root/boot.dump                 //比较dump与实际文件
[root@www ~]# restore -i -f /root/etc.dump.bz2              //进入互动模式
[root@www ~]# restore -r -f /root/boot.dump                 //还原整个文件系统
[root@www ~]# mkisofs -r -v -o /tmp/system.img /home /etc   //将/home和/etc目录添加至system.img镜像档,这种方法添加所有文件将会散乱的加入到镜像中。
//使用以下方法可以将镜像文档按照目录结构来创建
[root@www ~]# mkisofs -r -V 'linux_file' -o /tmp/system.img -m /home/lost+found -graft-point /root=/root /home=/home /etc=/etc

```

> # 总结 #

## 常见扩展名对应的压缩打包工具 ##
|扩展名|打包、压缩工具|
|:-:|:-:|
|*.Z|compress程序压缩的文件|
|*.gz|gzip程序压缩的文件|
|*.bz2|bzip2程序压缩的文件|
|*.tar|tar程序打包的数据，并且没有经过压缩|
|*.tar.gz|tar程序打包的文件，并且经过了gzip压缩|
|*.tar.bz2|tar程序打包的文件，并且经过了bzip2压缩|
