# 省略了MySQL JDBC web三件套的笔记

## 基本概念

> web开发

* 静态web
 html css
 提供给所有人看到数据始终不会发生变化

* 动态web
  * 淘宝，几乎所有网站
  * 提供给所有人看到的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同
  * 技术栈：Servlet/SP,ASP,PHP

在Java中，动态web资源开发的技术成为JavaWeb

## web应用程序

web应用程序：可以提供浏览器访问的程序

* a.html\b.html\c.html多个web资源可以被外界访问，对外界提供服务
* 访问的任何资源都存在于一台计算机上
* URL
* 这个统一的web资源会被放在同一个资源下
* 一个web应用由多部份组成
    * html，css，js
    * jsp，servl
    * java
    * jar包
    * 配置文件

web应用程序编写完毕后，若想提供给外界访问，需要一个服务器来统一管理

## 静态web

* *.htm,*.html这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取，通络
* 静态web的缺点
  * web页面无法动态更新，所有用户看到的都是同一个页面
    * 轮播图，点击特效、伪动态
    * Js
    * VBScript
  * 它无法与数据库交互

## 动态web

页面会动态展示：“web”展示的效果因人而异

缺点

* 假如服务器的动态web资源出现了错误，我们需要重新编写我们的后台程序，重新发布
  * 停机维护

优点

* 可以动态更新
* 可以与数据库交互

## web服务器

### 技术

ASP
 * 微软
 * 在HTML中嵌入了VB的脚本，ASP+COM
php
 * 开发速度快，功能强大，跨平台
 * 无法承载大访问的情况

JSP/Servlet:
 * sun 公司主推的B/S架构
 * 基于Java语言
 * 可以承载三高问题
   
### 服务器

web服务器

被动处理用户的请求和一些相应信息

Tomcat 初学者，首选 
IIS 

### 启动Tomcat

双击startup

直接x

访问8080端口

### Tomcat配置

服务器核心配置文件

server.xml

### 网站时怎么访问的

输入域名

检查本机hosts有没有域名映射

有：直接返回对应ip
没有，去dns服务器找，找不到就返回找不到

### 发布网站

将自己写的网站放到服务器中指定的文件夹下，就可以访问了

## Http

超文本传输协议，通常运行在TCP上
* 文本：html、字符串
* 超文本： 图片，音乐，视频，定位，地图。。。。。。
* 80

Https： 安全的

### 两个时代
* http1.0
  * http/1.0：客户端可以与web服务器链接，只能获得一个web资源，断开连接
* hyyp2.0
  * http/1.1：可以获得多个web资源

### http请求
客户端---发请求---服务器
#### 请求行
* 请求行中的请求方式：GET
* 请求方式：Get，Post 。。。
  * Get：请求能携带的参数比较少，大小有限制，会在url中显示，不安全但高效
  * Post：与Get完全相反
  
#### 消息头
告诉浏览器所支持的数据类型
支持哪种编码
语言环境
缓存控制
告诉浏览器，请求完断开还是保持链接

### http响应
服务器---响应---客户端

#### 响应体

## Servlet

* Servlet 是sun公司开发动态web的一项技术
* Sun再这些API中提供一个接口就是Servlet
  * 编写一个类实现Servlet接口
  * 把开发好的Java类部署到Web服务器中
  
  把实现了Servlet接口的Java程序就是Servlet
### Maven环境优化

修改web.xml为最新
将maven的结构搭建完整

### 编写Servlet

直接继承HttpServlet

```java
package com.zerui.servlet;


import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;
import java.io.PrintWriter;

public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        
        PrintWriter writer = resp.getWriter();
        
        writer.println("Hello Servlet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

### 编写Servlet的映射

我们写的是Java程序，但是要通过浏览器访问
而浏览器需要链接web服务器
所以我们需要在web服务中注册我们写的Servet
还要给一个浏览器能够访问的路径

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
<!--注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.zerui.servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```


### Mapping
一个Servlet可以指定一个映射路径

一个Servlet可以指定多个路径

一个Servlet可以指定同用映射路径

```xml
<servlet-name>hello</servlet-name>
<url-pattern>/hello/*</url-pattern>
```

默认请路径

```xml
<servlet-name>hello</servlet-name>
<url-pattern>/*</url-pattern>
```

指定一些后缀或者前缀等等

 ### servletcontext

 Web容器在启动的时候
 会为每一个Web程序都创建一个对应的ServletContext对象
 它代表了当前的web应用
* 共享数据
  在这个Servlet中的数据可以在另一个Servlet中获取
  ```java
  ServletContext context = this.getServletContext();
  String username = (String) context.getAttribute("username");
  //username在另一个Servlet中setAttribute设置

  resp.setContextType("text/html");
  resp.setcharacterEncoding("utf-8");
  resp,getWriter().print("名字"+ username);
  ```




