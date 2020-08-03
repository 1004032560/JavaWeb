## 1、Ajax

### 1.1、什么是Ajax

`Asynchronous javascript and xml`：异步的 Javascritp 和 XML

核心对象：通过 XMLHttpRequest 简称 xhr，实现局部刷新

<br>

### 1.2、Ajax思想

使用 XMLHttpRequest 对象，与服务器交互，实现局部刷新。

局部刷新：不提交整个页面，而是在页面的某个部分；例如：一个文本框或者按钮，发送请求，实现刷新。

整体刷新：整个页面提交。

<br>

## 2、异步和同步

### 2.1、异步

不等，上一步没做完，不等，继续做自己的

特点：

约定：和上一步约定好放数据的地方

<br>

### 2.2、同步

等待，上一步做完，一直等待

<br>

## 3、Ajax用法

### 3.1、原生Ajax

1. 创建 XMLHttpRequest 对象
2. 调用 open 方法，打开连接
3. 使用回调函数接收返回的数据
4. 发送请求

~~~html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<base href="${pageContext.request.contextPath }/">
<title>Insert title here</title>
<script type="text/javascript">
function test(){
	   //1.创建xhr对象
	   var x=new XMLHttpRequest();
	   //2.调用open方法,打开连接
	   x.open("GET","AjaxServlet?name=ZhangSan",true);
	   //3.数据放到筐里,把筐准备好
	   x.onreadystatechange=function(){
	     //在这里接收数据,分析数据
	     //x.status 响应状态码 200 OK 404:请求的资源没找到 500 服务器内部错误
	     if(x.status==200 && x.readyState==4){
	       //响应的数据放在x.responseText
	       alert(x.responseText);
	     }
	   }
	   //4.发送请求
	   x.send();
	 }
</script>
</head>
<body>
<button onclick="test()">Ajax</button>
</body>
</html>
~~~

<br>

### 3.2、jQuery Ajax

#### 3.2.1、jQuery原生

~~~jsp
<script type="text/javascript" src="js/jquery-1.8.3.js"></script>
<script type="text/javascript">
 function test(){
   $.ajax({
     url:"AjaxServlet",
     type:"GET",
     data:{name:"ZhangSan"},
     success:function(data){
       alert(data);
     },
     dataType:"text"
   });
 }
</script>
~~~

<br>

#### 3.2.2、jQuery简化版

~~~jsp
<script type="text/javascript" src="js/jquery-1.8.3.js"></script>
<script type="text/javascript">
 function test(){
	$.post(
		"AjaxServlet",
		{name:"ZhangSan"},
		function(data){
		    alert(data);
		},
		"text"
	)
 }
</script>
~~~





