## JSP 的作用

Servlet 和 JSP 都可以生成动态页面；然而，JSP 更适合生成动态页面，因为其中的部分静态页面可以直接使用 HTML



## Servlet 的作用

接受来自 JSP 的请求，处理请求，然后跳转到 JSP 页面，把结果显示到客户端



## Servlet 与 JSP 之间的跳转方式

### 跳转方式一：

响应重定向（间接）：响应接口提供了该方法 `senderRedirect(String location)`；相当于客户端重新请求 location 所在的资源 `response.sendRedirect(request.getContextPath()+"/xxx")`

特点：

1. 实际是两次 HTTP 请求

2. 服务器端在响应第一次请求的时候，让浏览器再向另外一个 URL 发出请求，从而达到转发的目的

3. 浏览器地址栏发生变化，显示的是第二次请求的地址





### 跳转方式二：

请求转发（直接）：RequestDispatcher 接口定义了请求转发的方法

`forward(ServletRequest request，ServletResponse response)`

要使用 forward 方法，需要先获取请求接口中的 RequestDispatcher 对象

特点：

1. 客户端和浏览器只发出一次请求

2. 请求转发是在服务器内部进行转发

3. 浏览器地址栏还是显示第一次请求的 URL，没有发生变化



## 请求属性的使用

如果需要在 Servlet，JSP 之间跳转时，同时把一些自定义的、或者通过数据库查询的、或者调用其他资源获得的数据传递到下一个资源时，就可以把这些数据设置为请求的属性。

请求属性可以是任意类型的对象，可以用 setAttribute 方法将对象作为属性存储到请求对象中

请求参数是用户提交请求时，自动封装到请求对象中的一些输入信息，都是 String 类型

设置值：`setAttribute(String name, Object object)`

取值：`getAttribute(Object object)`

删除值：`removeAttribute(String name)`