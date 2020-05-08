HTTP1.0和HTTP1.1最主要的区别就是：

- HTTP1.1默认是**持久化连接**！

在HTTP1.0默认是短连接：

![img](https://mmbiz.qpic.cn/mmbiz_png/2BGWl1qPxib2fuoQwW0ugqdD8wxEWXeemHOwW3sL5UAYv5kfdByQhb5ibuK3kgNOABDfviaJy06ic1eRxteyr0WeSg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

简单来说就是：**每次与服务器交互，都需要新开一个连接**！

在HTTP1.1中默认就使用持久化连接来解决：**建立一次连接，多次请求均由这个连接完成**！(如果阻塞了，还是会开新的TCP连接的)

![img](https://mmbiz.qpic.cn/mmbiz_png/2BGWl1qPxib2fuoQwW0ugqdD8wxEWXeemiamB8ibsA1FZdLcSkca8YjSyBD3rnMf13TibwJlfvSK114ShppnJvnUUQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

相对于持久化连接还有另外比较重要的改动：

- HTTP 1.1增加host字段

- HTTP 1.1中引入了`Chunked transfer-coding`，范围请求，实现断点续传(实际上就是利用HTTP消息头使用分块传输编码，将实体主体分块传输)

- HTTP 1.1管线化(pipelining)理论，客户端可以同时发出多个HTTP请求，而不用一个个等待响应之后再请求

- - 注意：这个pipelining仅仅是**限于理论场景下**，大部分桌面浏览器仍然会**选择默认关闭**HTTP pipelining！
  - 所以现在使用HTTP1.1协议的应用，都是有**可能会开多个TCP连接**的！

**HTTP1.0和HTTP1.1的一些区别**

HTTP1.0最早在网页中使用是在1996年，那个时候只是使用一些较为简单的网页上和网络请求上，而HTTP1.1则在1999年才开始广泛应用于现在的各大浏览器网络请求中，同时HTTP1.1也是当前使用最为广泛的HTTP协议。 主要区别主要体现在：

1. **缓存处理**，在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。
2. **带宽优化及网络连接的使用**，HTTP1.0中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1则在请求头引入了range头域，它允许只请求资源的某个部分，即返回码是206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。
3. **错误通知的管理**，在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。
4. **Host头处理**，在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应消息都应支持Host头域，且请求消息中如果没有Host头域会报告一个错误（400 Bad Request）。
5. **长连接**，HTTP 1.1支持长连接（PersistentConnection）和请求的流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启Connection： keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点。



**HTTP2.0和HTTP1.X相比的新特性**

- **新的二进制格式**（Binary Format），HTTP1.x的解析是基于文本。基于文本协议的格式解析存在天然缺陷，文本的表现形式有多样性，要做到健壮性考虑的场景必然很多，二进制则不同，只认0和1的组合。基于这种考虑HTTP2.0的协议解析决定采用二进制格式，实现方便且健壮。
- **多路复用**（MultiPlexing），即连接共享，即每一个request都是是用作连接共享机制的。一个request对应一个id，这样一个连接上可以有多个request，每个连接的request可以随机的混杂在一起，接收方可以根据request的 id将request再归属到各自不同的服务端请求里面。
- **header压缩**，如上文中所言，对前面提到过HTTP1.x的header带有大量信息，而且每次都要重复发送，HTTP2.0使用encoder来减少需要传输的header大小，通讯双方各自cache一份header fields表，既避免了重复header的传输，又减小了需要传输的大小。
- **服务端推送**（server push），同SPDY一样，HTTP2.0也具有server push功能。



参考链接：

https://juejin.im/entry/5981c5df518825359a2b9476

https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484302&idx=1&sn=5fafcb988463b5b2df9120552b6dc3f8&chksm=ebd7428fdca0cb99d5ed60296100b315c4ecaefc901fb5bb5448f902c6f41b0fa0dc18d5ee06&scene=21###wechat_redirect

