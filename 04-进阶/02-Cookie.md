## 1、Cookie 功能与特点

Cookie：是指一段保存在客户端的小文本

Cookie的功能：将用户活动过程中的状态信息保存在客户端

Cookie的特点：

1. 保存用户的信息
2. 服务器可以获得用户信息，跟踪用户的状态



## 2、Cookie 的生命域

1. name：名字
2. content：值
3. domain：域
4. path：路径
5. create：创建时间
6. expired：失效时间
7. 最大生命时间：Cookie 的失效时间减去 Cookie 创建时间





## 3、创建 Cookie 和设置 Cookie 的属性的 API

`Cookie(String name, String value)`：创建 Cookie 对象，指定相应的名称和值

`cookie.setMaxAge()`：设置 Cookie 的最大生命时间

`cookie.setValuee()`：设置 Cookie 的值

`cookie.setDomain()`：设置域名



## 4、在响应中设置Cookie

通过 `response.addCookie(cookie)`，将创建好的 Cookie 对象保存到客户端。

~~~java
//创建 Cookie 对象
Cookie cookie = new Cookie("user", "looper");
//将 Cookie 保存到客户端
response.addCookie(cookie);
~~~



## 5、Cookie最大生命时间

1. 将 Servlet 创建好的 Cookie 对象通过 `response.addCookie(cookie)` 放到 response 对象中
2. 如果没有设置最大生命时间的情况下，浏览器接收到 Cookie 对象后存储到浏览器的本地 Cookie 缓存中，关闭浏览器之后缓存就没有了，Cookie 也没有了
3. 如果设置了最大生命时间的情况下（如：`7*24*3600`），浏览器接收到 Cookie 对象后存储到浏览器的本地 Cookie 缓存和硬盘中，关闭浏览器缓存就没有了，Cookie 还存在，下次开启浏览器访问网站时 Cookie 还能使用



## 6、获取请求中的 Cookie

1. 第一次请求：服务器将 Cookie 放到 response 对象中，让浏览器保存 Cookie 对象



2. 第二次请求：浏览器会自动带 Cookie 对象一并发送到服务器



## 7、获取请求中的Cookie信息

当访问相同域，及路径时，没有超过有效时间的 Cookie 对象将自动通过请求发送到服务器端

`Cookie[] getCookies()`：获取请求中所有的 Cookie 对象，返回数组对象

~~~java
//得到浏览器发送回来的 Cookie 数组
Cookie[] cookies = request.getCookies();
for (Cookie cookie1 : cookies) {
    //获取Cookie的值
	System.out.println(cookie1.getName()+" : "+cookie1.getValue());
}
~~~

