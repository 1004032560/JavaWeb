## 1、Eclipse 中配置 Tomcat

1. 在 Eclipse 中找到`Window --- preferences --- server --- runtime environments-add`
2. 选择 `Tomcat9.0` 版本，点击 next 按钮



## 2、Eclipse 中配置服务器

1. 在 Eclipse 中找到 `Window --- Show View --- Server`
2. 底部工具栏中就会出现 Service

3. 点击 `No servers are available. create a new server...`
4. 选择 `Tomcat 9.0` 对应的下载的版本
5. 点击 `Finish` 完成即可



## 3、创建 Web 应用

1. 创建一个 `Dynamic Web Project`

   src：目录存放的是 Java 源代码文件，也就是 Servlet 源码

   WebContent：目录下存放的是 JSP、HTML 以及图片文件

   WebContent 下的 Web-INF 中的 `lib` 文件夹存放的是导入第三方的 `jar` 包；`web.xml` 则是 Web 应用的配置文件，Servlet 的配置就在这



2. 在 `src` 目录下，按照创建 Java 类的方式，选择 Servlet，创建一个 Servlet 类

~~~java
public class HelloServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

    public HelloServlet() {
      super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.getWriter().append("Served at: Hello Servlet!").append(request.getContextPath());
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}

}
~~~



3. 在 `web.xml` 文件中会自动配置 servlet 节点

~~~xml
<servlet>
	<servlet-name>HelloServlet</servlet-name>
	<servlet-class>com.looper.servlet.HelloServlet</servlet-class>
</servlet>
<servlet-mapping>
	<servlet-name>HelloServlet</servlet-name>
	<url-pattern>/HelloServlet</url-pattern>
</servlet-mapping>
~~~

`<servlet>` 节点中：

包含元素 `<servlet-name>` 及 `<servlet-class>`

`<servlet-name>` 可以使用任意标识符，与 `<servlet-mapping>` 节点相关联

`<servlet-class>` 是Servlet类的完整类名

`<servlet-mapping>` 节点中：

包含元素 `<servlet-name>` 及 `<url-pattern>`

其中 `<servlet-name>` 与已经 `<servlet>` 节点中的 `<servlet-name>` 对应

`<url-pattern>` 是逻辑 URL，非常非常重要，访问 Servlet 就使用这个 url-pattern，启动 Tomcat 之后，在浏览器，的 URL 项目工程路径后面加上 `<url-pattern>` 中的路径即可访问该 Servlet



4. 启动（部署） Tomcat：右键选中工程 --> Run As --> Run on Server --> Finish
5. 运行 Web 应用，在地址栏中输入：`localhost:8080/firstServlet/HelloServlet` 即可访问当前 Servlet

