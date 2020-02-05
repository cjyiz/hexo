---
title: http学习记录
date: 2018-10-13 
tags: http
categories: 网络服务
---
# 一、HTTP简介
  HTTP是一种详细规定了浏览器和万维网服务器之间通信规则，通过因特网传送万维网文档的数据传输协议。全名叫 ***超文本传输协议（Hypertext transfer protocol）***。<!-- more -->

---
---
# 二、工作原理
  * 1.连接WEB服务器，单击某个超链接，HTTP开始工作。
  * 2.建立连接后，客户端发送一个请求给服务器。请求方式的格式为：统一资源标识符（URL）、协议版本号，后面是MIME信息包括请求修饰符、客户机信息等。有五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。
  * 3.服务器接收请求，并反馈响应信息。其格式为一个状态行，包括协议版本号、一个成功或者错误的代码，后面是MIME信息包括服务器信息、实体信息等。
  * 4.客户端接收反馈的响应信息后，通过浏览器处理并显示在用户的显示屏上，然后客户机与服务器断开连接。
    一个请求的开始到一个响应的结束称为事物，当一个事物结束后还会在服务端添加一条日志条目。

---

# 三、HTTPS
  * HTTPS是在HTTP基础上建立TLS/SSL加密层，并对数据进行加密，是HTTP协议的加密版。并且对搜索引擎更友好，利于SEO。因此现在越来越多的网站逐渐用HTTPS协议替代HTTP。 
---

# 四、案例 
  以[百度](https://www.baidu.com)为例，演示一下如何用Chrome开发者工具查看HTTP请求及响应内容。
  1.打开Chrome,按F12打开开发者工具，找到Network选项。
![1](../http学习记录/1.png)

  2.地址栏输入百度网址`https://www.baidu.com`,回车。可以看到有很多请求响应资源。
![2](../http学习记录/2.png)

  3.单击第一个百度的响应，可以看到右侧有详细的信息。点击view source ，可以查看具体的请求响应内容。
![Network](../http学习记录/3.png)

  4.请求内容

![request](../http学习记录/request.png)

  5.响应内容
![response](../http学习记录/response.png)

---

# 五、curl命令
  curl是一个利用URL规则在命令行下工作的文件传输工具，可以说是一款很强大的http命令行工具。它支持文件的上传和下载，是综合传输工具，但按传统，习惯称url为下载工具。
  在[explainshell.com](https://explainshell.com/) 中可以查看具体命令用法。
  在命令行中输入下面指令运行试试看。
   ` $ curl -s -v -H "Frank:xxx" --  "https://www.baidu.com" ` 

---

# 六、注意事项
  * 1.HTTP端口号默认为80,但是也可以手动改为8080或者其他端口号。HTTPS默认端口号为443。
  * 2.HTTP协议规定每次连接只处理一个请求。服务器处理完请求并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
  * 3.HTTP协议是对于事物没有记忆能力，后续处理需要前面的信息时，需要重新传输数据。
  * 4.HTTP协议使用统一资源标识符URL来传输数据和建立连接。
  * 5.HTTPS协议在浏览器显示绿色安全锁，HTTP没有显示。

参考链接：
[菜鸟教程HTTPS详解](http://www.runoob.com/http/http-messages.html)
[explainshell.com](https://explainshell.com/)
[关于HTTP协议，一篇就够了](https://www.cnblogs.com/ranyonsue/p/5984001.html)