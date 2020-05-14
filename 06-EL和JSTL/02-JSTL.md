## 1、JSTL

JSTL：（Jsp Standard Tag Library）JSP 标准标签库

JSTL 作用：

1. 用 Java 类实现动态功能
2. 简化 JSP 文件，不用写大量的 Java 脚本
3. 标签可以重复使用，利于维护

JSTL 包含：标签库处理器类 + tld 文件（标签描述符文件）



## 2、JSTL结构

标签处理器类

tld 文件：（Tag Library Descriptor）标签库描述文件

c.tld ：核心

fn.tld：函数



## 3、tld文件的格式

1. taglib 标签下的 uri：tld 文件的唯一标识

2. taglib 标签下的 tag 标签：
   * tag 标签下的 name 标签：表示 tag 标签的名称
   * tag 标签下的 tag-class 标签：表示 tag 标签的名称
   * tag 标签下的 body 标签：表示 tag 标签体的内容
   * tag 标签下的 attribute 标签：表示 tag 标签的属性
     * name：属性的名称
     * required：属性是否可以省略，true 表示可以省略，false 表示不可以省略
     * rtexprvalue：是否使用动态的表达式，true 表示可以使用，false 表示不可以使用



## 4、使用JSTL标签的步骤

1. 导入 `jstl1.2.jar`

2. `<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>`

3. `<c:标签名 属性名="值"/>`
4. `<c:out value="${a}"></c:out>`



## 5、属性相关的标签

### 5.1、set标签

1. 语法：

`<c:set var="属性名" value="属性值" scope="page|request|session|application"/>`

相当于：`<% request.setAttribute("name", "ZhangSan"); %>`

2. 作用：

* 向作用域添加属性名和值

scope属性可以省略：

* 指定 scope，会向指定的作用域添加属性名和值

* 如果省略 scope，默认会向 page 作用域添加属性和值

### 5.2、remove标签

1. 语法：

`<c:romove var="属性名" scope="page|request|session|application"/>`

2. 作用：

* 从作用域删除属性

scope属性可以省略：

* 指定 scope，会从指定的作用域删除属性

* 如果省略 scope，会从 4 个作用域从小到大依次寻找，找到就删除，直到全部删除为止



### 5.3、out标签

语法：`<c:out value="${ requestScope.username }"></c:out><br>`

输出标签，几乎不用，用 EL 表达式



前三个总案例：

~~~jsp
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<%-- <% request.setAttribute("name", "ZhangSan"); %> --%>
<c:set var="name" value="ZhangSan" scope="request"></c:set>

<c:set var="username" value="LiSi" ></c:set>

<c:out value="${ requestScope.name }"></c:out><br>

<c:out value="${ requestScope.username }"></c:out><br>
<c:out value="${ sessionScope.username }"></c:out><br>
<c:out value="${ applicationScope.username }"></c:out><br>
<c:out value="${ pageScope.username }"></c:out><br>
~~~



### 5.4、if标签

​    1.语法:

`<c:if test="条件表达式"/>`

​	`if标签体`

`</c:if>`

2. 作用：

* 当条件表达式是 true，则执行 if 标签体

* 否则，就不执行 if 标签体

3. 例子：

~~~jsp
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<c:if test="${empty a}">
	${ requestScope.name }<br>
</c:if>
~~~





### 5.5、hoose/when/otherwise/标签

语法：

~~~jsp
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<c:set var="score" value="${ param.score }"></c:set>

<c:choose>
	<c:when test="${empty score}">请输入成绩：${ score }</c:when>
	<c:when test="${  score < 0 || score > 100 }">分数错误：${ score }</c:when>
	<c:when test="${score>=90}">A级！成绩为：${ score }</c:when>
	<c:when test="${score>=80}">B级！成绩为：${ score }</c:when>
 	<c:when test="${score>=70}">C级！成绩为：${ score }</c:when>
 	<c:when test="${score>=60}">D级！成绩为：${ score }</c:when>
 	<c:otherwise>E级</c:otherwise>
