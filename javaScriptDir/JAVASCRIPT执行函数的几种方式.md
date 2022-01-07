# JAVASCRIPT执行函数的几种方式

```javascript
function f01(){console.log("hello")};
f01();
VM1044:1 hello
(function f01(){console.log("hello")})()
VM1104:1 hello
(function f01(){console.log("hello")}())
VM1118:1 hello
(function(){console.log("aaa")})() //（函数体）（）
VM1270:1 aaa
```

当对函数完成定义时，

***函数名+（）*** 执行

***（函数定义结构）+（）*** 执行

***（函数定义结构（））*** 执行

## 定义framework型的函数

```javascript
(function (){var ajax = 1000;})();
//使用方法体加括号运行函数
console.log(ajax)
VM1408:1 Uncaught ReferenceError: ajax is not defined
    at <anonymous>:1:13
//但是由于ajax不是全局变量，所以无法在控制台输出
```

```javascript
(function (){var ajax = 1000;window.ajax=ajax;})();
//在方法体{}内加入了window.ajax=ajax
console.log(ajax)   
VM1601:1 1000
//成功将方法内变量转化为全局变量
```

将所有代码放到一个函数里封装起来，使用window.xxx=xxx;对外传递一个可以操作所有函数的对象

```javascript
(function(){
    var Ajax=function(){}
    //每个js函数内部存在一个原型对象，被所有函数实例共享
    /*
    在这里prototype里面的内容就是这个原型对象
    外界通过Ajax.functionName调用的对应函数，都会从prototype
    中获取字节码
    */
    Ajax.prototype={
        doAjaxGet:function(xxx,xxx,xxx){
            ......
        },
        doAjaxPost:function(xxx,xxx,xxx){
            ......
        },
        functionName:function(param){
            functionBody;
        }
    }
    window.Ajax = new Ajax();
})
```

示例：

```javascript
(function(){
  var tree=function(height){
    this.height=height;
  };
    tree.prototype={
    getHeight:function(){
      return this.height;
    },
        setHeight:function(height){
      this.height=height;
    }
  }
    //将其输出成系统变量
    window.tree=tree;
})();
```

<img src="..\img\javascript封装函数.png" alt="javascript封装函数" style="zoom:150%;" />

