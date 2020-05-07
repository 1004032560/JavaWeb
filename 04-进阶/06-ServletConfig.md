



## 1、得到ServletConfig对象



~~~java
		//得到ServletConfig对象
		ServletConfig servletConfig = getServletConfig();
		
		//得到Servlet名称
		String servletName = servletConfig.getServletName();
		System.out.println(servletName);
		
		//得到上下文对象
		//getServletContext().getInitParameter("name")
		ServletContext servletContext = servletConfig.getServletContext();
		System.out.println(servletContext);
		
		//得到Servlet初始化参数
		//String initParameter = getInitParameter("name");
		String initParameter = servletConfig.getInitParameter("name");
		System.out.println(initParameter);
~~~





