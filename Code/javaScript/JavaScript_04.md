# JavaScript 第四章-变量、作用域和内存 #
## 基本类型和引用类型 ##
> JS中的变量属于**松散类型**的变量，因此其变量在定义时可以赋值任何数据。

* **动态属性**  
      在JS中只能给引用类型值动态添加属性。而基本数据类型虽然添加时也不会报错，但那并不是有效的代码，会在使用时输出undefined。
* **复制变量值**
      在基本变量之间复制时，所复制的值是相互独立的，互不影响。例如：
      var num1 = 5;
      var num2 = num1;
      其中的num2在创建时使用的是num1的一个副本，而非num1本身。

      在引用类型变量之间复制时，所复制的是引用本身，因此当改变对象本身时，会同时对两个引用产生影响。
* **参数传递**
      ECMAScript中所有函数的参数都是按值传递。但是在访问的时候区分为按值访问和按引用访问。
      值访问不会改变函数外部的值。引用访问会改变函数外部的值。
* **值类型检测**
      检测值类型时一般使用typeof工具，其中字符串返回string，数字返回number，布尔返回boolean，未定义变了返回undefined，null和对象返回object，函数返回function。
      如果想更具体得检测object的原型，则需要使用instanceof工具。

## 执行环境和作用域 ##
> js中，每个函数都有自己的执行环境，当代码在一个环境中执行时，会创建变量对象的一个作用域链，其用途是保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端始终是当前执行的代码所在环境的变量对象。他会在执行时一级一级向上搜索，就像由函数内部向上层函数搜索一样，直到找到所需的内容。其永远也不会向下搜索（也就是外部函数无法访问函数中的局部变量）。示例如下：
```
var color = "blue";
function changeColor(){
	var anotherColor = "red";
	function swapColors(){
		var tempColor = anotherColor;
		anotherColor = color;
		color = tempColor;
		console.info(tempColor);          //red
		console.info(anotherColor);       //blue
		console.info(color);              //red
	}
	swapColors();
}
changeColor();
console.info(anotherColor);           
//此处会报错，但是如果变量声明是没有写var则会正常输出，原因是浏览器会将anotherColor转化为局部变量
```  

* **延长作用域链**
      在一般情况下，执行环境类型只有两种————全局和局部，但是在遇到try-catch语句的catch块和with语句时，作用域链就会加长。
      function buildUrl(){
      	var qs = "?debug=true";
      	with(location){
      		var url = href + qs;
      	}
      	return url;
      }
      url变量为函数执行环境的一部分。
* **没有块级作用域**
      JS中没有块级作用域的变量，简单暴力的例子如下：
      if(true){
        var color = "blue";
      }
      alert(color) //输出blue   但是在C语言中，color出了if的块将会被销毁
      1. 声明变量
        使用var声明的变量会自动添加到最接近的环境中。如果初始化是没有使用var，则会添加到全局变量中。
      2. 查询标识符
        JS中查询表示符按照链状向上。

## 垃圾回收 ##
* **标记清除**
      垃圾收集器在运行时会对所有存储在内存中的变量加上标记，然后去掉环境中的变量以及被环境中的变量引用的变量的标记。而再次之后再次被加上标记的变量被视为准备删除的变量。
* **引用计数**
      当声明了一个变量并将一个引用类型值赋给该变量时，则这个值的引用次数就是1.如果同一个值又被赋给另一个变量时，则该值的引用次数加1.
      相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数减1.当引用次数为0时，回收。
      引用计数的策略中，如果出现循环引用则会导致内存泄漏。
