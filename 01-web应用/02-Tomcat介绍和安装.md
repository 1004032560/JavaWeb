## 4、Tomcat介绍和安装

### 4.1、Tomcat 定义：

Web 应用服务器，又称为 Servlet Container（Servlet 容器）



### 4.2、Tomcat 特点：

1. 开源

2. 免费，

3. 在中小型应用开发和并发访问用户不是很多的情况下被普遍使用

4. 开发和调试 Servlet、JSP 程序的首选



### 4.3、Tomcat 官网：

`http://tomcat.apache.org`

使用 9.0 版本：`Tomcat 9.0.34 Released`



### 4.5、Tomcat 安装：

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



![05](E:\1.soft\personalNotes\JavaWeb\images\20200427\05.png)

![06](E:\1.soft\personalNotes\JavaWeb\images\20200427\06.png)



3. 测试启动是否成功，在浏览器中访问 Tomcat：`http://localhost:8080 `



![07](E:\1.soft\personalNotes\JavaWeb\images\20200427\07.png)



