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
> ## 3. 会话跟踪 ##
> ## 4. Filter ##
> ## 5. Listener ##
