# Java Web —— web应用及web服务器简介 #
> ## 1. Java Web 应用基本结构 ##

Java Web应用程序是由各种各样的组件组合而成的。一个基本的Java Web应用程序首先需要本身的代码和依赖的三方库代码，然后需要部署描述符，最后将这些打包为WAR发布就完成了一个基本JAVA Web应用程序的开发，发布。
> ### 1.1 Servlet、过滤器、监听器和JSP ###

* **Servlet**  
  Servlet是用于接受和响应HTTP请求的JAVA类。几乎发送到应用程序的所有请求都将经过某种类型的Servlet处理。（在Servlet技术出现之前，普遍使用的动态网页生成程序称作CGI）
* **过滤器**  
  过滤器可以拦截发送给Servlet的请求，通过使用过滤器可以完成很多需求，类似数据压缩，加密，认证等等。
* **监听器**  
  监听器负责通知某些代码做一些事情，例如在Java Web应用程序的生命周期中，通知应用程序启动、关闭、HTTP会话创建、销毁等。  
* **JSP**  
  JSP可以为Web应用程序创建动态的、基于HTML的图形用户界面。JSP还包含很多其他内容，例如STL、自定义标签、国际化、本地化等。
*  **其他组件**  
  Java Web中还包括很多其他组件，例如JSTL、EL表达式、WebSocket等等

> ### 1.2 目录结构和War文件 ###

Java Web应用程序最终将以War文件或未归档的Web应用程序目录进行部署。Jar 文件只是一个简单的ZIP格式归档文件，其中包含了可以被JVM识别的标准目录结构。Java Web应用程序归档或War是Java Web应用程序对应的归档文件。

> ### 1.3 部署描述符 ###

> ### 1.4 类加载器 ###

> ### 1.5 企业级应用程序归档文件 ###

> ## 2. Web 容器 ##

> ### 2.1 Apache Tomcat ###

> ### 2.2 GlassFish ###

> ### 2.3 JBOSS & WildFly ###

> ### 2.4 其他容器和应用服务器 ###

a
> ## 3. 开发环境搭建 ##

首先需要安装JAVA开发环境和运行环境，这里直接到oracle官网下载[**JDK**](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)并安装即可。其次需要安装一个IDE来辅助我们开发，这里选择大众的[**Eclipse**](https://www.eclipse.org/downloads/)，同样到官网下载安装。最后我们需要安装一个web服务器，这里选择apache的[**tomcat**](http://tomcat.apache.org/)（这里不再赘述安装方法）。
> ### 3.1 使用时常见问题 ###  

* **修改tomcat端口号**  
  端口号配置是在tomcat安装目录的*/conf/server.xml*文件中记录，找到<Connector>标签，将**port**属性改为你期望的端口即可，修改完成后需要重启tomcat生效。修改时需注意不要改到已被占用的端口，这将会导致tomcat无法启动。
* **在tomcat上设置虚拟主机**  
  在tomcat设置虚拟主机可以使其同时运行多个不同域名的网站。修改的地方同样是在*/conf/server.xml*中，找到<Engine>标签，添加多个**Host**标签来添加，例如：  
  ```
  <Engine name="Catalina" defaultHost="localhost">  
    <Host name="localhost"  appBase="webapps/test" unpackWARs="true" autoDeploy="true">  
    <Host name="www.ltany.org"  appBase="webapps/ltany" unpackWARs="true" autoDeploy="true">  
  </Engine>
  ```
