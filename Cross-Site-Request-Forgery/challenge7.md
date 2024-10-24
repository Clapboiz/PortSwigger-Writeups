![image](https://github.com/user-attachments/assets/e77df31f-e5ff-4532-94a2-c02abbfcf1d1)

Như bạn đọc vào thì bạn có thể thấy được rằng challenge này nó dùng `samesite: lax`. Thì để tôi sơ qua về lí thuyết cho bạn hiểu.

SameSite là một thuộc tính của cookie giúp kiểm soát việc cookie có được gửi cùng với các yêu cầu đến từ các trang web khác nhau hay không. Nó được thiết kế để giúp bảo vệ ứng dụng khỏi các cuộc tấn công CSRF và giảm thiểu việc theo dõi của bên thứ ba.

Thuộc tính SameSite có thể có các giá trị sau:

+ SameSite=Lax: Cookie chỉ được gửi khi người dùng điều hướng đến trang web (ví dụ: nhấp vào link trên một trang khác). Cookie không được gửi khi yêu cầu là phương thức không phải là GET (ví dụ: POST, PUT). Đây là chế độ mặc định của nhiều trình duyệt hiện nay. Nó vẫn chấp nhận cookie khi điều hướng liên kết thông thường (GET request) nhưng hạn chế cookie khi có POST request từ một trang khác, nhằm giảm nguy cơ CSRF.
+ SameSite=Strict:
Cookie chỉ được gửi nếu yêu cầu xuất phát từ cùng một trang web. Ngay cả khi người dùng nhấp vào liên kết từ một trang web khác, cookie cũng sẽ không được gửi. Điều này cung cấp mức bảo vệ cao nhất khỏi CSRF, nhưng có thể làm giảm trải nghiệm người dùng.
+ SameSite=None: Cookie sẽ được gửi trong tất cả các yêu cầu, ngay cả khi đến từ các trang web khác. Tuy nhiên, kể từ khi trình duyệt Chrome cập nhật, nếu thuộc tính SameSite=None được sử dụng, cookie cũng phải có thuộc tính Secure, nghĩa là chỉ gửi qua kết nối HTTPS.

![image](https://github.com/user-attachments/assets/91775044-e050-4e52-a207-4bd7d8c82eab)

Tiến hành đổi email và bắt request thì ta thấy được lần này nó không yêu cầu csrf token, nhưng khi tôi gen ra form thì tôi gửi con bot nó lại không hoạt động, lí do là gì nhỉ ??

![image](https://github.com/user-attachments/assets/16a16636-7ab2-4227-b15f-6cc20d60d789)

Bạn có thể thấy samesite không được set, tức là mặc định nó là lax. vậy còn cách nào khác không??

POST không gửi cookie trong cross-site requests với SameSite=Lax, để chặn CSRF.

GET vẫn gửi cookie trong cross-site requests nếu có điều hướng cấp cao nhất, nên có thể bypass CSRF trong một số trường hợp.

Vậy thì tiến hành đổi sang GET v:

![image](https://github.com/user-attachments/assets/a09e80c3-ecba-4985-adc1-cdcc57896558)

v:, đọc doc tiếp thì để gửi với get method thì ta phải thêm _method vào

![image](https://github.com/user-attachments/assets/d4934f66-ec72-43f6-a4f8-642b916cedeb)

Và thành công :V, tiến hành gen ra poc rồi gửi cho con bot thôi :">

Payload:

```
<script>
    document.location = "https://0a7b00d0045cccdf81541184006600a5.web-security-academy.net/my-account/change-email?email=abc@gmail.com&_method=POST";
</script>
```

Đó, sở dĩ ko dùng được payload do burp gen ra là vì nó ko hiểu đc ngữ cảnh, nó đang coi như gói đó là POST nhưng thực tế nó đang là get, vì vậy phải làm bằng cơm v:, và vì cái này là GET nên cần j auto submit form :">. ok chứ.

![image](https://github.com/user-attachments/assets/4cb9f5bd-b757-4d21-9813-0805aae97027)

Thành công rồi 

## REFERENCES
[1]. https://laravel.com/docs/5.0/routing#method-spoofing
