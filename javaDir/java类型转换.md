# java类型转换

- Object转int

  Object不能直接转int,因为，Object是父类，但可以将Object转成String类型

  再通过Integer.parseInt()，parseInt()需要String作为输入。最终的代码就是

  Integer.parseInt(object.toString());
  
- java中小转大，不存在相关的类型问题，可以进行隐式转换，大转小不仅要保证

  小类型是能够存的下的，并且要加上类型

  ```java
  byte a = 1;
  byte b = 2;
  //byte c = a+b;这样就会报错,因为+会自动将数据类型升至int
  byte c = (byte)(a+b);
  System.out.println("光年的长度："+300000000*60*60*24);//-127631360
  //-127631360这个数明显是错的，因为在过程中计算超过了int的范围，造成了溢出。
  System.out.println("光年的长度："+300000000L*60*60*24);//25920000000000
  //但是不能在24之后加L，因为3亿*60就已经超过int的范围了，在这种情况下就已经出现了数据的丢失了。
  ```

  

