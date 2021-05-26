# HTML跨域访问

## 同源策略

***如果ajax发起请求时，如果想要正确的返回数据，需要进行配置*** 

```java
1.请求协议名称http https
2.域名地址
3.端口号
```

***但是浏览器要求ajax发起请求的配置与自身的配置一致*** 

*如果这3个里面有一个不相同，就是跨域访问* 

**ajax** 在访问时可能会出现跨域访问的问题，不过ajax是在浏览器端发起请求

还可以使用**httpclient** 在服务器发起http请求。不过过程是有些繁琐。但是可以规避跨域访问造成的问题，因为跨域访问是浏览器才会发生的问题。

### 实现跨域的基本原理

> *http默认开放src的跨域访问*
>
> 1. 由于浏览器同域策略的限定，禁止ajax发起跨域请求
> 2. 但是http存在引入外部文件的需要
> 3. 所以浏览器对于src属性具有开放策略。用来实现跨域访问。
>

## 实现跨域的方案（src）

###  利用javaScript中的src属性，实现跨域 

```javascript
<script type="text/javascript" src="jquery.js"></script>
```

###  自定义回调函数

1. 通过上述方式引入数据后，如果页面想要调用，就需要通过函数名称，才能正确调用。

2. 设置自定义回调函数为远程调用的数据起名。

   

   ```javascript
   /*在页面上写自己的回调函数，并且保证回调函数写在script标签的前面*/
   function hello(data){
   	alert(data.name)
   }
   ```

3. 将远程调用的返回值经过特殊的格式封装**"callback(JSON)"** 

   ```javascript
   /*这是在服务器端写的需要返回给前端的文件格式*/
   hello({"id":1,"name":"tom"})
   ```

   

### JSONP

> `JSONP`(JSON with Padding)时**JSON** 的一种**使用模式**，可用于解决主流浏览器跨域数据访问带来的数据问题。

#### JSONP的优化

##### 问题：

1. 需要通过javaScript中的src属性，繁琐不方便
2. 每次调用都需要自定义回调函数
3. 前后端调用时，必须满足回调函数名称一致

##### 解决办法：

1. 优化ajax方法，让ajax实现跨域访问
2. 使用随机参数，动态生成回调函数名称，保证名称不重复
3. 发起跨域请求时，自带回到函数方法名称，有后台获取，实现名称一致

#### Jquery实现JSONP

```javascript
$.ajax({
  url:"跨域访问的网址"，
  dataType:"jsonp",
  type:"get",
  jsonp:"callback", //指定参数名称，一般不做修改
  jsonCallback:"指定的回调的名称"，//指定回调函数的名称
  success:function (data){  //data就是服务器经过jquery封装返回的数据
   	......
	}
})
最后服务请求的url就可能时http://www.域名.com/访问路径？callback=回调的名称
```

