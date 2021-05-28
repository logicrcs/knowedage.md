# RestTemplate

springboot提供的一个Res远程调用工具

在引入了对应的包后private RestTemplate之后就可以使用springboot注入对象。

- getForObject() - 执行get请求
- postForObject() - 执行post请求

```java
@AutoW
private RestTemplate rt
  rt.getForObject("url",就收数据的对象[,params1])
  
  rt.getForObject("http://localhost:8101/{1}/score?score={2}",JsonResult.class,userId,Score)
  //url里面有几个空位就在传递的数据里有几个参数，参数之间使用逗号隔开
```



