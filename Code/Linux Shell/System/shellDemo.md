# 一个脚本模版 #
```
#!/bin/bash
#Program:程序说明
#History:修改历史
#Date   auther    version
#环境变量
export PATH=$PATH:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
#读取变量
read -p "Please input your first name: " firstname  # 提示使用者输入
read -p "Please input your last name:  " lastname   # 提示使用者输入
echo -e "\nYour full name is: $firstname $lastname" # 结果由萤幕输出
#数值计算
total=$((123 * 456)
```
# 判断式 #

|测试参数|意义|
|:-:|:-:|
|-e|判断档名是否存在|
|-f|判断档名是否存在且为文件|
|-d|判断档名是否存在且为目录|
|-b|判断档名是否存在且为block device装置|
|-c|判断档名是否存在且为character device装置|
|-S|判断档名是否存在且为Socket文件|
|-p|判断档名是否存在且为FIFO（pipe）文件|
|-L|判断档名是否存在且为连接档|
|-r|判断档名是否存在且有读权限|
|-w|判断档名是否存在且有写权限|
|-x|判断档名是否存在且有执行权限|
|-u|判断档名是否存在且有SUID属性|
|-g|判断档名是否存在且有SGID属性|
|-k|判断档名是否存在且有Sbit属性|
|-s|判断档名是否存在且为非空白文件|
|**测试参数**|**两个文件之间比较**|
|-nt|判断file1是否比file2新|
|-ot|判断file1是否比file2旧|
|-ef|判断两个文件是否为同一个文件（主要判断两个文件是否指向相同inode）|
|**测试参数**|**两个变量比较**|
|-eq|两个数值相等|
|-ne|两个数值不等|
|-gt|n1大于n2|
|-lt|n1小于n2|
|-ge|n1大于等于n2|
|-le|n1小于等于n2|
|-z|判断字符串是否为空，为空返回true|
|-n|判断字符串是否非空，非空返回true|
|=|判断str1是否等于str2，相等返回true|
|!=|判断str1是否不等于str2，不等返回true|
|**测试参数**|**多重判断**|
|-a|两个条件同时为true时返回true（and）|
|-o|两个条件有一个为true时返回true（or）|
|!|取非|
