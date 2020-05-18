## 1、如何获取全新的PushBuilder

### 1.1、HTTP 2.0

HTTP 2.0：超文本传输 2.0 协议，是下一代 HTTP 协议

特点：使用加密技术，防止攻击

目标：改善 Web 应用程序的用户体验

Servelet 4.0主要新功能：为服务器推送全新的 API



### 1.2、Server Push

**主动推送，提高效率**

Server Push 是 HTTP/2 规范中引入的一种新技术，即服务端在没有被客户端明确的询问下，抢先地 ”推送“一些网站资源给客户端（浏览器），该特性可以极大的改善页面访问效果。

使用 Server Push 技术之后，当 WEB 浏览器请求 /index.html 之后，WEB 服务端会直接将需要推送的资源一并发给WEB浏览器，而不需要WEB浏览器依次进行请求，这减少了WEB浏览器进行请求所消耗的时间。

4.0 是通过 PushBulider 接口实现服务器的推送

4.0 全新的 Servlet 映射，实现映射

HttpServletMapping 接口支持运行时发现映射



### 1.3、HttpServletMapping接口

1. Servlet 4.0 的全新 servlet 映射发现 API 使服务器能够对 URL（可调用 servlet）执行运行时检查。例如，对 1.txt, /brain 和 /brain/1.txt 的请求将通过 URL 模式 /brain/* 和 *.txt 激活 servlet。

2. HttpServletMapping 接口支持运行时发现 servlet 的映射 URL。可以在 HttpServletRequest 实例上调用 getHttpServletMapping()，获取接口的实例。



## 2、Servlet 4.0 的细微变化

1. Trailer 响应标头支持发送方在分块消息的末尾包含额外字段。这用于提供在发送消息主体时可能会动态生成的元数据，例如，消息完整性检查、数字签名或后期处理状态。

2. Servlet 4.0 添加了 GenericFilter 和 HttpFilter 抽象类，这些抽象类通过最低限度地实现生命周期方法 init() 和 destroy()，简化了编写过滤器。

3. Servlet 4.0 还集成了全新的 HTTP Trailer，支持发送方在分块消息的末尾包含额外的字段。

4. ServletContext 接口采用了一些新方法：

   * addJspFile() 可将带有给定 JSP 文件的 servlet 添加到 servlet 上下文中。

   * getSessionTimeout() 和 setSessionTimeout() 可提供对会话超时的访问权限。

   * getRequestCharacterEncoding() 和 setRequestCharacterEncoding() 可为当前  的servlet 上下文提供访问权限，并改变默认的请求字符编码。

5. HttpServletRequest 接口上的 isRequestedSessionIdFromUrl() 方法已被弃用。

6. 由于升级到 Java SE 8，默认方法已被添加到侦听器接口中。