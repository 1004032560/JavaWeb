## 1、Servlet 线程特性

Web 应用服务器为每个客户端的链接启动一个线程来服务





## 2、请求和响应接口

Web 应用基于 HTTP 协议，HTTP 协议基于请求和响应模型

### 请求数据：

通过浏览器给服务器的所有数据称为请求数据

### 响应数据：

通过服务器给客户端的所有数据称为响应数据

### 请求接口和响应接口：

**封装和操作请求数据和响应数据的是请求接口和响应接口**

`javax.servlet.http.HttpServletRequest` 接口继承 `javax.servlet.ServletRequest`

`javax.servlet.http.HttpServletResponse` 接口继承 `javax.servlet.ServletResponse`

### doXXX 方法

服务器会创建请求对象和响应对象传递给 doXXX 中，doXXX 可以使用请求对象和响应对象





## 3、利用Servlet对客户端不同方式请求作出动态响应

### 客户端访问服务器的三种方式：

1. 直接从地址栏输入 URL 访问
2. 在网页中点击超链接访问
3. 在网页中通过表单提交访问

### 结论

1、直接使用URL访问，是GET方式，调用doGet方法；

2、超级链接访问，是GET方式，调用doGet方法；

3、表单提交访问，取决form的method属性的值，默认是get，指定为post时，调用doPost方法；





## 4、Servlet 获取请求参数

Servlet 中获取普通请求不同名或同名的参数（name1=value1&name2=value2&...）的方法



客户端向服务器 Servlet 传递请求参数的方式有两种

1. 在 URL 中添加内容：`url?name1=value1&name2=value2`
2. form 表单中 `<input/>` 标签中 `<select>` 标签等传递请求参数



服务器会将请求参数封装到请求对象当中





## 5、Servlet 初始化参数



Servlet 的初始化参数只能在当前的 Servlet 中使用

## 6、全局参数

在应用下的所有的 Servlet 都能过使用的参数，叫做全局参数

所有的 Servlet 都可以使用的参数



## 7、Servlet 加载启动选项





## 8、Servlet 配置中通配符*的用法



只要是





## 9、首页和错误页面的配置

### 首页配置

`web.xml` 中在 `<welcome-file-list>` 节点下的子节点中 `<welcome-file>` 配置指定页面为首页

### 错误页面配置

错误码



异常类型

~~~xml
<error-page>
	<exception-type>java.lang.NullPointerException</exception-type>
<location>/exception.html</location>
~~~





