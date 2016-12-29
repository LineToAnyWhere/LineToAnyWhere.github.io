# Java Web —— Web技术基础 #
> ## 1. Servlet ##

Java Web 应用程序中所有的请求、相应最终都是由Servlet来完成的。  
在Servlet的生命周期中，有两个特殊注解，可以将一些方法放在init()之前和destory()之后执行，例如：  
```
#以下两种写法均可，被@PostConstruct注解的方法将在init()之前执行一次，被@PreDestory注解的方法将在destory()之后执行一次
@PostConstruct
public void someMethod(){
  ...
}
public @PreDestory void anotherMethod(){
  ...
}
```
Servlet有两种转跳，分别是Forward和Redirect：  
* Forward  
  ```
  #由服务器完成跳转，浏览器不会重新发出请求，特别的在使用forward方法前，不能有任何输出到达客户端，否则会抛出异常。
    RequestDispatcher dis = request.getRequestDispatcher("/index.html");
    dis.forward(request,response);
  ```
* Redirect
  ```
    #利用服务器返回的状态码实现操纵浏览器转跳，状态码详见HTTP协议，此处用的是301，302两个。其中301为永久转跳，302为临时转跳。
    response.setStatus(HttpServletResponse.SC_MOVED_TEMPORARILY);
    response.setHeader("Location", "http://www.google.com");
    #以上两步操作可以由一步代替
    response.sendRedirect("http://www.google.com");
  ```

Servlet 自动刷新&定时跳转
```
response.setHeader("Refresh", "1000;URL=http://localhost:8080/xx/index.html");
```
> ## 2. JSP ##

**JSP工作过程：**JSP是一种Servlet，但是与HttpServlet工作方式不太一样，HttpServlet是先编译再部署，而JSP是先部署，再编译。一般将新的JSP部署到服务器上之后，执行过程如下:例如部署了first.jsp，在第一次访问的时候，服务器会先将first.jsp转化为标准的JAVA源代码first_jsp.java，并将first_jsp.java编译为first_jsp.class文件，该文件便是JSP对应的Servlet。编译完成后运行该文件来响应客户端请求。以后再访问的时候就不再编译，直接调用该文件来响应。JSP既然也是Servlet，其生命周期也和Servlet一样。不过JSP还有自己的初始化方法与销毁方法:_jspInit()与_jspDestroy(),另外JSP是有序编译的。  
**JSP语法：**
* **JSP脚本 <% %>**  
  JSP脚本遵循Java语法，可以出现在JSP脚本的任何地方。
* **JSP输出 <%= %>**  
  JSP输出变量时，其后不能带";"号，在输出某个类对象时会自动调用其toString()方法。
* **JSP方法 <%! %>**  
  JSP方法中，声明方法或者全局变量时需使用此语法。
* **JSP指令 <%@ %>**  
  JSP指令用来声明JSP页面的一些属性等，例如编码方式、文档类型。JSP指令格式为<%@ directive {attribute=value}* %>。其中*号表示可以有0个或多个属性。directive的位置一般的指令有page、tablib、include。
* **JSP行为 <jsp:>**  
  JSP行为是一组JSP内置的标签，JSP行为是对常用的JSP功能的抽象与封装，包括自定义JSP行为与标准JSP行为。标准JSP行为格式为<jsp:elements {attribute="balue"}* />。

**JSP隐藏对象：**
* **out**  
  隐藏对象out是javax.servlet.jsp.JspWriter类的实例。
* **request**  
  隐藏对象request是javax.servlet.ServletRequest类的实例
* **response**  
  隐藏对象response是javax.servlet.ServletResponse类的实例
* **config**  
  隐藏对象config是javax.servletServletConfig类的实例。
* **session**  
  隐藏对象session是javax.servlet.http.HttpSession类的实例。
* **application**  
  隐藏对象application是javax.servlet.ServletContext类的对象。
* **page**  
  隐藏对象page为javax.servlet.jsp.HttpJspPage类的实例。page相当于普通java类中的关键字this。
* **pageContext**  
  隐藏对象pageContext为javax.servlet.jsp.PageContext类的实例。
* **exception**  
  隐藏对象exception为java.lang.Exception类的对象。

> ## 3. 会话跟踪 ##

