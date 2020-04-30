# 1、动态网页的执行原理

Servlet 中生成动态页面太麻烦，大部分静态内容也需要一行一行输出，所以 JavaEE 提供了 JSP 组件



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



2. 编译

服务器将 `blank_jsp.java` 编译成类文件 `blank_jsp.class`，翻译和编译的过程遵守 Servlet 规范，因此说 JSP 的本质也是 Servlet



3. 实例化

服务器实例化类 `blank_jsp.class`



4. 提供服务

调用类中的 `_jspService` 方法提供服务



### 总结

JSP 的本质就是 Servlet，不过服务器对 JSP 进行了翻译和编译，JSP 也就是一个 Java 类









## 4、脚本元素

脚本元素：是包含 Java 代码的元素时

语法格式：<% Java代码 %>

特点：服务器翻译脚本元素时，会将其中的 Java 代码翻译到 _jspService 方法中，将在浏览器中提示错误

~~~jsp
<body>
blank.jsp<br/>
<%
  System.out.println("Hello Jsp!");
%>
</body>
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





