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
* JSP脚本 <% %>  
  > JSP脚本遵循Java语法，可以出现在JSP脚本的任何地方。
* JSP输出 <%= %>  
  JSP输出变量时，其后不能带";"号，在输出某个类对象时会自动调用其toString()方法。
* JSP方法 <%! %>
* JSP指令 <%@ %>
* JSP行为 <jsp:>

> ## 3. 会话跟踪 ##
> ## 4. Filter ##
> ## 5. Listener ##
