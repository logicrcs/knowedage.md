# html文档就绪时间函数

1.将相关script代码放到body里面，在页面的最后面

2.js本身的文档就绪事件函数：在浏览器加载完之后执行

```javascript
window.onload = function(){
    //里面的函数会在整个html文档加载完毕后执行
}
```

3.使用jQuery提供的文档就绪事件函数

```javascript
$(function(){
    
})；
```

