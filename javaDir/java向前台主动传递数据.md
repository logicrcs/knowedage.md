# java向前台主动传递数据

- 使用Cookie

  ```java
  @GetMapping("/zsdwMobileList")
      String zsdwMobileList(HttpServletResponse response,@RequestParam Map<String, Object> params) {
          Cookie cookie = new Cookie("layuiId", (String) params.get("layuiId"));
          Cookie cookie1 = new Cookie("year", (String) params.get("year"));
          Cookie cookie2 = new Cookie("fillquarter", (String) params.get("fillquarter"));
          response.addCookie(cookie);
          response.addCookie(cookie1);
          response.addCookie(cookie2);
          return "sevenone/mobile/zsdwMobileList";
      }
  //HttpServletResponse response代表引入了返回对象
  //通过创建cookie，并将cookie放入response将其传给前台
  ```

  