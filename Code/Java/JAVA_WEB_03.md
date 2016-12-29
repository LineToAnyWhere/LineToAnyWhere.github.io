# Java Web —— Web高级技术 #
> ## 1. JSTL标签库 ##

> ## 2. JSTL标签库 ##
> ## 3. JSTL标签库 ##
> ## 4. JDBC概述 ##
> ## 5. XML概述 ##

**XML**(Extensible Markup Language)是由W3C推出的一种数据交换标准。可以用于定义Web网页上的文档元素和商业文档，同时还可以用于复杂结构数据的表示和传输。在结构上有些类似于HTML.XML的前身是SGML。当使用XML表示数据时，可以根据用户需要组织成任意符合XML规范的形式，具有很强的灵活性。其一般用途主要有：存储数据、分离数据、交换数据、共享数据。在XML技术架构中，DTD和Schema负责数据定义，DOM和SAX负责数据解析，样式风格为XSTL.下面举一个XML的例子，如：
```
  <article>
    <title>JAVA</title>
    <author>张三</author>
    <price>20.0</price>
  </article>
  //
  <article>
    <property name="title" value="JAVA" />
    <property name="author" value="张三" />
    <property name="price" value="20.0" />
  </article>
```
** XML基本语法 **
* ** XML需要有声明文档 **  
  `<?xml version="1.0" encoding="UTF-8">`
* ** 标签必须闭合 **  
* ** 必须合理嵌套 **  
* ** XML元素规范 **  
  元素的名字可以包含字母、数字和其他符号，但是不能以数字或者标点符号开头，布恩那个以XML开头，元素名中不能包含空格，也不能有一些特殊字符(&=<>/)等
* ** 一个元素只能有一个同名属性**  
* ** 只能有一个根元素 **  
* ** 大小写敏感 **  
* ** 元素中空格被保留 **  
* ** 注释写法与HTML相同 **  
* ** 需要大面积转义时使用<![CDATA[ ]]> **  
* ** 表示特殊符号需要使用转义字符 **  

|字符|转义字符|
|:--------:|:--------:|
|<|&lt|
|>|&gt|
|&|&amp|
|'|&apos|
|"|&quot|

** JAVA中关于XML的API **
JDK中关于XML的API有两个，分别是
* **JAXP** (The Java API For XML Processing) : 主要负责解析XML
* **JAXB** (JAVA Architecture for XML Binding) : 主要负责将XML映射为JAVA对象
