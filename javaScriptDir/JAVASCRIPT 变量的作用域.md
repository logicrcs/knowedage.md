# JAVASCRIPT 变量的作用域 

javascript原生的变量定义之后的作用域是有问题的

```javascript
for(var i=0;i<5;i++){}
console.log(i)
VM2126:1 5
//本来i不应该被for之外的语句访问到的，但是却被访问到了
//所以在ES6中引入了块级作用域和let
```

所以javascript更新了新的变量定义，***let只能所在的代码块内有效***

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

let适用于for循环

```javascript
for(let i =0; i <10; i++){
// ...
}
console.log(i);
// ReferenceError: i is not defined
// 但在for循环中，每个i都是一个全新的值，如下面代码
// a数组内的每一个都是执行console.log(i),并且在保存
// 的时候就已经将i的地址信息保存进去了
// 由于let的默认属性，所以每次循环都会创建一个新的i
var a =[];
for(let i =0; i <10; i++){a[i]=function(){
    console.log(i);
    };
}
a[6]()
6
//每一个值都是一段代码
a[5]
ƒ (){
    console.log(i);
    }
a[5]()
5
```

但var就与let不同

```javascript
//var是定义全局变量,所以无论是使用几遍循环，都会存在一个i
var a =[];
for(var i =0; i <10; i++){
  a[i]=function(){
    console.log(i);
	};
}
a[1]
ƒ (){
    console.log(i);
}
a[1]()
10
a[2]()
10
a[2]
ƒ (){
    console.log(i);
}
```

***for的作用域***

for其实是双重作用域，设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域

```javascript
for(let i =0; i <3; i++){
  let i ='abc';
  console.log(i);
}
3VM88:3 abc
//输出了 3 次abc,说明作为循环变量的i在从0-2这个过程中
//没有出现里面的变量干扰循环变量的现象

```

***var全局作用域***

```javascript
//虽然ful在声明之前被使用，但是由于var创建的是全局变量
//所以不会直接报错
console.log(ful)
var ful = 11
undefined
//但如果是let就会直接报错
console.log(lim)
let lim = 11
VM232:1 Uncaught ReferenceError: lim is not defined
    at <anonymous>:1:13

```

***let不允许在相同区域中重复声明同一个变量，也不允许在变量的声明之前使用变量，这两中行为都会报错***

***块级作用域***

**注意：**别{}包裹的内部才能算是块级元素

```javascript
//只有使用{}才能创建块级元素
// 第一种写法，报错
if (true) let x = 1;
VM374:2 Uncaught SyntaxError: Lexical declaration cannot appear in a single-statement context
// 第二种写法，不报错
if (true) {
  let x = 1;
}
undefined
```



```javascript
//原本使用匿名立即执行函数表达式（匿名IIFE）是为了能够使得
//变量能够在限定的范围内使用，代码如下所使，本来使用var定义
//tmp为全局变量，但是由于匿名函数执行之后便会被立即回收，所以
//变量就不存在溢出的风险了
(function () {
  var tmp = "xxx";
}());
tmp
VM270:1 Uncaught ReferenceError: tmp is not defined
    at <anonymous>:1:1
//但是使用Let上块级作用域后，这种问题就不复存在了
{
  let tmp = "ccccc"
}
tmp
VM331:1 Uncaught ReferenceError: tmp is not defined
    at <anonymous>:1:1
```

**注意：**在块级作用域中声明的函数是不能在作用域外使用的

```javascript
(function () {
  if (false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }
  f();
}());
VM336:6 Uncaught TypeError: f is not a function
    at <anonymous>:6:3
    at <anonymous>:7:2
//当然也有些浏览器支持这么使用，但20210707，火狐，谷歌浏览器
//已不支持这么使用
{
  //如果要使用，请使用函数表达式
  let a = 'secret';
  let f = function () {
    return a;
  };
}
```

***const***

由const声明的变量是不能改变值，当然这个不能改变指的是一个被const声明得**变量x指向得目标内存地址中保存的数据是不能改变的**。所以如果目标内存地址直接保存的就是数据，就像数值，字符串，布尔值这样的简单类型，那么就相当于常量。**可如果是符合类型的数据，就像变量和数组，变量指向的内存地址保存的就不是实际数据了，而是一个指向实际数据指针。对此，const就只能保证这个指针是固定的，但不能保证它指向的数据也不变。**

`const与let一样适用于块级作用域，也和Let一样不可重复`

