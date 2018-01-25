# Python条件、循环 #

## 导入外部包 ##
```
import somemodule [as xx]
from somemodule import somefunction [as xx]
from somemodule import somefunction, anotherfunction
from somemodule import *
```
## 赋值语句 ##
```
x, y, z = 1, 2, 3
x, y = y, x                       //交换两个变量的值X
x = y = somefunction()            //链式赋值
```
## 布尔值 ##
```
False None 0 "" () [] {}          //作为布尔值时为假的值，其他一切为真
```
## 条件执行 ##
```
num = input('Enter a number:')
if num > 0:
  print(num + "大于零")
elif num < 0:
  print(num + "小于零")
else:
  print(num + "等于零")
```
## 运算符 ##
```
==, <, >, >=, <=, !=, is, is not, in, not in
and, or, not                      //布尔运算符
0 < age < 100                     //比较运算符可以连用
```
## 循环语句 ##
```
x = 1
while x <= 100:
  x += 1
```
