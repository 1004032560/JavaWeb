## 1、Session 简介

Session：是会话跟踪的另一种实现手段

Session：是存储在服务器上的对象，该对象由服务器创建并维护（每种服务器）；

Session 特点：

1. 服务器为客户端和服务器的每次会话创建一个并维护一个 Session 对象
2. 每个服务器对 Session 的创建和维护的底层实现都不同

Tomcat 如何维护 Session 的 ID：

Tomcat 使用 Cookie 来维护 Session 对象的 ID 值；该 Cookie 的名字为 JSESSIONID





## 2、Session 使用方法





`request.getSession()`：获取当前请求相关的 Session 对象，如果该对象存在则返回该对象的值，如果不存在则创建一个新的 Session 对象。





1. Session 可以保存任何对象
2. Session 保存的状态信息，如：登录信息（用户信息）或者其他的状态信息
3. Session 可以跨页面，跨请求访问；因此 Session 可以使用重定向
4. 不能无限制的存储，随着越来越多的用户登录
5. 每个 Session 持续的时间是用户访问的时间加上不活动的时间
6. 实现自定义 Session 的基本步骤













## 3、HttpSession 对象的获取





## 4、Session 常用方法

添加设置属性值：`setAttribute(String name, Object object)`

获取属性值：`getAttribute(String name)`，该返回值为 Object 类型

删除属性值：`removeAttribute(String name)`



## 5、Session 失效的方法

### 为什么要让 Session 失效：

1. 会话对象时存储在服务器端的对象，一直存在需要占用一定的服务器资源
2. 会话中往往保存着用户的一些数据，如果一直有效，存在一定安全隐患



### Session 失效方法：

1. 服务器都有默认的失效时间，Tomcat 中默认30分钟自动失效；



2. 在 XML 中配置使 Session 失效（单位：分钟）：

~~~xml
<session-config>
	<session-timeout>50</session-timeout>
</session-config>
~~~



3. 通过调用 HttpSession 接口中的方法使 Session 失效：

`invalidate()`：会立刻销毁 Session 对象

~~~java
//设置 Session 立即失效
session.invalidate();
~~~

`setMaxInvalidate(int interval)`：设置最大销毁时间（单位：秒），超过时间之后，会立刻销毁 Session 对象

~~~java
//设置 Session 立即失效
session.invalidate(24*3600);
~~~