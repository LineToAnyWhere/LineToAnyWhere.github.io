# JavaScript 第三章-基本概念 #
## 语法规则 ##
* **区分大小写**
* **命名规则同类C语言**（其首字母可以为$）
* **注释规则同类C语言**
* **包含严格模式**（即浏览器将会根据ECMAScript5的标准执行，这会使ECMAScript3中的一些不确定行为被处理，对于不安全操作也会抛出异常）
* **语句结尾以分号结尾**（可以省略分号，推荐加上分号以方便对脚本压缩）
* **使用松散类型变量**（可以保存任何类型的数据,在函数中，如果隐式得声明变量，将会得到一个全局变量，例如message="Hi",此时message为全局变量）  

## 数据类型 ##
>ECMAScript中共有六种数据类型，其中五种简单数据类型(Undefined,Null,Boolean,Number,String)和一种复杂数据类型(Object)。  
JS中使用操作符`typeof`来判断变量的类型。（由于undefined派生自null，因此null==undefined返回值为true）.  
ECMAScript中的字符串是不可变得，如果改变某个变量则会先销毁原来的字符串，然后再用另一个**包含新值的字符串填充该变量**  
ECMAScript中的对象就是**一组数据和功能的集合**。在JS中Object同样是所有对象的基类。

**一些关于数据类型的函数：**  

|函数名|函数说明|
|:--------:|:--------:|
|Boolean()|将其他数据类型转换位Boolean类型|
|isFinite()|判断一个数是否又穷，是返回true，否返回false|
|isNaN()|判断一个参数是否**不是**数值,不是返回true，是数值返回false。其中在基于对象使用该函数时，会先调用对象的valueOf(),然后确定返回值是否可以转换为数值，如果不能则基于这个返回值调用toString()，再测试返回值。|
|Number()|将传入参数转为数值，空字符串返回0|
|parseInt(参数，转换为多少进制)|将传入参数转为数值，空字符串返回NaN。**建议在任何时候都传入第二个参数**|
|parseFloat()|与parseInt()类似，但只接受一个参数，会忽略前导0|
|toString()|null和undefined没有该方法。该方法可以接受一个参数，当对数字进行转换时可以添加进制参数，如：num.toString(16) 将num转为16进制。|
|String()|该函数可以转换null和undefined,一般在不知道被转换数据类型时使用|  

## 运算符 ##
### 一元运算符 ###
>**递增递减**运算符与C语言中的类似，不同之处在于，该运算符还可以用于字符串、布尔值、浮点值和对象。应用场景如下所示（但不建议使用此类晦涩难懂的写法）
* 应用于包含数字字符的字符串时，先将其转换为数字值，之后执行运算。
* 应用于不包含数字字符的字符串时，将其值设为NaN。
* 应用于布尔false（true）时，先转换为0（1），再执行运算.
* 应用于浮点数时，直接运算。
* 应用于对象时，先调用对象的valueOf()方法，如果取得NaN，则调用toString()方法后再进行运算。

> **加减**运算符同数学中一样，在对不同数据类型运算时，会进行相应的转换。

### 位运算符 ###
> 在对**NaN**和**Infinity**值应用位运算符时，这两个值会被当作**0**来处理。按位运算符对程序运算效率的优化有很大帮助。
* NOT 按位非** ~ ** (~X相当于-X-1)
* AND 按位与** & **
* OR  按位或** | **
* XOR 按位异或** ^ **
* **<<** 左移运算符 （移动时右侧使用 0 来补齐）
* **\>\>** 右移运算符 （移动时左侧使用符号位的数来补齐）
* **\>\>\>** 无符号右移 （移动时左侧使用 0 来补齐）

### 布尔运算符 ###
> 逻辑非 **!** 可用于任何数据类型。  
逻辑与 **&&** 也可用于任何数据类型，但其返回值不一定是布尔值：
* 如果第一个操作数是对象，则返回第二个操作数。
* 如果有一个操作数为null，则返回null。
* 如果有一个操作数为NaN，则返回NaN。
* 如果有一个操作数为undefined，则返回undefined。

> 逻辑或 **||** 也可用于任何数据类型，但其返回值不一定是布尔值：
* 如果第一个操作数是对象，则返回第一个操作数。
* 如果第一个操作数返回false，则返回第二个操作数。
* 如果两个操作数都是对象，则返回第一个操作数
* 如果两个操作数都是null，则返回null。
* 如果两个操作数为NaN，则返回NaN。
* 如果两个操作数为undefined，则返回undefined。  
**特殊用法：  
`var myObj = firstObj || backupObj;`  
此方法中firstObj为有效值时将会给myObj赋值，当其为null或其他无效值时，则将后备参数backupObj赋给myObj**

