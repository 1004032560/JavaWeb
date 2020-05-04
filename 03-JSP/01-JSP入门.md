# 1、动态网页的执行原理

1. 容器初始化 Servlet 实例，根据请求方法，调用相应的 doXXX 方法，并初始化请求和响应对象，作为 doXXX 方法的参数使用；

2. 执行 doXXX 方法后，将响应对象中的数据流写到客户端；

3. 客户端浏览器将收到的数据进行解析，显示给用户；



## 2、JSP 的功能与特性

### JSP

JSP 是指（`Java Server Page`）Java 服务器端的页面

是 JavaEE 规范中的 Web 组件，用来编写动态页面

### JSP的特点

1. JSP 运行在服务器端，本质是 Servlet

2. JSP 文件以 `.jsp` 为后缀，在工程目录中存在 WebContent 目录下

3. JSP 文件可以直接在浏览器中访问

4. JSP 文件中的内容就是 HTML+Java 代码，静态部分使用HTML和文本即可，动态部分使用Java代码



## 3、JSP 的执行流程

1. 翻译

翻译的特点：JSP 的命名

单词.jsp 会被翻译成：`单词_jsp.java`

数字.jsp 会被翻译成：`_数字_jsp.java`

Web 服务器找到 `blank.jsp` ，对其进行翻译，生成 `blank_jsp.java` 文件，就是 Servlet



2. 编译

服务器将 `blank_jsp.java` 编译成类文件 `blank_jsp.class`，翻译和编译的过程遵守 Servlet 规范，因此说 JSP 的本质也是 Servlet

~~~java
public void _jspService(final javax.servlet.http.HttpServletRequest request, final javax.servlet.http.HttpServletResponse response)
      throws java.io.IOException, javax.servlet.ServletException {

    if (!javax.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) {
      final java.lang.String _jspx_method = request.getMethod();
      if ("OPTIONS".equals(_jspx_method)) {
        response.setHeader("Allow","GET, HEAD, POST, OPTIONS");
        return;
      }
      if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method)) {
        response.setHeader("Allow","GET, HEAD, POST, OPTIONS");
        response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSP 只允许 GET、POST 或 HEAD。Jasper 还允许 OPTIONS");
        return;
      }
    }

    final javax.servlet.jsp.PageContext pageContext;
    javax.servlet.http.HttpSession session = null;
    final javax.servlet.ServletContext application;
    final javax.servlet.ServletConfig config;
    javax.servlet.jsp.JspWriter out = null;
    final java.lang.Object page = this;
    javax.servlet.jsp.JspWriter _jspx_out = null;
    javax.servlet.jsp.PageContext _jspx_page_context = null;


    try {
      response.setContentType("text/html; charset=UTF-8");
      pageContext = _jspxFactory.getPageContext(this, request, response,
      			null, true, 8192, true);
      _jspx_page_context = pageContext;
      application = pageContext.getServletContext();
      config = pageContext.getServletConfig();
      session = pageContext.getSession();
      out = pageContext.getOut();
      _jspx_out = out;

      out.write("\r\n");
      out.write("<!DOCTYPE html PUBLIC \"-//W3C//DTD HTML 4.01 Transitional//EN\" \"http://www.w3.org/TR/html4/loose.dtd\">\r\n");
      out.write("<html>\r\n");
      out.write("<head>\r\n");
      out.write("<meta http-equiv=\"Content-Type\" content=\"text/html; charset=UTF-8\">\r\n");
      out.write("<title>Insert title here</title>\r\n");
      out.write("</head>\r\n");
      out.write("<body>\r\n");
      out.write("blank.jsp\r\n");
      out.write("</body>\r\n");
      out.write("</html>");
    } catch (java.lang.Throwable t) {
      if (!(t instanceof javax.servlet.jsp.SkipPageException)){
        out = _jspx_out;
        if (out != null && out.getBufferSize() != 0)
          try {
            if (response.isCommitted()) {
              out.flush();
            } else {
              out.clearBuffer();
            }
          } catch (java.io.IOException e) {}
        if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
        else throw new ServletException(t);
      }
    } finally {
      _jspxFactory.releasePageContext(_jspx_page_context);
    }
  }
~~~



3. 实例化

服务器实例化类 `blank_jsp.class`



4. 提供服务

调用类中的 `_jspService` 方法提供服务



### 总结

Servlet 生成动态页面比较繁琐，使用 JSP 生成动态页面比较便捷，因为其中的静态内容可以使用 HTML 生成

JSP 的本质就是 Servlet，不过服务器对 JSP 进行了翻译和编译，JSP 也就是一个 Java 类



## 4、脚本元素

脚本元素：是包含 Java 代码的元素时

语法格式：<% Java代码 %>

特点：服务器翻译脚本元素时，会将其中的 Java 代码翻译到 `_jspService` 方法中，将在浏览器中提示错误

~~~jsp
<body>
blank.jsp<br/>
<%
  System.out.println("Hello Jsp!");
%>
</body>
~~~

翻译之后

~~~java
  out.write("blank.jsp<br/>\r\n");
  System.out.println("Hello Jsp!");
  out.write("\r\n");
~~~



## 5、表达式元素

表达式元素：用来向页面输出动态内容

语法格式：<%= Java代码 %>

特点：服务器翻译表达式元素时，将把其中 Java 代码部分的返回值使用 out.write 语句输出

~~~jsp
<body>
<%=request.getRemoteAddr()%>
</body>
~~~

翻译之后

~~~java
 	out.write("<body>\r\n");
    out.print(request.getRemoteAddr());
    out.write("\r\n");
    out.write("</body>\r\n");
~~~



## 6、声明元素

声明元素：在 JSP 文件中定义类的成员变量或方法的元素

语法格式：<%! Java代码 %>

特点：声明元素被翻译到Java类中，而不是_jspService方法中；

## 7、模板元素

模板元素：指 JSP 中静态 HTML 或者 XML 内容



## 8、注释元素

在 JSP 中可以使用注释元素，有三种情况

### JSP 注释

格式：`<%-- JSP 注释 --%>`

特点：JSP的注释只有在源代码中可见，翻译时已经忽略；

### HTML 注释

格式：`<!-- HTML 注释 --> `

特点：

1. HTML注释翻译时会被翻译成out.write("<!-- HTML注释 -->\r\n"),

2. 会被返回到客户端

3. 在网页源代码能看见

4. 但是不显示到页面中

### Java 注释

格式：

1. 单行：//
2. 多行：/*   */
3. doc 文本：/**   */

特点：

1. Java 注释会翻译到.java文件中
2. 但是编译时忽略