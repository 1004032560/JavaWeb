## 5、常见的 Servlet 容器简介

**常见的 Servlet 容器：JBoss、Resin、GlassFish 4、Tomcat**

**补充：（付费，用于大型公司，电信产业）Weblogic、Websphere**



## 6、Servlet 概念及功能

### Servlet 定义：

JavaEE 规范中的 Web 开发组件

### Servlet 特点：

1. 运行在服务器端
2. 需要 Servlet 容器的支持（例如：Tomcat）
3. Servlet 是一个 Java 类，遵守一定的 Java 开发规范（例如：继承 HttpServlet）
4. 通过浏览器访问 Servlet，Servlet 返回给浏览器动态页面





## 6、Servlet 特点

### 6.1、Servlet家谱

**二类二接口，3 + 2 方法**

HttpServlet 类和 GenericServlet 类；Servlet 接口和 ServletConfig 接口。

Servlet 接口的三个方法：init(参数)、service、destroy

ServletConfig 接口的两个方法：getInitParameter、getServletContext



### 6.2、Servlet生命周期

当用户第一次从浏览器请求访问一个 Servlet 类（HelloServlet 类）的时候，HelloServlet 类的生命周期就开始了

1. Tomcat 调用 HelloServlet 构造方法实例化，创建该类的对象
2. Tomcat 调用 Java EE API 中的初始化方法，先调用有参的 Init 方法，再调用无参的 init 方法，进行初始化

3. 初始化成功之后，Tomcat 调用 service 方法，通过判断请求的方式，调用相应的 doXXX 方法，例如：doPost、doGet 等方法
4. 相应的 doXXX 方法处理完成返回结果之后，本次请求提供服务结束
5. Tomcat 根据使用情况，在适当的时机销毁 Servlet 对象，销毁前调用 destroy 方法

~~~java
public class HelloServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

    public HelloServlet() {
      System.out.println("HelloServlet()构造方法...");    
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("doGet()方法...");
		response.getWriter().append("Served at: Hello Servlet!").append(request.getContextPath());
	}

	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		System.out.println("service()方法...");
		super.service(req, resp);
	}

	@Override
	public void init(ServletConfig config) throws ServletException {
		System.out.println("init(ServletConfig config)有参数方法...");
		super.init(config);
	}

	@Override
	public void init() throws ServletException {
		System.out.println("init()无参数方法...");
		super.init();
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}

	@Override
	public void destroy() {
		System.out.println("destroy()方法...");
	}
}
~~~

浏览器向服务器请求了两次之后的结果：

~~~java
HelloServlet()构造方法...
init(ServletConfig config)有参数方法...
init()无参数方法...
service()方法...
doGet()方法...
service()方法...
doGet()方法...
destroy()方法...
~~~

