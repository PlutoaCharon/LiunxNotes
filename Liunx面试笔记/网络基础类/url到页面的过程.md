## 输入一个网址后发生了什么

- 输入网址并回车。
- 解析域名获得服务器 IP。
- 根据 IP 建立 TCP 管道。
- 浏览器连接 TCP 管道并发送 HTTP 请求。
- 服务器接收并处理请求。
- 服务器通过 TCP 管道传输 HTML 响应。
- 浏览器处理 HTML 响应，并渲染页面。
- 如果 HTML 内包含图片，CSS，JS 等其他资源，会继续请求其他资源。

详细内容可以参考：

[当你在浏览器中输入 google.com 并且按下回车之后发生了什么？](https://github.com/skyline75489/what-happens-when-zh_CN)

[细说浏览器输入URL后发生了什么](https://segmentfault.com/a/1190000012092552)