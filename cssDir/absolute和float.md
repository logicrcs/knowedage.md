# absolute和float

> **原则上position:absolute和float:left拥有相似的特型，都会使元素出现inline-block现象，position：absolute会将自己的布局与界面的原布局脱离开，float:left则仅仅Inline-block化，并且向左漂移。根本的差别是，绝对定位脱离了文档流，浮动则还在文档流里面**

***造成的实际结果为***

1. 文档流中的文字不会与浮动元素重叠，但会与绝对定位元素

   重叠

2. 绝对定位如果设置了left:0;top:0;就会从DOM tree中独立对最近的position:relative祖先标签定位，没有，就

   相对于body定位。

   

