# SPDY

`用于解决HTTP的性能瓶颈`

在类似Facebook,Twitter,微博等网站上。每时每刻都会有大量的新增

内容，而在对应的WEB网页客户端上，就需要实时的对数据进行更新，

在对于HTTP来说却无法很好的完成这些任务。因为原生的HTTP标准存在

以下限制：

1. 一条连接上只可发送一个请求
2. 请求只能由客户端发出，且客户端不能接受出响应之外的指令
3. 请求/响应首部未经压缩就发送。首部信息越多延迟越大。
4. 首部相同产生大量冗余。
5. 非强制压缩传送。

## Ajax

```
名词翻译
Asynchronous 
adj.[电] 异步的；不同时的；不同期的
```



`Ajax(Asynchronous JavaScript and XML,异步JavaScript与XML技术)`

`是一种有效利用JavaScript和DOM(Document Object Model,文档对象`

`模型)的操作，以达到局部Web页面替换加载的异步通信手段。只更新一部`

`分数据，响应传输的数据量因此减少。`

**核心技术：**XMLHttpRequest的API，使用JavaScript脚本语言与服

务器进行HTTP通信。

**总结：**通过Ajax实时从服务器获取数据，减少了数据的传输量，

但仍由可能产生大量的HTTP请求。

## Comet

`当服务器端有了新内容，Comet直接给客户端返回响应`

**原理：**通过延迟应答，模拟实现服务器端向客户端推送

(Server Push),Comet先将响应挂起，当内容更新，再

返回响应。`但延长了连接的持续时间，消耗了更多的资源，`

`也并未解决HTTP协议本身的问题。`

## SPDY目标

虽然出现了Ajax和Comet等提高易用性的技术，使HTTP得到了改善。

但并未改变HTTP本身的限制，所以`需要对HTTP协议层面进行一些改动`

## 设计方案

SPDY没对HTTP协议完全改写，而是在TCP/IP的应用层与传输层

之间通过新加入会话层。`SPDY以会话层的形式加入，控制数据的`

`流动，采用HTTP建立通信连接`。不影响使用HTTP的GET和POST，

Cookie以及HTTP报文。

**层次位置：**HTTP在应用层，TCP在传输层，IP在网络层，数据链路

层就是硬件层。为了HTTP的安全性，就在应用层和传输层之间加入

SSL进行安全传输，作为表示层。为了提高HTTP性能，就在HTTP与

SSL之间作为会话层之间加入SPDY。

## 实现功能

- 多路复用流

  通过单个TCP连接，处理无数个HTTP请求

- 赋予请求优先级

  SPDY可以无限制并发处理请求，并逐个分配优先级顺序

- 压缩HTTP首部

  减少通信产生的数据包数量及发送的字节数。

- 推送功能

  支持服务器主动向客户端推送数据

- 服务器提示功能

  服务器主动提示客户端请求所需资源，让客户端提前知道

  服务器所拥有的资源，就不用客户端请求服务器资源列表。

  减少发送不必要的请求。

## SPDY效果

由于SPDY只是将单个域名(IP地址)的通信多路复用，但当网页使用

到多个域名下的资源的时候，效果就不佳了。但其确实可以消除一部

分HTTP瓶颈，但许多问题并不只是HTTP瓶颈导致。

# WebSocket

利用Ajax和Comet技术可以提升Web的浏览速度。但还是会被HTTP

瓶颈限制。WebSocket网络技术被开发出来解决问题。

`WebSocket,即Web浏览器与Web服务器之间全双工通信标准，主要解决`

`Ajax和Comet里XMLHttpRequest附带的缺陷所引起的问题`

## WebSocket协议

- 场景：

  `当Web服务器与客户端建立WebSocket协议的通信连接，之后`

  `所有的通信都依靠这个专用协议进行`

- 传输内容：

  `JSON,XML,HTML或图片任意格式的数据`

- 规范：

  `由于是基于HTTP协议，所以连接发起方还是客户端，当连接`

  `建立以后，双方均可直接向对方发送报文`

- 特点：

  1. 推送功能

     服务器可向客户端直接推送功能

  2. 减少通信量

     只要建立连接，就一直保持连接，并且WebSocket的

     首部信息很小

## 请求与响应

```http
Accept-Encoding: gzip, deflate, br
Accept-Language: zh,zh-TW;q=0.9,en-US;q=0.8,en;q=0.7,zh-CN;q=0.6
Cache-Control: no-cache
Connection: Upgrade
Host: 127.0.0.1:3000
Origin: http://localhost:3000
Pragma: no-cache
Sec-WebSocket-Extensions: permessage-deflate; client_max_window_bits
Sec-WebSocket-Key: bwb9SFiJONXhQ/A4pLaXIg==
Sec-WebSocket-Version: 13
Upgrade: websocket
```

- Connection: Upgrade 表示要升级协议

- Upgrade: websocket 要升级协议到websocket协议

- Sec-WebSocket-Version 表示websocket的版本。如果服务端

  不支持该版本，需要返回一个Sec-WebSocket-Versionheader，

  里面包含服务端支持的版本号。

- Sec-WebSocket-Key 对应服务端响应头的Sec-WebSocket-Accept，由于没有同源限制，websocket客户端可任意连接支持websocket的服务。这个就相当于一个钥匙一把锁，避免多余的，无意义的连接。

***

```http
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connetion:Upgrade
Sec-WebSocket-Accept: bwb9SFiJONXhQ/A4pLaXIg==
Sec-WebSocket-Protocol: chat
```

Sec-WebSocket-Accept是由握手请求中的Sec-WebSocket-Key

生成的，不一样，上面只是复制的例子。连接成功后，通信就不再

使用HTTP的数据帧，而采用WebSocket独立的数据帧。

***

```javascript
// Create WebSocket connection.
const socket = new WebSocket('ws://localhost:8080');

// Connection opened
socket.addEventListener('open', function (event) {
    socket.send('Hello Server!');
});

// Listen for messages
socket.addEventListener('message', function (event) {
    console.log('Message from server ', event.data);
});
```

# HTTP2.0

`HTTP2.0的目标是改善网页速度体验`

- HTTP Speed + Mobility

  `由微软起草，建立在SPDY与WebSocket基础上`

- Network-Friendly HTTP Upgrade

  `改善移动端通信的HTTP性能`

  

