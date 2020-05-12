## 1、MVC分页

当数据表的记录多的时候，页面一页显示不下，会用到分页技术。

规定页面显示多少条，没显示的会在下一页或者后面的页面显示

首页   上一页   下一页   尾页



## 2、实现分页步骤

1. JSP 传递请求参数当前页 curPage
2. Servlet 接收请求参数 curPage

3. 分页中需要用到的七大变量

~~~java
//获取到JSP传递的请求参数，即当前页数
String curPage = (String)request.getParameter("curPage");
//1.判断当前参数是否为null,不是null则将其转换为int类型,否则设置为1
int currentPage = curPage==null ? 1 : Integer.parseInt(curPage);
//2.pageSize 表示每页显示的条数，自己指定页面显示的条数
int pageSize = 2;
//3.count 总记录数，从数据库中获取总记录数
int count = peopleService.getCount();
//4.pageCount 总页数；总记录数%每页显示的条数==0，
//则：总页数=总记录数/每页显示的条数
//否则：总页数=总记录数/每页显示的条数+1
int pageCount = count%pageSize==0 ? count/pageSize : count/pageSize+1;
//5.prevPage 上一页
int prevPage = currentPage==1 ? 1 : currentPage-1;
//6.nextPage 下一页
int nextPage = currentPage==pageCount ? pageCount : currentPage+1;
//7.startPage 起始页
int startRecord = (currentPage-1)*pageSize;
~~~

4. 从数据库中分页查找，需要传入起始页和每个页面显示的条数

~~~java
List list=service.list(startRecord,pageSize);
~~~

5. 将获取的数据添加到请求域中
6. 请求转发到 list.jsp 中

7. 在 JSP 中获取请求对象中的数据，展示到页面

~~~jsp
<td colspan="3">
	<button onclick="paging(1)">首页</button>
	<button onclick="paging(<%=request.getAttribute("prevPage")%>)">上一页</button>
	<button onclick="paging(<%=request.getAttribute("nextPage")%>)">下一页</button>
	<button onclick="paging(<%=request.getAttribute("pageCount")%>)">尾页</button>
</td>
~~~

`Servlet`

~~~java
private void list(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //接收请求参数curPage
    String curPage = request.getParameter("curPage");
    System.out.println(curPage);
    //判断curPage==null
    int currentPage=curPage==null?1:Integer.parseInt(curPage);
    System.out.println(currentPage);
    //b)pageSize每页显示的条数
    int pageSize=2;
    System.out.println(pageSize);
    //count总记录数:数据库表一共有多少条记录
    int count=studentService.getCount();
    System.out.println(count);
    //总页数:pageCount
    int pageCount=count%pageSize==0?count/pageSize:count/pageSize+1;
    System.out.println(pageCount);
    //上一页prevPage
    int prevPage=currentPage==1?1:currentPage-1;
    System.out.println("prevPage="+prevPage);
    //下一页nextPage
    int nextPage=currentPage==pageCount?pageCount:currentPage+1;
    System.out.println("nextPage="+nextPage);
    //起始记录
    int startRecord=(currentPage-1)*pageSize;
    System.out.println("startRecord="+startRecord);
    //得到分页列表数据
    List<Student> list = studentService.list(startRecord, pageSize);
    for (Student student : list) {
        System.out.println(student);
    }
    //分页列表数据放到请求作用域里
    request.setAttribute("list", list);
    request.setAttribute("prevPage", prevPage);
    request.setAttribute("nextPage", nextPage);
    request.setAttribute("pageCount", pageCount);
    //请求转发
    request.getRequestDispatcher("/list.jsp").forward(request, response);
}
~~~

`list.jsp`

~~~jsp
<%@page import="com.tjetc.domain.Student"%>
<%@page import="java.util.List"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
  function paging(curPage){
	  alert(curPage);
	  location.href="/0512-c3p0/StudentServlet/list?curPage="+curPage;
  }
</script>
</head>
<body>
 <table>
 <tr>
 <th>序号</th>
 <th>姓名</th>
 <th>年龄</th>
 </tr>
 <%
   List<Student> list=(List<Student>)request.getAttribute("list");
 if(list!=null){
   for(Student student:list){
%>
	<tr>
	  <td><%=student.getId()%></td>
	  <td><%=student.getName()%></td>
	  <td><%=student.getAge()%></td>
	</tr>   
<%	   
   }
 }
 %>
 <tr>
   <td colspan="3">
     <button onclick="paging(1)">首页</button>
     <button onclick="paging(<%=request.getAttribute("prevPage")%>)">上一页</button>
     <button onclick="paging(<%=request.getAttribute("nextPage")%>)">下一页</button>
     <button onclick="paging(<%=request.getAttribute("pageCount")%>)">尾页</button>
   </td>
 </tr>
 
 </table>
</body>
</html>
~~~

