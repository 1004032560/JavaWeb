## 1、C/S、B/S与RIA

### C/S 结构：

是 Client/Server（客户机/服务器）的简称，桌面应用程序（例如：QQ）；

又称胖客户端，需要在电脑上安装特定的客户端软件。

### B/S 结构：

是 Browser/Server（浏览器/服务器）的简称，浏览器上访问网页（例如：访问百度）；

又称瘦客户端，不需要在电脑上安装特定的软件，只需要安装一个浏览器就可以运行。

### C/S 和 B/S 的区别：

C/S 需要安装客户端，但是操作便捷

B/S 不需要安装客户端，用户体验不如 C/S 不够好，安全性也比 C/S 低

### RIA：

是（Rich Internet Application）富客户端网络应用；

基于 B/S 结构，在浏览器中实现与客户端类似的体验（局部刷新、可拖拽等）

## 2、web

### web 站点：

web 站点即 Web Site 也称为 Web 网站

某公司用来宣传的网站也就是 Web 站点，也就是用户用来浏览信息，该站点不提供服务（静态网站）

### web 应用：

web 应用被称为 Web Application

通过浏览器访问的应用程序，为用户提供相关的服务（动态网站）

### HTTP 服务器：

定义：HTTP 服务器也称为 Web 服务器，提供网上信息浏览服务

例如：Apache、Nginx、IIS（微软）

特点：使用浏览器访问 Web 站点或者 Web 应用，必须通过 HTTP 服务器

### Web 应用服务器：

定义：能够运行服务器上的应用程序，并将结果返回给客户端浏览器的软件

例如：Tomcat 就是 Web 应用服务器

特点：兼具 HTTP 服务器的一部分功能

## 3、开发 Web 应用的核心技术

### CGI：

通用网关接口（Common Gateway Interface）

Web 应用服务器提供的信息服务的标准接口，目前使用较少

### .NET：

是微软公司的企业应用框架，例如：Asp.net、Ado.net等

是用于中小企业，不能跨平台具有局限性

### PHP：

相对易学的 Web 开发技术，在互联网小型应用中使用广泛

### JavaEE：

JavaEE 是 Oracle 公司的企业应用框架，在大型企业公司应用广泛

例如：Servlet、JSP 是 Web 开发组件

## 4、Tomcat介绍和安装

### Tomcat 定义：

Web 应用服务器，又称为 Servlet Container（Servlet 容器）

### Tomcat 特点：

1. 开源

2. 免费，

3. 在中小型应用开发和并发访问用户不是很多的情况下被普遍使用

4. 开发和调试 Servlet、JSP 程序的首选

### Tomcat 官网：

 `http://tomcat.apache.org`

使用 9.0 版本：`Tomcat 9.0.34 Released`

### Tomcat 安装：

1. 进入官网

![01](E:\1.soft\personalNotes\JavaWeb\images\20200427\01.png)

2. 找到最新的版本

![02](E:\1.soft\personalNotes\JavaWeb\images\20200427\02.png)

3. 下载对应操作系统的压缩包

4. 下载本地之后解压（解压时路径中不要含中文）

![03](E:\1.soft\personalNotes\JavaWeb\images\20200427\03.png)

### Tomcat 目录结构：

![04](E:\1.soft\personalNotes\JavaWeb\images\20200427\04.png)

bin：用于存放 Tomcat 启动（startup.bat）和停止（startdown.bat）等批处理脚本和 shell 脚本

conf：Tomcat 相关的配置文件

lib：Tomcat 服务器的依赖库目录，主要存放 Tomcat 运行环境依赖的 jar 包

log：Tomcat 默认的日志存放目录

temp：Tomcat 运行时产生的临时文件

webapps：Tomcat 默认的 Web 部署目录

work：jsp 代码编译后生成的 class 目录

### 启动 Tomcat：

1. 启动前必须保证已经配置好 JDK 的环境变量

2. 到 Tomcat 的 bin 目录下点击 `startup.bat` 启动
3. 测试启动是否成功，在浏览器中访问 Tomcat：`http://localhost:8080 `

## 5、常见的 Servlet 容器简介

常见的 Servlet 容器：JBoss、Resin、GlassFish 4、Tomcat

补充：（付费，用于大型公司，电信产业）Weblogic、Websphere

## 6、Servlet 概念及功能

### Servlet 定义：

JavaEE 规范中的 Web 开发组件

### Servlet 特点：

1. 运行在服务器端
2. 需要 Servlet 容器的支持（例如：Tomcat）
3. Servlet 是一个 Java 类，遵守一定的 Java 开发规范（例如：继承 HttpServlet）
4. 通过浏览器访问 Servlet，Servlet 返回给浏览器动态页面