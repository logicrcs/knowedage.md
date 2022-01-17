# javaScript

## JS基本设定



1.通过外部文件引入javascript代码时，不要把标签写成自闭的

```javascript
<script src="demo.js"/>
    /*
    这种形式会在某些情况下出现浏览器不能正确引入的情况
    */
<script src="demo.js"></script>//应当是这种方式
```

2.js的复杂数据类型主要指对象：内置对象，自定义对象，数组，函数

基本数据类型:数值类型，字符串类型，布尔类型，undefined,null.

数值类型：js的数值在底层都是浮点型，但在需要时会自动在整型与浮点型之间转换。特殊值：infinity 正无穷大 ，-infinity  负无穷大，NAN 非数值

字符串在底层都有对应的包装对象--String

```javascript
var str1 = "hello JS";//typeof str3 -- string
var str2 = new String("Hello JS");//typeof str4 -- object 是包装类型
str1.valueof();//当需要时，会将字符串转成相应的包装对象，从而调用属性和方法
str2.value0f();
```

undefined:值只有一个，undefined,声明了变量，但是没有为变量赋值时，

该变量的值就是undefined;

3.js声明什么变量都是用var关键字，并且可以指向任意类型的数据

​	**注意：** var与let都可以用于定义任意变量，但是作用范围有区别

const 用于定义常量，定义之后便不能改变了

4.js数组声明方式

(1)声明 var arrl = [];

(2) var arr2 = [88,"hello",true,123];

(3) var arr3 = new Array();

js数组可以存放任意类型数据，使用length属性获取。数组长度会随着需要

自动延长。

```javascript
var object = {}
undefined
typeof object
"object"
var string = "strign"
undefined
typeof string
"string"
var ListType = []
undefined
typeof ListType
"object"
//数组也是object与json类似
var arr2 = [88,"hello",true,123];
undefined
typeof arr2
"object"
```



5.js中不能使用--

## JS中的dom操作

```javascript
function changeImg(){
    //通过id属性获取img元素对象，返回表示img元素的js对象
    var img = document.getElementById("img1");
    //通过img元素的src属性值修改图片的路径
    img.src = "imgs/on.gif";
}
```

## JS中的提示函数

```javascript
var flag = window.confirm("确认")
```

会弹出下面提示框

![](https://s2.loli.net/2022/01/13/w6OrJ2Zc3YIDHvL.png)

如果点击确认就会给flag返回一个true，取消就返回false

```javascript
flag
true
```

# JSON

**JSON**(JavaScript Object Notation) 是一种轻量级的数据交换格式。它使得人们很容易的进行阅读和编写。同时也方便了机器进行解析和生成。

本质也就是一个字符串，只不过格式特殊

格式可以查看json官网http://www.json.org.cn/index.htm

***对象格式*** 

```json
{
    key1:"value1",
    key2:"value2"
}
```

***数组格式*** 

```json
["value1","value2","value3"]
```

***调用方式***

在js中调用json是非常简单的

- name["key"]是支持最全面的，既可以在括号里放字符串

  也可以放字符串变量

- name.key比较方便并且直观，但是不能接变量，因为其会把变量当成字符串处理

```javascript
{jxgzdxze: 474.5615, deptid: 1, Hsse: 0,allnumber: 1485,deptid: 1,deptname: "中原油田普光分公司",jxgzdxze: 474.5615,quarterpunish: -66.9183,quartersalary: 541.4798,zzjljl: 0,zzxjl: 0}

var data = {jxgzdxze: 474.5615, deptid: 1, Hsse: 0,allnumber: 1485,deptid: 1,deptname: "中原油田普光分公司",jxgzdxze: 474.5615,quarterpunish: -66.9183,quartersalary: 541.4798,zzjljl: 0,zzxjl: 0}
data["Hsse"]
0
data.Hsse
0
var x = "deptname"
undefined
data.x
undefined
data[x]
"中原油田普光分公司"
```

 使用解构赋值提取JSON数据

```javascript
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};
let { id, status, data: number } = jsonData;
console.log(id, status, number);
// 42, "OK", [867, 5309]
```



# ajax

多次ajax嵌套要将内层的ajax设置成同步，否则就无法合理的显示数据