## 1、Cookie 功能与特点

Cookie：是指一段保存在客户端的小文本

Cookie的功能：将用户活动过程中的状态信息保存在客户端

Cookie的特点：

1. 保存用户的信息
2. 服务器可以获得用户信息，跟踪用户的状态



## 2、Cookie 的生命域

1. name：Cookie 的名字
2. content：Cookie 的值
3. domain：Cookie 的域
4. path：
5. create：Cookie 的创建时间
6. expired：Cookie 的失效时间
7. 最大生命时间：Cookie 的失效时间减去 Cookie 创建时间





## 3、创建 Cookie 和设置 Cookie 的属性的 API

`Cookie(String name, String value)`：创建 Cookie 对象，指定相应的名称和值

`cookie.setMaxAge()`：设置 Cookie 的最大生命时间

`cookie.setValuee()`：设置 Cookie 的值

`cookie.setDomain()`：设置域名







## 4、在响应中设置 Cookie



~~~java
//创建 Cookie 对象
Cookie cookie = new Cookie("user", "looper");
//将 Cookie 保存到客户端
response.addCookie(cookie);
~~~







## 5、获取请求中的 Cookie







## 6、获取请求中的 Cookie信息

当

`Cookie[] getCookies()`：获取请求中所有的 Cookie 对象，返回数组对象

~~~java
//得到浏览器发送回来的 Cookie 数组
Cookie[] cookies = request.getCookies();
for (Cookie cookie1 : cookies) {
    //获取Cookie的值
	System.out.println(cookie1.getName()+" : "+cookie1.getValue());
}
~~~

