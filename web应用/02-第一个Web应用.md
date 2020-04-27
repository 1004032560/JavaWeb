## 1、Eclipse 中配置 Tomcat

Window --- preferences --- server --- runtime environments-add





## 2、编写第一个 Servlet





## 3、web.xml 中配置 Servlet

<servlet>节点

包含元素<servlet-name>及<servlet-class>,其中<servlet-name>可以使用任意标识符，<servlet-class>是Servlet类的完整类名；

<servlet-mapping>节点

包含元素<servlet-name>及<url-pattern>,其中<servlet-name>与已经定义的name对应，<url-pattern>是逻辑url，非常非常重要，访问Servlet就使用这个url-pattern



## 4、部署到 Tomcat





## 5、运行 Web 应用





## 6、Servlet 生命周期

### Servlet 家谱

二类二接口，3 + 2 方法

HttpServlet 类和 GenericServlet 类；Servlet 接口和 ServletConfig 接口。





## 7、Eclipse 常用配置