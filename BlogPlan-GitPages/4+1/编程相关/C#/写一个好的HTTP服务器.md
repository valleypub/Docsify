[toc]


1. 所谓的实现一个HTTP server究竟是做哪些工作？？？基于TCP组件来按照HTTP协议图纸来写出一个应用层的封装？？？
2. 现在HTTP Server一般怎么写？？
	1. https://blog.csdn.net/heiyeshuwu/article/details/2576915




# C版本的



# C#版本的
## .NET下的HTTP程序开发技术

### WebRequest类
- 是什么
	- WebRequest类是.NET Framework的请求／响应模型的抽象（abstract）基类，用于访问Internet数据。它允许使用该请求／响应模型的应用程序可以用协议不可知的方式从Internet请求数据。

### HttpWebRequest类
- 是什么
	- HttpWebRequest类是针对HTTP的特定实现。该类通过HTTP和服务器交互。HttpWebRequest类对HTTP进行了完整的封装，例如，对HTTP中的Header、Content、Cookie都提供了对应的属性和方法。利用HttpWebRequest类，可以很容易地写出一个模拟浏览器自动登录的程序。


### 提交数据的编码方式

#### POST提交的页面抽象字符内容的编码的方式
1. 中文编码：常用的有gb2312 和 utf8两种。由于无法告知对方提交数据的编码类型，所以编码方式要以对方的网站为标准。常见的网站中，
	1. www.baidu.com （百度）的编码方式是gb2312
	2. www.google.com （谷歌）的编码方式是utf8。
2. 英文编码：utf8 ，ASCII，不同的网站使用的都是哪些？？？
	1. 百度：
	2. 谷歌：
	3. 

#### POST方式
由于POST方式提交的参数中可以说明使用的编码方式，所以理论上能获得更大的兼容性，提交时可以说明编码的方式，使对方服务器能够正确地解析。



#### Web Service方式