</c:choose>
~~~



### 5.6、forEach标签

1. 语法：`<c:forEach items="集合变量名" var="集合变量名"> ${临时变量} </c:forEach>`

2. 说明：
   * items：${集合变量名} 取得存储在作用域里的集合值，可以对集合进行遍历
   * 对于遍历的每一项，放到页面作用域的属性名为临时变量名的属性中
   * 可以通过 ${集合变量名} 从页面作用域中取得当前循环遍历到的值，显示在页面上
   * begin：表示循环从哪个索引开始取数据，索引默认从 0 开始
   * end：循环到哪个索引结束，索引默认从 0 开始
   * step：步长，每次走几步，默认是 1 ，可以设置多个
   * varStatus：状态变量，包含 5 个属性
     * index：代表迭代的索引，从 0 开始
     * count：代表迭代的次数，从 1 开始
     * first：当前是否是第一项，是则 true，否则 false
     * last：当前是否是最后一项，是则 true，否则是 false
     * current：当前项

3. 例子：

~~~jsp
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<%
   List<String> list=new ArrayList<>();
   list.add("aaa");
   list.add("bbb");
   list.add("ccc");
   list.add("ddd");
   list.add("eee");
   list.add("fff");
   list.add("ggg");
   list.add("hhh");
   request.setAttribute("list", list);
%>
<c:forEach items="${list}" var="s" begin="2" end="6" step="2" varStatus="st">
	当前值的下标:${ st.index };当前值:${pageScope.s };第${st.count }次;当前是否为第一项:${st.first };当前项:${st.current }<br/>
</c:forEach>
~~~





### 5.7、forTokens标签

1. 语法

`<c:forTokens items="${变量名}" delims="分隔符" var="临时变量名">`

​	`${临时变量名}`

`</c:forTokens>`

2. 说明:

* items 放的是字符串变量名，也可以直接写字符串，可以从四大作用域之一取得，即可以使用 EL 表达式， ${存储在作用域的字符串变量名}

* var = ”临时变量名”，forTokens 标签处理器，会循环遍历用分隔符分割出来的数组集合，对于遍历到的当前项会存储到 pageContext 作用域的属性名为是 var 的临时变量名中，值是遍历到的当前项

* 标签体取得就是临时变量名所存储的遍历到的当前项值

3. 例子：

~~~jsp
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

request.setAttribute("s","a,b,c,d");

<c:forTokens items="${s}" delims="," var="token">
	${token}
</c:forTokens>
~~~



### 5.8、formatDate标签

1. 语法：

`<fmt:formatDate value="${d}" pattern="yyyy-MM-dd HH:mm:ss">`

2. 说明：

   `<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>`

   pattern 使用 Java 的日期时间模式字符串

3. 例子

~~~jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>

<%
Date date = new Date();
request.setAttribute("date", date);
%>

<fmt:formatDate value="${date }" pattern="yyyy-MM-dd HH:mm:ss"/>
~~~



### 5.9、fn:contains标签

1. 语法：

`${ fn:函数名(作用域里的变量名,值) }`

2. 说明：

   封装了字符串,函数名与字符串的方法名一样

   `<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>`

3. 例子：

~~~jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>

<% request.setAttribute("hobbies", "吃,乐"); %>

<!-- 复选框 -->
爱好：
<input type="checkbox" name="hobbies" value="吃" ${fn:contains(hobbies,"吃")?"checked='checked'":"" }>吃
<input type="checkbox" name="hobbies" value="喝" ${fn:contains(hobbies,"喝")?"checked='checked'":"" }>喝
<input type="checkbox" name="hobbies" value="玩" ${fn:contains(hobbies,"玩")?"checked='checked'":"" }>玩
<input type="checkbox" name="hobbies" value="乐" ${fn:contains(hobbies,"乐")?"checked='checked'":"" }>乐
~~~















