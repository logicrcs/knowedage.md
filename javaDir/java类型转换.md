# java类型转换

- Object转int

  Object不能直接转int,因为，Object是父类，但可以将Object转成String类型

  再通过Integer.parseInt()，parseInt()需要String作为输入。最终的代码就是

  Integer.parseInt(object.toString());