**Cookie：**Cookie是一种通过一段文本来记录一部分数据在客户端的技术，Cookie使用key-value属性对来保存数据，一个cookie对象保存一个属性对，在java中，cookie被封装成了javax.servlet.http.Cookie类。因为浏览器在每次访问页面时都会带上cookie信息，因为使用cookie时最好做到数据少而精，以此来提高访问速度。客户端读取Cookie时，除了name和value属性，其他属性都是不可读的，也不会被浏览器提交给服务器，在修改Cookie时，只能使用同名Cookie来覆盖原来的Cookie，并且要保证除value、maxAge之外的所有属性都要与原Cookie一致，否则浏览器将视为两个Cookie。Cookie的常用属性如下：
* **String name**  
  记录该Cookie的名称
* **Object value**  
  该Cookie的值，如果为Unicode字符，需要为字符编码，如果为二进制需要BASE64编码
* **int maxAge**  
  记录Cookie的失效时间，以秒为单位，负数为临时cookie，关闭浏览器失效；0表示删除该Cookie，正数为失效时间。
* **boolean secure**  
  该Cookie是否仅被使用安全协议传输。例如HTTPS，SSL等，默认为false
* **String path**  
  设置Cookie的使用路径，例如设置为“/sessionWeb”,则只有contextPath为“/sessionWeb”的程序可以访问，如果设置为“/”,则本域名下都可以访问，注意该值必须以“/”结尾。
* **String domain**  
  设置可以访问该Cookie的域名，如果设置为“.ltany.org”，则所有以“ltany.org”结尾的域名都可以访问该Cookie，该值第一个字符必须为“.”。
* **String comment**  
  该Cookie的用处说明，浏览器显示Cookie信息的时候显示该说明
* **int version**  
  该Cookie的版本号，0表示遵循Netscape的规范，1表示遵循W3C的RFC2109规范

**Session：**Session是另一种记录客户状态的技术，对应的类为javax.servlet.http.HttpSession。同样使用key-value的形式保存数据，不同于Cookie，Session将数据保存在服务器上，并且可以保存对象数据。由于HTTP是无状态协议，因为每次浏览器访问服务器时，都会带上一个名为JSessionID的Cookie，对于手机等不支持Cookie的浏览器，服务器会使用url重写的方式，将JSESSIONID写入URl，以此来判断该请求是哪个用户所发出的请求。下面列出一些常用的操作的Session方法：
* **setAttribute**  
  设置Session属性
* **getAttribute**  
  获取Session属性
* **getAttributeNames**  
  返回Session中存在的属性名
* **removeAttribute**  
  移除Session属性
* **getId**  
  返回Session的ID（JSESSIONID）
* **getCreationTime**  
  返回Session的创建日期
* **getMaxInactiveInterval**  
  获取Session的超时时间
* **setMaxInactiveInterval**  
  设置Session的超时时间
* **invalidate**  
  销毁该Session

> ## 4. Filter ##

**Filter:** Filter意为过滤器，用于在Servlet之外对request或者response进行修改。Filter提出了滤镜链(FilterChain)的概念。一个FilterChain包括多个Filter。客户端的请求在抵达Servlet之前会经过所有的Filter，返回时也会经过所有的Filter。一个Filter必须实现javax.servlet.Filter接口。Filter接口有以下三个方法：
* **init**  
  初始化Filter时调用的函数
* **doFilter**  
  处理拦截到的请求
* **destroy**
  销毁Filter时调用的函数

> ## 5. Listener ##

**Listener:** Listener是Servlet规范的另一个高级特性，用于监听JavaWeb程序中的事件，例如创建、修改、删除Session、request、context等，并出发相应的事件。使用Listener时需要实现响应Listener接口，在Servlet2.5规范中共有8种Listener，分别如下：
* **HttpSessionListener**  
  监听Session的创建与销毁。
* **ServletContextListener**  
  监听context的创建与销毁。
* **ServletRequestListener**
  监听request的创建与销毁。（请求的页面包含多图片时可能会触发多次request事件）
* **HttpSessionAttributeListener**
  监听Session中的属性变化，分别会执行其added、replaced、removed方法。
* **ServletContextAttributeListener**
  监听Context中的属性变化，分别会执行其added、replaced、removed方法。
* **ServletRequestAttributeListener**  
  监听Request中的属性变化，分别会执行其added、replaced、removed方法。
* **HttpSessionBindingListener**
  当对象被放到Session里时执行valueBound()方法，当对象被从Session里移除时执行valueUnbound()方法。
* **HttpSessionActivationListener**
  当服务器关闭时，会将Session里的内容保存到硬盘上。服务器重新启动时，会将Session内容从硬盘上重新加载。钝化时会执行sessionWillPassivate()方法，重新加载时执行sessionDidActivate()方法。
