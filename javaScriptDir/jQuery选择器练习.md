# jQuery选择器练习

1.id选择器：$("#id")

```javascript
//通过id选择b1的按钮，绑定点击事件，设置div的颜色
$("#b1").click(function(){
    $("div").css("background","#FD5551")
})
```

2.class选择器：$(".class")

```javascript
$("#b3").click(function(){
	$(".mini").css("background-color","#EE82EE")
})
```

3.层级选择器：$("祖先 后代")

```javascript
$("#b4").click(function(){
    $("div span").css("background-color","#EE82EE")
})
```

