# css选择器

1. 标签名选择器

```css
span{
 backgroud：#fff
}
标签名{
}
```

2. 类选择器

```css
.s1{
    
}
<span class = "s1"></span>
```

3. id选择器

```css
#s1{
    
}
<span id = "s1"></span>
```

4. 后代选择器

   ```css
   div span
   就是选择div内部的span元素
   ```
```css
   
   使用后代选择器可以使用id选择器与类选择器一起使用
   
   //在这其中，input[name='id']叫属性选择器
   #middle form table input[name = 'username']{
       ......
   }
   #middle form table .yzsj span{
       .....
   }
```

   