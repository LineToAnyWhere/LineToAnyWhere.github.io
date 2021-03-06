# Regularex #
> # Regularex简介 #
正则表达式是一种处理字符串的方法，他以行为单位来对字符串进行处理，通过一些规则和特殊符号的辅助可以轻松的把字符串处理成我们需要的样子。  
正则表达式受语系影响，正常情况下应该以LANG=C的语系为基准来使用正则表达式。

> # 正则规则 #

### 通用规则 ###
|特殊符号|功能|
|:-:|:-:|
|[:alnum:]|英文大小写以及数字，即0-9,a-z,A-Z|
|[:alpha:]|英文大小写，即a-z,A-Z|
|[:blank:]|空格键或者TAB键|
|[:cntrl:]|键盘上的控制键，即CR,LF,Tab,Del等|
|[:digit:]|数字，即0-9|
|[:graph:]|除了空格键和Tab之外的所有按键|
|[:lower:]|小写字母，即a-z|
|[:print:]|任何可以被打印出来的字节|
|[:punct:]|标点符号，即: " ' ? ! ; : # $ ...|
|[:upper:]|大写字母，即A-Z|
|[:space:]|任何产生空白的字节，包括空格，Tab，CR等|
|[:xdigit:]|16进制的数字类型，包括0-9，A-F，a-f|

### grep ###
|RE字符|意义与用法|
|:-:|:-:|
|^word|待搜索的word在行首，例如搜索以#号开头的行：grep '^#' a.txt|
|word$|待搜索的word在行尾，例如搜索以!号结尾的行：grep '!$' a.txt|
|.|至少有一个任意字符，例如搜索'e字符e'形式的行：grep 'e.e' a.txt|
|\|逃脱字符，去掉特殊符号的特殊意义，例如搜索带有\字符的行：grep \\ a.txt|
|*|重复0或无穷多个前一个字符，例如搜索goo.。.形式的行：grep 'goo*' a.txt|
|[list]|字节集合，里面列出想要取得的字节，例如取god或gad字符的行：grep g[oa] a.txt|
|[n1-n2]|字节集合，里面列出想要取得的字节范围，例如g任意d字符的行：grep g[a-z]d a.txt|
|[^list]|字节集合，里面列出不想取得的字节或字节范围，例如：grep 'oo[^t]' a.txt|
|\{n,m\}|连续n到m的前一个字符({1}{1,}{1,3})，例如找出连续2个或3个前一个字符，例如：grep go\{2,3\} a.txt|
|**RE字符**|**延伸的正则表达式**|
|+|至少一个前一个字符，例如搜索包含go..d的行：grep -e 'go+d' a.txt|
|?|零个或一个前一个字符，例如搜索god的行： grep -e 'go?d' a.txt|
|竖线分隔符|搜索或关系的两个字符串，例如搜索gd或god的行：grep -e 'gd竖线分隔符good' a.txt|
|()|找出群组字符串，例如搜索good或god的行：grep -e 'g(o竖线分隔符oo)d' a.txt|

### sed ###
|功能|用法|
|:-:|:-:|
|删除第2-5行|sed '2,5d'|
|第3行添加hello|sed '2a hello'|
|第2行插入hello|sed '2i hello'|
|替换第2-4行内容|sed '2,5c hello2-5'|
|列出2-5行内容|sed '2,5p'|
|搜索a并取代为b|sed 's/a/b/g'|
|直接替换文件中的内容|sed -i 's/a/b/g'|

### awk ###
awk中$0代表整行数据，$1,$2,$3......代表第1，2，3栏位的数据，在awk中，后序的参数都是以单引号`''`号阔住的。
使用示例：
```
使用规范：awk '条件类型1{动作1} 条件类型2{动作2} ...'
[root@www ~]# last -n 5| awk '{print $1 "\t lines: " NR "\t columns: " NF}'
root     lines: 1        columns: 10
[root@www ~]# cat /etc/passwd | awk '{FS=":"} $3 < 10 {print $1 "\t " $3}'
[root@www ~]# cat /etc/passwd | awk 'BEGIN {FS=":"} $3 < 10 {print $1 "\t " $3}'   //BEGIN确保awk在读入第一行时就以:为分隔符
```
|变量名称|意义|
|:-:|:-:|
|NF|每行（$0）拥有的栏位总数|
|NR|目前AWK处理的是第几行数据|
|FS|目前的分隔符，默认是空格|

### diff ###
diff使用示例：
```
diff [-bBi] from-file to-file
-b: 在一行中忽略多个空格。
-B: 忽略空白行的差异。
-i: 忽略大小写。
//通过diff命令生成补丁文件patch
diff -Naur passwd.old passwd.new > passwd.patch
```

### patch ###
patch使用示例：
```
[root@www ~]# patch -pN < patch_file        //升级
[root@www ~]# patch -R -pN < patch_file     //还原
```
