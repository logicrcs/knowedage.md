# JAVASCRIPT 变量的作用域 

javascript原生的变量定义之后的作用域是有问题的

```javascript
for(var i=0;i<5;i++){}
console.log(i)
VM2126:1 5
//本来i不应该被for之外的语句访问到的，但是却被访问到了
```

所以javascript更新了新的变量定义

```javascript
for(let j=0;j<5;j++){}
console.log(j);
VM2385:1 Uncaught ReferenceError: j is not defined
    at <anonymous>:1:13
//现在由let定义的变量就可以由好的作用域控制了
```

而观察变量定义的作用范围

```javascript
function ff(){
    {
        var i=100;
        let j=200;        
    }
    console.log("i",i);
    console.log("j",j);
}
ff()
VM2656:6 i 100
VM2656:7 Uncaught ReferenceError: j is not defined
    at ff (<anonymous>:7:21)
    at <anonymous>:1:1
//可以发现由var定义的变量可以超出代码块的限制，但let定义的变量不行
console.log(i)
VM2754:1 5
//但两者均不能超出函数体的限制
```

