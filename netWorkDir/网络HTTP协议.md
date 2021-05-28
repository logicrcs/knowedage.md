#	HTTP

- HTTP是无状态协议，一次请求和响应的内容本身不会持久化

  不用保存状态，可以减少服务器的计算机资源的开销。

- 部分请求报文结构

  1. GET http://hackr.jp/index.htm HTTP/1.1

  2. GET /index.htm HTTP/1.1

     HOST: hackr.jp

  3. POST /submit.cgi HTTP/1.1

     HOST: www.hackr.jp

     Content-Length: 1560

  4. PUT /example.html HTTP/1.1

     HOST: www.hackr.jp

     Content-Type: text/html

     Content-Length: 1560

     报文开头是PUT，代表这个请求报文时用来传输文件的

- 持久连接

  在显示包含大量内容的网页时，网页上的资源往往不能同步

  刷新完毕，这个时候就要保证TCP保证连接，只好没有任意

  一段明确提出断开连接，就保持TCP的连接状态。总而言之，

  持久连接就是建立一次TCP连接后进行多次请求和响应的交

  互。HTTP Persistent Connections,也称HTTP keep-al

  ive或是HTTP connection reuse。

  **优点：**

  1. 减少了TCP连接的重复建立与断开所造成的额外开销

  2. 不必发送请求后等待响应，可以同时并行发送多个请求

     实现请求的管线化(pipelining)

- Cookie

  由于HTTP是无状态协议，虽然减少了服务器的压力，但是也

  无法根据之前的状态进行本次的请求处理。在一些用户登录

  的场景里，就非常麻烦了。在需要保留无状态协议这个优势

  的前提下，又要解决无状态带来的问题，就引入了Cookie技

  术。**通过在请求与响应报文中写入Cookie信息来控制客户**

  **端的状态**

  **具体操作：**Cookie会根据从服务器端发送的响应报文中一个

  名为Set-Cookie的首部字段信息，通知客户端保存Cookie。

  在下次客户端发送请求时，将保存在客户端Cookie的内容加

  到请求报文中。服务器端发现请求报文中的Cookie后，检查

  是哪个客户端发送的连接请求，对比服务器的记录，得到与

  客户端对应的状态信息。

- HTTP报文

  用于HTTP协议交互的信息。客户端叫做请求报文，服务器端

  叫做响应报文。本身由多行(用CR+LF做换行符)数据构成的

  字符串文本。

  1. 报文首部：服务器端或客户端需处理的请求或响应的内

     容及属性。

  2. CR+LF : 回车符和换行符均为16进制。

     CR(Carriage Return),回车符：0x0d

     LF(Line Feed),换行符：0x0a

  3. 报文主体：需要发送的数据。

  **请求报文首部：**请求行，请求首部字段，通用首部字段，实

  体首部字段，其他。

  **响应报文首部：**状态行，响应首部字段，通用首部字段，实

  体首部字段，其他。

  1. 请求行：包含用于请求的方法，请求URI和HTTP版本。

  2. 状态行：包含表明响应结果的状态码，原因短语和HTTP

     版本

  3. 首部字段：包含表示请求和响应的各种条件和属性的

     各类首部；一般4种，通用首部，请求首部，响应首部

     和实体首部。

  4. 其他：包含HTTP的RFC里未定义的首部(Cookie之类)。

- 编码提传输速率

  HTTP/1.1中存在一种称为**传输编码(Transfer Coding)**的

  机制，可以在通信时按某种编码方式传输，但只定义作用于

  分块传输编码中。

  为了防止在资源加载的过程中出现由于网络中断而重复加载

  的问题，实现了指定了下载的实体范围的功能，名为

  范围请求(Range Request),**能够从告知服务器端下载完整**

  **文件的一部分，从而实现了能从之前下载中断处恢复下载**

  类似于下载器领域的断点续传。

  对应范围请求，响应会返回状态码为206 Partial Content

  的响应报文。对于多重范围的范围请求，响应会在首部字段

  Content-Type标明multipart/byteranges后返回响应报

  ```http
  /*范围请求的请求头*/
  GET /tip.jpg HTTP/1.1
  HOST: www.usagidesign.jp
  Range: bytes =5001-10000	//从5001字节到10000字节
  //如果是5001之后的 Range:bytes=5001-
  //Range: bytes=-3000, 5000-7000 代表从一开始到
  3000字节和5000-7000字节的多重范围
  
  /*范围请求的响应体*/
  HTTP/1.1 206 Partial Content
  Date: Fri, 13 Jul 2012 04:39:17 GMT
  Content-Range: bytes 5001-10000/10000
  Content-Length: 5000
  Content-Type: image/jpeg
  ```

- 内容协商

  客户端和服务器就响应的内容进行交涉，然后提供给客户端

  合适的资源。这种机制就是**内容协商**

  但浏览器的默认语言是英语或中文，网页对应的显示英文版

  或是中文版的WEB界面。是**内容协商(Content Negotiation)**

  的实际应用。其以响应资源的语言，字符集，编码方式等作为

  判断基准。有三种类型：

  1. **服务器驱动协商(Server-driven Negotiation)**

     服务器以请求的首部字段为参考自动处理，不一定是

     合适的。

  2. **客户端驱动协商(Agent-driven Negotiation)**

     用户在浏览器的可选项列表中手动选择或利用JavaScript

     脚本在Web页面自行选择。

     ![用户选择语言](C:\Users\Administrator\Desktop\企管处考核系统\knowedage.md\img\客户端驱动协商.png)

  3. **透明协商(Transparent Negotiation)**

     服务器驱动与客户驱动的结合。就是双管齐下。

