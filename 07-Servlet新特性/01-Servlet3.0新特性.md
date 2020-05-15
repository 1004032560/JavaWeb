## 1、Servlet3.0新特性



## 1.1、非阻塞

#### 1.1.1、非阻塞特性：

接收到请求之后，**启动一个异步线程处理请求**，客户端可以继续请求这个 Servlet，而不必等待上一次请求返回。



#### 1.1.2、配置非阻塞特性：

1. 在 web.xml 中配置 `<async-supported>true<async-supported>`

2. 注解配置：`@WebServlet(asyncSupported = true)`

~~~java
@WebServlet(value = "/PrintServlet", asyncSupported = true)
public class PrintServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

    public PrintServlet() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//设置响应的内容类型
	    response.setContentType("text/html;charset=utf-8");
	    //获得输出流
	    PrintWriter out=response.getWriter();
	  out.println(Thread.currentThread().getName()+": Hello，我是PrintServlet,马上要进入死循环打印了！");
	    out.close();
	    while(true){
	      System.out.println("正在打印，请稍后......");
	    }
	}
}
~~~





## 1.2、注解

注解有 5 中类型

`@WebServlet`

`@WebInitParam`

`@WebFilter`

`@Weblistener`

`@MultpartConfig`

### 1.2.1、@WebServlet

`@WebServlet` 作用：对 Servlet 进行配置



#### 必选属性：

value 或者 urlPatterns，这两个的值是一样的，而且代表的含义也是一样的

urlPatterns 属性等价于 web.xml 配置文件中的 `<url-pattern>` 标签

value 等价于 urlPatterns 属性

注意：value 和 urlPatterns 不能同时设置，只能使用其中一个，同时设置就会报错

~~~java
@WebServlet(value = "/PrintServlet")
@WebServlet(value = {"/HelloServlet","/abc"} )
@WebServlet(value = {"/HelloServlet","/abc"}, value = "/PrintServlet")  //会报错
~~~



#### 可选属性：

1. name：等价于 web.xml 配置文件中的 `<servlet-name>` 标签

如果不指定 name：则默认值为 Servlet 的类全路名（包名 + 类名）

如果指定了 name：则 Servlet 的名称就是 name 的值

~~~java
//配置Servlet名称
@WebServlet(value = "/HelloServlet", name = "HelloServlet" )
//获取Servlet名称
String servletName = getServletName();
~~~



2. loadOnStartup：等价于 web.xml 配置文件中的 `<load-on-start-up>` 标签

服务器启动加载 Servlet 的顺序，数字越小，启动顺序越早

~~~java
@WebServlet(value = "/HelloServlet",loadOnStartup = 3)
~~~



3. initParams：等价于 web.xml 配置文件中的 `<init-param>` 标签

4. asyncSupported：等价于 web.xml 配置文件中的 `<async-supported>` 标签

5. description：等价于 web.xml 配置文件中的 `<description>` 标签

6. displayName：等价于 web.xml 配置文件中的 `<display-name>` 标签



### 1.2.2、@WebInitParam

`@WebInitParam`：配置初始化参数



~~~java
//配置初始化参数
@WebServlet(value = "/HelloServlet",
			initParams = {@WebInitParam(name="username",value = "looper")}
		)
//获取初始化参数
String username = getServletConfig().getInitParameter("username");
~~~



### 1.2.3、@WebFilter

`@WebFilter`：配置过滤器



#### 必选属性：

在 value、urlPattern、servletNames 三个中至少包含一个

urlPatterns：属性等价于 web.xml 配置文件中的 `<url-pattern>` 标签

value：等价于 urlPatterns 属性；并且 value 和 urlPattern 只能有一个

servletNames：指定该过滤器将应用的范围



#### 可选属性：

1. filterName：等价于 web.xml 配置文件中的 `<filter-name>` 标签

~~~java
//配置filterName
@WebFilter(servletNames = "HelloServlet",filterName = "FilterName")
//获取值
public void init(FilterConfig fConfig) throws ServletException {
	System.out.println(fConfig.getFilterName());
}
~~~



2. initParams：等价于 web.xml 配置文件中的 `<init-param>` 标签

~~~java
//配置initParams
@WebFilter(servletNames = "HelloServlet"s,
			initParams = {@WebInitParam(name = "name",value = "looperFilter")}
		)
//获取initParams的值
public void init(FilterConfig fConfig) throws ServletException {
	System.out.println(fConfig.getInitParameter("name"));
}
~~~



3. dispatcherTypes：过滤器的转发模式，取值包括：ASYN（异步）、ERROR（错误）、FOREARD（请求转发）、INCLUDE（包含）、REQUEST（请求）

4. asyncSupported：等价于 web.xml 配置文件中的 `<async-supported>` 标签

5. description：等价于 web.xml 配置文件中的 `<description>` 标签

6. displayName：等价于 web.xml 配置文件中的 `<display-name>` 标签



### 1.2.4、@WebListener

`@WebListener`：配置监听器

此注解是用来声明监听器，它主要的属性只有一个：

value：这个属性表示的是监听器的描述信息，整个配置可以简写成`@WebListener("XXX")`



### 1.2.5、@MultpartConfig

在 Servlet 设置 `@MultpartConfig` 表示：对文件上传支持

 



## 1.3、文件上传

在 Servlet 设置 `@MultpartConfig` 表示：对文件上传支持

1. location：存放路径

2. maxFileSize：上传文件的最大尺寸

3. maxRequestSize：请求的最大尺寸

4. fileSizeThreshold：当内容超过该值的时候，内容就会被写到文件

~~~java
@MultipartConfig(location = "E://aaa", maxFileSize = 3, maxRequestSize = 3, fileSizeThreshold = 2)
~~~



实现文件上传例子：

`add.jsp` 通过表单提交，上传文件

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<base href="${pageContext.request.contextPath }/">
</head>
<body>
<form action="UploadServlet" method="post" enctype="multipart/form-data">
	姓名：<input type="text" name="name"><br>
	照片：<input type="file" name="photo"><br>
	<input type="submit" value="提交">
</form>
</body>
</html>
~~~



`UploadServlet` 类实现对文件的存储

~~~java
@WebServlet("/UploadServlet")
@MultipartConfig(location = "E://aaa", maxFileSize = 3, maxRequestSize = 3, fileSizeThreshold = 2)
public class UploadServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public UploadServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request,
HttpServletResponse response) throws ServletException, IOException {
		//设置编码
		request.setCharacterEncoding("UTF-8");
		//获取值
		String name = request.getParameter("name");
		//处理上传
		Part part = request.getPart("photo");
		//判断是否为空
		if (part!=null&&part.getSize()>0) {
			//取得上传的文件名
			String fileName = part.getSubmittedFileName();
			//上传文件的存放路径
			String realPath = request.getServletContext().getRealPath("/upload/");
			System.out.println(realPath);
			//创建file对象
			File dir = new File(realPath);
			//判断/upload是否存在
			if (!dir.exists()) {
    			dir.mkdirs();
			}
			part.write(realPath+"/"+fileName);
			response.getWriter().print("upload OK.....");
			System.out.println("upload OK.....");
        }
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}
}
~~~

