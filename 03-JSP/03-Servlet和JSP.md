## JSP 的作用

Servlet 和 JSP 都可以生成动态页面；然而，JSP 更适合生成动态页面，因为其中的部分静态页面可以直接使用 HTML



## Servlet 的作用

接受来自 JSP 的请求，处理请求，然后跳转到 JSP 页面，把结果显示到客户端



## Servlet 与 JSP 之间的跳转方式

### 跳转方式一：

响应重定向（间接）：响应接口提供了该方法







### 跳转方式二：

请求转发（直接）：RequestDispatcher 接口定义了请求转发的方法

`forward(ServletRequest request，ServletResponse response)`

要使用 forward 方法，需要先获取

特点：

1. 客户端和浏览器只发出一次其请求
2. 服务器端响应一次请求的时候
3. 浏览器地址栏不变



## 请求属性的使用

如果需要在Servlet、JSP之间跳转时，同时把一些自定义的、或者

设置值：`setAttribute(String name, Object object)`

取值：`getAttribute(Object object)`

删除值：`removeAttribute(String name)`