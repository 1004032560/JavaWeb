## 九大内置对象

内置对象是指在JSP中可以直接使用的对象，不需要声明，直接使用固定的名字即可。



与输入输出有关的对象：request、response、out

与属性作用域有关的对象：session、application、pageContext

与 Servlet 相关的对象：page、config

与错误处理有关的对象：exception



## 四大作用域

作用域从小到大：page、request、session、application

page 当前页面有效（页面跳转后无效）

request 同一次请求有效（请求转发后有效，重定向后无效）

session 同一次对话有效（同一个浏览器在退出关闭之前都有效）

application 全局有效（整个项目）