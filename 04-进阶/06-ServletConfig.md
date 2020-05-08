## 1、得到ServletConfig对象

通过 getServletConfig() 方法获得 ServletConfig 对象

~~~java
    //得到ServletConfig对象
    ServletConfig servletConfig = getServletConfig();
~~~



## 2、得到Servlet的name

通过 ServletConfig 的对象调用 getServletName() 方法获得 Servlet 的 name

~~~java
    //得到Servlet名称
    String servletName = servletConfig.getServletName();
    System.out.println(servletName);
~~~



## 3、得到ServletContext上下文对象

通过 ServletConfig 的对象调用 getServletContext() 方法获取上下文对象

~~~java
    //得到上下文对象
    //getServletContext().getInitParameter("name")
    ServletContext servletContext = servletConfig.getServletContext();
    System.out.println(servletContext);
~~~



## 4、得到Servlet初始化参数

通过 ServletConfig 的对象调用 getInitParameter(“name”) 方法获取初始化参数

~~~java
    //得到Servlet初始化参数
    //String initParameter = getInitParameter("name");
    String initParameter = servletConfig.getInitParameter("name");
    System.out.println(initParameter);
~~~



## 5、ServletConfig与ServletContext的区别

1. ServletConfig 是针对只有一个特定的 Servlet 的局部变量

2. ServletContext 是整个 Web application 的全局变量 ServletContext 存放在 ServletConfig 中 



