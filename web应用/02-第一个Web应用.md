## 1、Eclipse 中配置 Tomcat

1. 在 Eclipse 中找到`Window --- preferences --- server --- runtime environments-add`
2. 选择 `Tomcat9.0` 版本，点击 next 按钮





## 2、Eclipse 中配置服务器

1. 在 Eclipse 中找到`Window --- Show View --- Server`
2. 底部工具栏中就会出现 Service





## 2、编写第一个 Servlet





## 3、web.xml 中配置 Servlet

### `<servlet>`节点

包含元素 `<servlet-name>` 及 `<servlet-class>`

`<servlet-name>` 可以使用任意标识符，与 `<servlet-mapping>` 节点相关联

`<servlet-class>` 是Servlet类的完整类名；

### `<servlet-mapping>`节点

包含元素 `<servlet-name>` 及 `<url-pattern>`

其中 `<servlet-name>` 与已经定义的name对应，

`<url-pattern>` 是逻辑 URL，非常非常重要，访问 Servlet 就使用这个 url-pattern



## 4、部署到 Tomcat





## 5、运行 Web 应用





## 6、Servlet 生命周期

### Servlet 家谱

二类二接口，3 + 2 方法

HttpServlet 类和 GenericServlet 类；Servlet 接口和 ServletConfig 接口。





## 7、Eclipse 常用配置