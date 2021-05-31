# HTTP报文的结构

**报文首部：** 包含客户端及服务器处理时其至关重要作用的信息。

**空行(CR+LF)**

**报文主体：**所需要的客户和资源的信息都在这边。

# HTTP请求报文

在请求报文中的报文首部

**请求行：**方法。URI，HTTP版本

**HTTP首部字段：**请求首部字段，通用首部字段，实体首部字段

在响应报文中的报文首部

**状态行：**HTTP版本，状态码

**HTTP首部字段：**响应首部字段，通用首部字段，实体首部字段

# HTTP首部字段

## HTTP首部字段结构

- 由首部字段名和字段值构成，中间冒号风格

  ```http
  首部字段名： 字段名
  Content-Type: text/html;
  Keep-Alive: timeout=15, max=100
  ```

## 4种HTTP首部字段类型

- 通用首部字段(General Header Fields)

  请求与响应均会使用的首部

- 请求首部字段(Request Header Fields)

  从客户端向服务器端发送请求报文使用的首部。

- 响应首部字段(Response Header Fields)

  从服务器端向客户端发送请求报文使用的首部

- 实体首部字段(Entity Header Fields)

  针对请求报文和响应报文的实体部分使用的首部。