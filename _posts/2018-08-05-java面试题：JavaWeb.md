---
layout: post
title: "Java面试题：JavaWeb"
date: 2018-8-5
description: "面试题 JavaWeb"
tag: Java面试题 
---   

## Java面试题：JavaWeb

------

### 1.session和cookie我们一般用来做什么?

1. cookie 是一个非常具体的东西，指的就是浏览器里面能永久存储的一种数 据。跟服务器没啥关系，仅仅是浏览器实现的一种数据存储功能。 session 从字面上讲，就是会话。这个就类似于你和一个人交谈，你怎么知道 当前和你交谈的是张三而不是李四呢？对方肯定有某种特征（长相等）表明他 就是张三。 
2. session 也是类似的道理，服务器要知道当前发请求给自己的是 谁。为了做这种区分，服务器就要给每个客户端分配不同的“身份标识” ，然 后客户端每次向服务器发请求的时候，都带上这个“身份标识” ，服务器就知 道这个请求来自于谁了。至于客户端怎么保存这个“身份标识” ，可以有很多 种方式，对于浏览器客户端，大家都默认采用 cookie 的方式。
3. cookie 存于客户端。 session 存于服务器端。
4. 服务器鉴别 session 需要至少从 客户端传来一个 session_id， session_id 通常存于 cookie 中。所以在工程上 session 离了 cookie 基本没法用，但是 cookie 可以单独使用，不过 cookies 是明文存储，安全性很低，只使用 cookie 的话盗取了 cookie 基本就获取了用 户所有权限。    

**项目中登录的模块结合 cookie**    

当会员需要登录的时候，首先进入的是“登录页面”，输入用户名、密码、验 证码进行登录，进入单点登录系统（Controller） Service Mapper DB 提交登录页面，用户信息被提交到单点登录系统进行校验。如果登陆信息不正 确，校验错误，将错误的登陆信息进行回显返回给用户，重新登录。验证通 过，就将用户信息保存到 redis 中，并且生成 token 作为一个标识，并将 token 保存到 cookie 里面，发送给用户浏览器，下次请求的时候就会带回来， 获取 cookie 里面的 token，根据 token 再去 redis 中查询对应的用户信息。登 录成功后将重定向到登录之前的访问页面。

------

### 2.Http协议中有哪些请求方式?

- **GET：** 用于请求访问已经被 URI（统一资源标识符）识别的资源，可以通过 URL
  传参给服务器
- **POST：**用于传输信息给服务器，主要功能与 GET 方法类似，但一般推荐使用
  POST 方式。
- **PUT：** 传输文件，报文主体中包含文件内容，保存到对应 URI 位置。
- **HEAD：** 获得报文首部，与 GET 方法类似，只是不返回报文主体，一般用于验证 URI 是否有效。
- **DELETE：**删除文件，与 PUT 方法相反，删除对应 URI 位置的文件。
- **OPTIONS：**查询相应 URI 支持的 HTTP 方法。

------

### 3.get 与 post 请求区别?

1. get 重点在从服务器上`获取资源`， post 重点在向服务器`发送数据`；
2. get 传输数据是通过 URL 请求，以 field（字段） = value 的形式，置于 URL 后，并用"?"连接，多个请求数据间用"&"连接，如http://127.0.0.1/Test/login.action?name=admin&password=admin，这个过程用户是可见的；
   post 传输数据通过 Http 的 post 机制，将字段与对应值封存在请求实体中发送给服务器，这个过程对用户是不可见的；
3. Get 传输的数据量小，因为受 URL 长度限制，但效率较高；
   Post 可以传输大量数据，所以上传文件时只能用 Post 方式；
4. get 是不安全的，因为 URL 是可见的，可能会泄露私密信息，如密码等；
   post 较 get 安全性较高；
5. get 方式只能支持 ASCII 字符，向服务器传的中文字符可能会乱码。
   post 支持标准字符集，可以正确传递中文字符。

------

### 4.常见 Http 协议状态?

