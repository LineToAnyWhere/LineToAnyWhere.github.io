# cal #
> # 命令描述 #

显示日历命令
> # 常用参数 #

* **[[[day] month] year]**  
  用于显示某年某月的日历

> # 应用示例 #

```
  cal 2017        //显示2017年日历
  cal 02 2017     //显示2017年2月日历
  cal 28 02 2017  //显示2017年2月日历，日期停在28号
```
# bc #
> # 命令描述 #

Linux 下的计算器软件
> # 常用参数 #

* **scale=3**  
  设置计算机输出的小数点后位数，此例为输出小数点后三位。

> # 应用示例 #

```
功能简单，此处不再举例。
```
# date #
> # 命令描述 #

用于显示Linux的系统时间。
> # 常用参数 #

* **[+FORMAT]**  
  格式化输出日期，常用的格式化有：%Y、%m、%d、%H、%M、%S，分别代表年月日，时分秒。

> # 应用示例 #

```
  date +%Y/%m/%d
  date +%H:%M
  date "+%Y-%m-%d %H:%M:%S"
//AIX取昨天数据需要更改时区，不支持-d参数
  delname=`TZ=aaa24 date +%Y%m%d`
//AIX取明天数据需要更改时区，不支持-d参数
  delname=`TZ=aaa-24 date +%Y%m%d`
//昨天：
  date -d '-1 day' +'%Y%m%d'
  date -d "1 days ago" +%Y%m%d
  date --date='yesterday' '+%Y%m%d'
//前天
  date -d '-2 day' +'%Y%m%d'
  date -d "2 days ago" +%Y%m%d
//大前天
  date -d '-3 day' +'%Y%m%d'
  date -d "3 days ago" +%Y%m%d
//明天
  date -d '+1 day' +'%Y%m%d'
  date -d "1 days next" +%Y%m%d
  date --date='tomorrow' '+%Y%m%d'
//日期计算
  date -d "${arr[0]:6:8} ${arr[0]:14} +8 hour" +%Y%m%d%H
```
# 编码转换 #
> # 命令描述 #

将文档格式转换为不同编码
> # 常用参数 #

* **iconv**  
  --list ：列出 iconv 支持的语系数据  
  -f ：from ，原来的编码格式  
  -t ：to ，要转换的编码格式  
  -o file ：如果要保留原本的档案，那么使用 -o 新档名，可以建立新编码档案  

> # 应用示例 #

```
  iconv -f big5 -t utf8 vi.big5 -o vi.utf8    //将vi.big5从big5转为utf8，并生成新文件vi.utf8
```
# 格式转换 #
> # 命令描述 #

将DOS格式文档与linux/unix格式文档格式互转
> # 常用参数 #

* **dos2unix**  
  -k :保留该档案原本的 mtime 时间格式 (不更新档案上次内容经过修订的时间)  
  -n :保留原本的旧档，将转换后的内容输出到新档案，如： dos2unix -n old new
* **unix2dos**  
  -k :保留该档案原本的 mtime 时间格式 (不更新档案上次内容经过修订的时间)  
  -n :保留原本的旧档，将转换后的内容输出到新档案，如： dos2unix -n old new

> # 应用示例 #

```
  unix2dos -k man.config                       //将unix转为dos格式
  dos2unix -k -n man.config man.config.linux   //将dos格式转为unix，并保存为新文件
```
# 关机相关 #
> # 命令描述 #

* **shutdown**    关机
* **reboot**      重启
* **halt**        关机
* **poweroff**    关机
* **init**        切换运行等级

> # 常用参数 #

* **shutdown**  
  -t sec ： -t 后面加秒数，亦即『过几秒后关机』的意思   
  -k     ： 不要真的关机，只是发送警告信息出去！  
  -r     ： 在将系统的服务停掉之后就重新启动(常用)  
  -h     ： 将系统的服务停掉后，立即关机。 (常用)  
  -n     ： 不经过 init 程序，直接以 shutdown 的功能来关机  
  -f     ： 关机并启动之后，强制略过 fsck 的磁盘检查  
  -F     ： 系统重新启动之后，强制进行 fsck 的磁盘检查  
  -c     ： 取消已经在进行的 shutdown 命令内容。  
* **reboot**  
  -n     ： 不经过sync，直接进行reboot或halt  
  -f     ： 强制reboot或halt，不调用shutdown  
  -p     ： 关机并且调用halt   
