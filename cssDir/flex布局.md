# flex布局

https://blog.csdn.net/weixin_42836226/article/details/102809084

1. flex布局的调用

   ```css
   display:flex
   ```

2. flex的元素排列方式--**flex-direction**

   - **flex-direction:row;** 沿水平主轴让元素从左向右排列
   - **flex-direction:column;** 让元素沿垂直主轴从上到下垂直排列
   - **flex-direction:row-reverse;**沿水平主轴让元素从右向左排列

3. flex的元素换行设置--**flex-wrap**

   - flex-wrap: nowrap; (默认)元素不换行,比如：一个div宽度100%，设置此属性，2个div宽度就自动变成各50%；
   - flex-wrap: wrap; 元素换行,比如：一个div宽度100%，设置此属性，第二个div就在第二行了；

4. flex的元素定位方式--**justify-content**

   - justify-content : center;元素在主轴（页面）上居中排列

     ![](https://s2.loli.net/2022/01/13/p8LUNXKxrAOEsgt.png)

     