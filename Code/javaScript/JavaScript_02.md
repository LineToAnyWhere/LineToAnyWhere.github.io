# JavaScript 第二章-标签的使用 #
## `<script>`元素的使用 ##
### `<script>`不常见属性：###
* async：表示应该立即下载脚本，但不妨碍页面中的其他操作。
* defer：表示脚本可以延迟到文档完全被解析和显示之后再执行。

### 在HTML中使用： ###
>在浏览器解析JS代码或者外部JS文件时（**包括下载**），页面的处理过程都会暂时停止。  
JS引用标签一般放置在`<body>`标签的底部，这样可以使网页先加载DOM而无须等待JS的下载。  
在H5的规定中**延迟脚本**需要按出现的顺序执行，并且只适用于外部脚本文件。  
**异步脚本**不保证执行的先后顺序，因此需要确定加载的异步加载的JS脚本互不依赖，并且采用异步加载时，不要在JS中修改DOM，异步脚本一定会在页面的load事件前执行。

### 在XHTML中使用： ###
>由于XHTML的语法规定(主要是需要转义'<''>'等符号)，在XHTML中使用`内嵌<script>`脚本一般需要使用**CData**片段来包含，例如：  

```
<script type="text/javascript">
<![CDATA[
  function compare(a, b){
    return a < b ? true : false;
  }
]]>
</script>
```  
## `<noscript>`元素的使用 ##
>`<noscript>`元素主要用于在浏览器不支持JavaScript时或者是禁用JavaScript时显示其内容。示例如下：

```
<body>
  <noscript>
    <p>您的浏览器不支持javascript脚本或您禁用了它。</p>
  </noscript>
</body>
```
## 文档模式 ##
### 历史上出现过的文档模式 ###
* **混杂模式（quirks mode）**
* **标准模式（standards mode）**
* **准标准模式（almost standards mode）**  

>文档模式的作用主要是告诉浏览器按照什么样的规范来解读JavaScript代码。如果未声明，一般浏览器会默认开启**混杂模式**，然后混杂模式对跨浏览器的情况并没有良好的一致性。其中H5的标准模式如下所示：  

```
<!-- HTML5 -->
<!DOCTYPE html>
```