### 乘性运算符 ###
> 操作数为非数值的情况下会发生自动的类型转换，会先调用Number()转型函数将其转为数值，空字符将被转为0，布尔true被转为1.  

### 加性运算符 ###
> 对于加法来说，每个加法操作都是独立的，例如：**“1 plus 2 is” + 1 + 2； 将得到“1 plus 2 is 12” 如果想要使后两个数先得到计算需要这样写“1 plus 2 is” + (1 + 2)**  

### 关系运算符 ###
> 在比较两个字符串时，比较的是两个字符串对应的字符编码，其中大写字母的字符编码都小于小写字母。即 **B < a 是 true**  
任何数与NaN比较所得的结果都是**false**  

### 相等运算符 ###
> 相等和不等**== | != **, 先转换再比较。比较规则如下：
* null和undefined是相等的  
* null和undefined不能在比较时转换成其他任何值
* 如果有一个操作数是NaN，则返回false。NaN == NaN 为 **fasle**
* 如果比较的是两个对象，则比较他们是不是同一个对象。  

> 全等和不全等**=== | !==**， 仅比较不转换
* null == undefined返回true，因为他们是类似的值。而null === undefined返回false，因为他们是不同类型的值。

### 条件运算符 ###
> variable = boolean_expression ? true_value : false_value;  

### 赋值运算符 ###
> 包括以为运算符 <<=、>>=、>>>=  

### 逗号运算符 ###
> 主要用于在一条语句中执行多个操作。  

## 语句 ##
### if语句 ###
> if语句中的条件可以是任意表达式，ECMAScript会自动调用Boolean()来转换表达式的值为一个布尔值。  

### do-while语句 ###
> 后测试循环语句，其测试条件中的表达式同if语句。  

### while语句 ###
> 前测试循环语句，其测试条件中的表达式同if语句。  

### for语句 ###
> ECMAScript 中不存在块级作用域。因此for中定义的变了在外部同样可以访问到。

### for-in语句 ###
> for-in语句主要用于迭代，枚举对象。例如：  
```
for(var propName in window){
  document.write(propName)
}
```
如果要迭代的对象的变量值为null或undefined，则会抛出错误(在HTML5中修复为不再执行循环体)。  

### label语句 ###
> 使用label可以在代码中添加标签：**label：statement**  

### break和continue语句 ###
> break到一个label会使语句直接跳至最外层。  
  continue到一个label会使语句退出内部循环，执行外部循环：  
  ```
  var num = 0;
  outermost:
  for(var i = 0; i < 10; i++){
    for(var j = 0; j < 10; j++){
      if(i == 5 && j == 5){
        continue outermost;
      }
      num ++;
    }
  }
  alert(num) //95
  ```  

### with语句 ###
> with用于将代码的作用域设置到一个特定的对象中：
  ```
  var qs = location.search.substring(1);
  var hostName = location.hostname;
  var url = location.href;
  ```
  将上述代码简写为下述代码：
  ```
  with(location){
    var qs = search.substring(1);
    var hostName = hostname;
    var url = href;
  }
  ```  

### switch语句 ###
> 类似C语言，但其自己的特性是，switch中可以使用任何数据类型，包括字符串，对象。同时，case的值可以是常量，变量，表达式。所有switch中的比较使用的是**===** 因此不会对值进行类型转换。例如：
```
switch("hello world"){
  case "hello" + " world":
    alert("Greeting was found");
    break;
  case "goodbye":
    alert("Closing was found");
    break;
  default:
    alert("Unexpected message was found");
}
```

## 函数 ##
> 传入ECMAScript函数的参数会以一个数组(并不是Array的实例)的形式传入，在函数内部可以使用**arguments**对象来对传入参数进行访问。特别是在ECMAScript中，没有函数签名。导致其没有函数重载，并且在**ECMAScript中的所偶参数传递的都是值，不可能通过引用传递参数。**  
arguments在使用时可以这样：
```
function doadd(num1,num2){
  arguments[1] = 10;
  alert(arguments[0] + num2); //num2现在的值为10
  alert(arguments.length);
}
```
上述代码中使用arguments访问了传入参数，计算了arguments的传入个数。并且在这个函数中，修改了第二个参数的值，这个在ECMAScript中存在这样的特殊情况
* arguments访问的参数和实参使用不同的内存地址
* 通过arguments修改传入参数值的时候，会自动同步到实参
* 对于实参个数少于形参时，未传入的实参将会以undefined赋值。
