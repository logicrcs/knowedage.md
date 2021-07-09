# JAVASCRIPT中的可遍历数据

- **String**

  **for...of循环遍历**`能够正确识别文字编码`

  ```javascript
  let text = String.fromCodePoint(0x20BB7);
  for (let i of text) {
    console.log(i);
  }
  VM358:2 𠮷
  //而传统的for循环会认为其实两个不能打印字符
  for (let i = 0; i < text.length; i++) {
    console.log(text[i]);
  }
  VM364:2 �
  VM364:2 �
  ```

  

