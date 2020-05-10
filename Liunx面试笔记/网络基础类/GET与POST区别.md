## **HTTP请求GET和POST的区别**



1.GET提交，请求的数据会附在URL之后（就是把数据放置在HTTP协议头＜request-line＞中），以?分割URL和传输数据，多个参数用&连接;例如：`login.action?name=hyddd&password=idontknow&verify=%E4%BD%A0 %E5%A5%BD`如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密，得出如： `%E4%BD%A0%E5%A5%BD`，其中％XX中的XX为该符号以16进制表示的ASCII。

 POST提交：把提交的数据放置在是HTTP包的包体＜request-body＞中。

 因此，GET提交的数据会在地址栏中显示出来，而POST提交，地址栏不会改变

2.传输数据的大小：

  首先声明,HTTP协议没有对传输的数据大小进行限制，HTTP协议规范也没有对URL长度进行限制。 而在实际开发中存在的限制主要有：

  GET:特定浏览器和服务器对URL长度有限制，例如IE对URL长度的限制是2083字节(2K+35)。对于其他浏览器，如Netscape、FireFox等，理论上没有长度限制，其限制取决于操作系统的支持。

  因此对于GET提交时，传输数据就会受到URL长度的限制。

  POST:由于不是通过URL传值，理论上数据不受限。但实际各个WEB服务器会规定对post提交数据大小进行限制，Apache、IIS6都有各自的配置。

3.安全性：

  POST的安全性要比GET的安全性高。注意：这里所说的安全性和上面GET提到的“安全”不是同个概念。上面“安全”的含义仅仅是不作数据修改，而这里安全的含义是真正的Security的含义，比如：通过GET提交数据，用户名和密码将明文出现在URL上，因为(1)登录页面有可能被浏览器缓存， (2)其他人查看浏览器的历史纪录，那么别人就可以拿到你的账号和密码了，

4. 数据解析

`GET`: 通过`Request.QueryString`获取变量的值

`POST`: 通过`Request.form`获取变量的值

## [99%的人理解错 HTTP 中 GET 与 POST 的区别](https://www.oschina.net/news/77354/http-get-post-different)

## [Post 方法参数写在body中和写在url中有什么区别？](https://www.zhihu.com/question/64312188)

## [幂等性](https://www.cnblogs.com/weidagang2046/archive/2011/06/04/idempotence.html)

## [HTTP｜GET 和 POST 区别？网上多数答案都是错的！](https://www.jianshu.com/p/fd67b576365d)