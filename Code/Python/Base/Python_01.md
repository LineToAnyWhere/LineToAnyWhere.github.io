# Python入门基础-day01 #

## 写在最前 ##
该套教程适用于有其他语言编程基础的同学，为了保证教程精简，能快速上手，语言细节部分不会赘述，建议想细学的买本书看，如果大家在学习过程中遇到什么问题，欢迎在后台提问，或添加我的QQ或微信：124660009。对于每次更新的课程，我会整理大家提过的问题做成Q&A附到教程最后。最后，周更，以上。

## Python3的安装 ##
Python3的安装比较简单，从[官网](https://www.python.org/downloads/)下载安装包,Windows用户安装时一路下一步就行，linux用户一般系统自带python2.7，如果要使用python3.6环境，需要下载[源代码](https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tar.xz),而后解压`tar xf Python-3.6.5.tgz`、编译安装`./configure && make && make install`

## Python3基本语法 ##
一元运算符与其他语言一样，二元运算符多了一个整除符号：`//`，一个幂运算符(优先级高于一元运算符)：`**`
赋值语句：`x = 3`  
控制台输出函数：`print(x)`  
获取用户输入：`x = input("x=")`  
建议使用获取用户输入(该函数会把输入转换为字符串)：`raw_input("enter your name")`  
原始字符串(正则表达式有用到,所有的字符都被当作原始字符，不需要转义，原始字符串的末尾不能是`\`)：`r'C:\windows\system32'`  
Unicode字符：`u'hello world~'`  
乘方函数：`x = pow(2,4)`  
四舍五入函数：`x = round(1.0/2.0)`

## 模块 ##
Python的模块可以理解为其他功能的扩展，需要使用import命令来导入:`import math`则导入了math包，可以使用更多的数学函数来进行计算，例如:`math.floor(32.9)`。导入也可以仅导入指定函数，例如：`from math import sqrt`,指定导入之后可以直接调用sqrt(25)

## Python脚本 ##
Python脚本一般以.py作为扩展名，例如`test.py`,运行时可以直接使用`python test.py`。在linux环境中，如果程序头有写清解释用的脚本，可以直接`./test.py`来执行，例如：
```
#!/bin/python3
print("滴，滴滴")
print("123" + "456" + "=123456" + str(777))
```
Python中使用`#`做注释符，使用`""`或者`''`来表示字符串或字符，同样使用`\`来做转义字符

## Q&A ##





python有6种内建序列，分别是：列表、元组、字符串、Unicode字符串、buffer对象、xrange对象
* **列表**  
  列表可以修改，内建函数有list()、
* **元组**  
  元组不能修改
* **字符串**
* **Unicode字符串**
* **buffer对象**
* **xrange对象**

序列的通用操作有种，分别是：索引，分片，相加，乘法，成员资格，长度，极值
* **索引**  
  通过下标来取的序列中的元素。例如:
  ```
  test="hello"                    //test[0]即为h
  ```
* **分片**  
  通过下标来取得一定范围内的元素。例如：
  ```
  numbers=[1,2,3,4,5,6,7,8,9,10]
  number[3:6]                     //[4,5,6]
  number[7:10]                    //[8,9,10]
  number[7,15]                    //[8,9,10]
  number[-3:]                     //[8,9,10]
  number[9:1]                     //[]
  number[:]                       //[1,2,3,4,5,6,7,8,9,10]
  number[0:10:5]                  //带步长参数分片结果是[1,6]
  number[::-5]                    //[10,5]
  ```
* **相加**  
  通过使用`+`号来连接两个序列（是可以对相同数据类型的序列操作）。例如：
  ```
  [1,2,3] + [3,4,5]               //结果是[1,2,3,3,4,5]
  ```
* **乘法**  
  使用数字`x`乘以一个序列会产生一个新的序列，新序列将原来的序列重复x次。例如：
  ```
  sequence=[None]*10              //使用None来初始化一个10长度的序列
  ```
* **成员资格**  
  使用`in`运算符可以检查一个值是否在序列中，返回值为一个bool。例如：
  ```
  permissions='rwx';
  'w' in permissions;             //返回true
  users=['root','ftp','ssh']
  input('Enter your user name') in users
  root                            //例如输入root返回true
  ```
* **长度，极值函数**  
  `len,min,max`分别可以求出序列的长度，最小，最大值。例如：
  ```
  numbers=[100,52,123]
  len(numbers)                    //3
  max(numbers)                    //123
  min(numbers)                    //52
  ```