1. 200：请求被正常处理
2. 204：请求被受理但没有资源可以返回
3. 206：客户端只是请求资源的一部分，服务器只对请求的部分资源执行 GET 方法，相应报文中通过 Content-Range 指定范围的资源。
4. 301：永久性重定向
5. 302：临时重定向
6. 303：与 302 状态码有相似功能，只是它希望客户端在请求一个 URI 的时候，能通过 GET 方法重定向到另一个 URI 上
7. 304：发送附带条件的请求时，条件不满足时返回，与重定向无关
8. 307：临时重定向，与 302 类似，只是强制要求使用 POST 方法
9. 400：请求报文语法有误，服务器无法识别
10. 401：请求需要认证
11. 403：请求的对应资源禁止被访问
12. 404：服务器无法找到对应资源
13. 500：服务器内部错误
14. 503：服务器正忙

------

### 5.Servlet 的执行流程。 doGet 和 doPost 的区别？

1. Servlet 的执行流程也就是 servlet 的生命周期，当服务器启动的时候生命周期开始，然后通过 init()*启动顺序根据 web.xml 里的 startup-on-load 来确定加载顺序*方法初始化 servlet，再根据不同请求调用 doGet 或 doPost 方法，最后再通过 destroy()方法进行销毁。
2. doGet 和 doPost 都是接受用户请求的方法， doGet 处理 get 请求， doPost 处理post 请求， doGet 用于地址栏提交， doPost 用于表单提交，在页面提交数据时， get 的数据大小有限制 4k， post 没有限制， get 请求提交的数据会在地址栏显示， post 不显示，所以 post 比 get 安全.

------

### 6.Jsp 的重定向和转发的流程有什么区别？

1. 重定向是`客户端`行为，转发是`服务器`端行为
2. 重定向时服务器产生两次请求，转发产生一次请求，重定向时可以转发到项目以外的任何网址，转发只能在当前项目里转发
3. 重定向会导致 request 对象信息丢失。转发则不会
4. 转发的 url 不会变,request.getRequestDispatch（） .forward()
5. 重定向的 url 会改变,response.getRedirect();

------

### 7.Jsp 的九大内置对象，三大指令，七大动作的具体功能？

1. **JSP 九大内置对象:**

   > - pageContext ：只对当前 jsp 页面有效，里面封装了基本的 request 和session 的对象
   > - Request ：对当前请求进行封装
   > - Session ：浏览器会话对象，浏览器范围内有效
   > - Application ：应用程序对象，对整个 web 工程都有效
   > - Out ：页面打印对象，在 jsp 页面打印字符串
   > - Response ：返回服务器端信息给用户
   > - Config ：单个 servlet 的配置对象，相当于 servletConfig 对象
   > - Page ：当前页面对象，也就是 this
   > - Exception ：错误页面的 exception对象，如果指定的是错误页面，这个就是异常对象

2. **三大指令：**

   > - Page ：指令是针对当前页面的指令
   > - Include ：用于指定如何包含另一个页面
   > - Taglib ：用于定义和指定自定义标签

3. **七大动作：**

   > - Forward，执行页面跳转，将请求的处理转发到另一个页面
   > - Param ：用于传递参数
   > - Include ：用于动态引入一个 jsp 页面
   > - Plugin ：用于下载 javaBean 或 applet 到客户端执行
   > - useBean ：使用 javaBean
   > - setProperty ：修改 javaBean 实例的属性值
   > - getProperty ：获取 javaBean 实例的属性值

------

### 8.request ，response，session 和 application 是怎么用的？

- Request 是客户端向服务端发送请求
- Response 是服务端对客户端请求做出响应
- Session 在 servlet 中不能直接使用，需要通过 getSession()创建，如果没有设定它的生命周期，或者通过 invildate()方法销毁，关闭浏览器 session 就会消失
- Application 不能直接创建，存在于服务器的内存中，由服务器创建和销毁









----------------------------

转载请注明原地址，宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！