## 1、forward带来的重复提交











## 2、解决重复提交

1. JSP 中设置 session 的值

~~~jsp
<%
	session.setAttribute("token", System.nanoTime()+"");
%>
~~~

2. JSP 的 form 表单中设置隐藏域的值

~~~jsp
<input type="hidden" name="token" value="<%= session.getAttribute("token") %>">
~~~

3. Servlet 中取出 session 的值和 form 表单中隐藏域 hidden 的值

~~~java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    System.out.println("提交成功！");
    //获取请求参数hidden中的值
    String tookenRequest = request.getParameter("token");
    //获取session的值
    String tookenSession = (String) request.getSession().getAttribute("token");

    if (tookenRequest==null || tookenSession==null || !tookenRequest.equals(tookenSession)) {
        response.getWriter().print("<h1>you are repaet submit</h1>");
    }else {
        request.getSession().removeAttribute("token");
        response.getWriter().print("<h1>submit success</h1>");
    }

}
~~~





## 3、单一外部控制器模式实现

















