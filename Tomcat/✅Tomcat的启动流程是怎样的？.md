# ✅Tomcat的启动流程是怎样的？

# 典型回答


想要详细了解Tomcat的启动流程， 可以通过代码来看，主要入口就是<font style="color:rgb(68, 68, 68);">Bootstrap这个类中，主要就是三个方法，init，load和start，下图是别人总结的一张完整的流程图，大家可以看一下：</font>

<font style="color:rgb(68, 68, 68);"></font>

![1681550795216-558ee94f-f6f2-4610-984f-bc60495188b4.jpeg](./img/G-HyyLh9-SH9gteJ/1681550795216-558ee94f-f6f2-4610-984f-bc60495188b4-279187.jpeg)



整个过程还是比较复杂的，我尝试着总结一下，方便大家理解和记忆，Tomcat的启动过程主要由以下几个步骤：



+ <font style="color:rgb(68, 68, 68);">bootstrap.init</font>
    - <font style="color:rgb(68, 68, 68);">加载启动类：加载启动相关的类加载器及类，创建Catelina对象。</font>
+ <font style="color:rgb(68, 68, 68);">bootstrap.load</font>
    - 加载配置文件：主要包括server.xml和web.xml，其中server.xml用于配置Tomcat的基础服务，如端口号、线程池等；web.xml用于配置Web应用程序的参数、Servlet和过滤器等信息。
    - 初始化组件：依次初始化Tomcat的各个组件，包括Server、Service、Connector、Engine、Host和Context，它们都是Tomcat运行的重要组成部分。
+ <font style="color:rgb(68, 68, 68);">bootstrap.start</font>
    - 启动服务：当所有组件初始化完成后，Tomcat会依次启动Connector、Engine、Host和Context，最终启动整个Tomcat服务。
    - 部署应用：启动完成后，会扫描指定的Web应用程序目录，自动部署已经打包好的Web应用程序。



以上步骤执行完之后，一个web应用就启动了，后续有请求到达时，会根据请求的URL匹配相应的Context，然后将请求转发到相应的Servlet或JSP进行处理。

  
 

<font style="color:rgb(68, 68, 68);"></font>



> 更新: 2024-07-08 12:11:50  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/rvm0tu1yvwobb6or>