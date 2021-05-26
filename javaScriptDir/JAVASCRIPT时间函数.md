JAVASCRIPT时间函数

***创建时间对象***

```javascript
var date = new Date;
var year = date.getFullYear();//2021
//getMonth()会返回比当前月份小1
var month = date.getMonth()//3
var curDate = date.getDate()//1 (1-31)
var curDate2 = date.getDay();//4(0-6,0代表星期天)
var curDate3 = date.toLocaleDateString();//2021/4/1 
var curDate4 = date.toLocaleString();//2021/4/1 下午5:06:56
```

