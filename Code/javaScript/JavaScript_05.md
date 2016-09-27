# JavaScript 第五章-引用类型 #
## 基本类型和引用类型 ##
#### Object类型 ####
> 在应用中主要用于**存储和传输数据**，一般用在传递参数时，对于必须值使用命名参数，对于可选参数使用对象字面量来封装。创建对象的两种写法：
```
方法一：
var person = new Object();
person.name = "Tom";
person.age = 19;
方法二：（该方法不会调用object的构造函数）
var person = {
  name:"Tom",
  age:19
};
```
一般访问对象属性时使用的都是点表示法，但是在JS中也可以使用方括号表示法来访问对象的属性。在使用方括号语法时，将要访问的属性以字符串的形式放在方括号中，**方括号法的好处是可以使用变了来访问属性，并且在属性含有空格等非字母非数字时，只能使用方括号法来访问。**示例如下：  
```
person["name"]等于person.name;
var propertyName = "name";
person[propertyName];
person["first name"] = "Tom"
```

#### Array类型 ####
> js中，一个Array类型中可以放入各种类型的数据，这与其他语言所有区别。**Array中的length属性不是只读的，可以通过修改其值来减少数组的项数。**
```
一些创建Array的方法：
var colors = new Array();
var colors = new Array(20);
var colors = new Array("red","blue","green");
colors.length = 2;    //此时colors中的green就被移除了。
```
* **数组检测**
      对于只有一个全局执行环境的情况下可以使用instanceof来检测Array。但是当全局执行环境有多个时，则需要使用isArray()方法来检测。
* **转换方法**
      一般情况下默认会使用Array的toString()方法完成转换，转换后是以逗号分隔的字符串。如果想要使用其他分隔符来分割，可以使用如下方法：
      alert(colors.join("|"));则会以|分割。

#### 栈方法 ####
> ECMAScript为数据提供了栈的处理方法。push()方法用于入栈，pop()方法用于出栈。
示例：
  var colors = ["red","blue"];
  var colors[3] = "brown";
  colors.push("black");
  var item = colors.pop();
  alert(tiem);
#### Object类型 ####
#### Object类型 ####
#### Object类型 ####
#### Object类型 ####
#### Object类型 ####
#### Object类型 ####
#### Object类型 ####
#### Object类型 ####

## 执行环境和作用域 ##
## 垃圾回收 ##