* **halt**  
  -n     ： 不经过sync，直接进行reboot或halt  
  -f     ： 强制reboot或halt，不调用shutdown  
  -p     ： 关机并且调用halt   
* **poweroff**  
  -n     ： 不经过sync，直接进行reboot或halt  
  -f     ： 强制reboot或halt，不调用shutdown  
  -p     ： 关机并且调用halt   
* **init**  
  init 0 关机  
  init 3 纯文本模式  
  init 5 含有图形接口模式  
  init 6 重新启动  

> # 应用示例 #

* **shutdown**
```
[root@www ~]# shutdown -h now  
立刻关机，其中 now 相当于时间为 0 的状态  
[root@www ~]# shutdown -h 20:25
系统在今天的 20:25 分会关机，若在21:25才下达此命令，则隔天才关机
[root@www ~]# shutdown -h +10
系统再过十分钟后自动关机
[root@www ~]# shutdown -r now
系统立刻重新启动
[root@www ~]# shutdown -r +30 'The system will reboot'  
再过三十分钟系统会重新启动，并显示后面的信息给所有在在线的使用者
[root@www ~]# shutdown -k now 'This system will reboot'  
仅发出警告信件的参数！系统并不会关机啦！吓唬人！
```

# 字符串处理 #
> # 命令描述 #

* **cut**   截取字符串中的数据
* **grep**  筛选字符串中的数据
* **sort**  对数据进行排序
* **wc**    统计输入的行，单词，字符数
* **uniq**  去重
* **join**  对数据进行合并
* **paste** 对数据进行合并
* **split** 对数据进行拆分

> # 常用参数 #

* **cut**  
  -d ：后面接分隔字符。与 -f 一起使用  
  -f ：依据 -d 的分隔字符将一段信息分割成为数段，用 -f 取出第几段的意思  
  -c ：以字符 (characters) 的单位取出固定字符区间  
* **grep**  
  -a ：将 binary 文件以 text 文件的方式搜寻数据  
  -c ：计算找到 '搜寻字符串' 的次数  
  -i ：忽略大小写的不同，所以大小写视为相同  
  -n ：顺便输出行号  
  -v ：反向选择，亦即显示出没有 '搜寻字符串' 内容的那一行  
  --color=auto ：可以将找到的关键词部分加上颜色的显示  
* **sort**  
  -f ：忽略大小写的差异，例如 A 与 a 视为编码相同  
  -b ：忽略最前面的空格符部分  
  -M ：以月份的名字来排序，例如 JAN, DEC 等等的排序方法  
  -n ：使用『纯数字』进行排序(默认是以文字型态来排序的)  
  -r ：反向排序  
  -u ：就是 uniq ，相同的数据中，仅出现一行代表  
  -t ：分隔符，默认是用 [tab] 键来分隔  
  -k ：以那个区间 (field) 来进行排序的意思  
* **wc**  
  -l ：仅列出行  
  -w ：仅列出多少字(英文单字)  
  -m ：多少字符  
* **uniq**  
  -i ：忽略大小写字符的不同  
  -c ：进行计数
* **join**  
  -t ：join 默认以空格符分隔数据，并且比对『第一个字段』的数据，如果两个文件相同，则将两笔数据联成一行，且第一个字段放在第一个  
  -i ：忽略大小写的差异  
  -1 ：这个是数字的 1 ，代表『第一个文件要用那个字段来分析』的意思  
  -2 ：代表『第二个文件要用那个字段来分析』的意思  
* **split**  
  -b ：后面可接欲分割成的文件大小，可加单位，例如 b, k, m 等  
  -l ：以行数来进行分割  
  PREFIX ：代表前导符的意思，可作为分割文件的前导文字。

> # 应用示例 #

```
[root@www ~]# echo $PATH | cut -d ':' -f 3,5                            //以：分割取出第三与第五列
[root@www ~]# export | cut -c 12-                                       //取出12个字符之后的内容
[root@www ~]# join -t ':' /etc/passwd /etc/shadow                       //以：分割结合
[root@www ~]# join -t ':' -1 4 /etc/passwd -2 3 /etc/group              //以：分割，取第一个文件第四列，第二个文件第三列合并
[root@www ~]# split -b 300k /etc/termcap termcap                        //将termcap分成以300k每个的文件
[root@www ~]# cat termcap* >> termcapback                               //将拆分的文件合并
```
