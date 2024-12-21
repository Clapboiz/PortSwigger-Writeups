![image](https://github.com/user-attachments/assets/6c125014-86bc-4112-8e42-6fa129f50753)

Trong bài lab này, bạn sẽ khai thác một lỗi bảo mật liên quan đến việc sử dụng JWT (JSON Web Tokens) trong xác thực người dùng. Cụ thể, lỗi liên quan đến việc lấy khóa công khai (public key) từ một URL không đáng tin cậy trong trường jku (JSON Web Key Set URL) trong header của JWT. Cơ chế này cho phép JWT chỉ ra URL chứa JWKS (JSON Web Key Set) để server có thể lấy khóa công khai từ đó, nhưng vấn đề là server không kiểm tra xem URL đó có thuộc miền đáng tin cậy hay không.

Sơ qua cho bạn 1 vài kiến thức lí thuyết về cách thức hoạt động của lỗ hổng

Trường jku trong JWT:
+ JWT có thể chứa trường jku (JSON Web Key Set URL) trong header, cho phép server lấy public key từ một URL mà token cung cấp.
+ Thông thường, URL này sẽ trỏ tới một endpoint JWKS được server tin cậy để lấy khóa công khai.

Lỗi bảo mật:
+ Trong bài lab này, server không kiểm tra xem URL trong trường jku có thuộc miền đáng tin cậy hay không. Điều này có nghĩa là bạn có thể chỉ định một URL của server của bạn (hoặc một máy chủ bên ngoài) và server sẽ tải khóa công khai từ đó mà không xác thực nguồn gốc.
+ Bạn có thể lợi dụng lỗ hổng này bằng cách tạo một URL chỉ trỏ đến máy chủ của bạn, nơi bạn có thể cung cấp khóa công khai (public key) của chính mình để ký lại JWT.

![image](https://github.com/user-attachments/assets/3b075917-36b1-45c0-b04a-9ab69c9e3915)

![image](https://github.com/user-attachments/assets/192d56d2-7ea7-41ce-bd28-28f29bfe005e)


```
{
    "keys": [
{
    "kty": "RSA",
    "e": "AQAB",
    "kid": "01237197-a505-4b47-ba72-7030e765df1b",
    "n": "sqs9ncNkWuZaLWahSPm7ZL19_KYpAGZpo07R-1SqxjbDwpwLDqpmvklcr3B2togQcfOfa599ipC4P9q3Mig_FvBr86ntfOzTvb1io_c17tPB4RkoCg3iUed9RoM-7u00Pg40Am_yFew9WTV4qxuvG4OmIIKS9EhuYHObrclGY9-p4Kv4xAlQ7AsRd5CSyBPQ5cxQR70KocEC2zFkRA_HG7XbXZJHAamN35MloMeq9oZf7uPnRSYKzXbZUYHwLRMqw_itQJz25RDRKBTOvncb-EMP5u8FE_Vptegp4bw7uz2uX2e4eO84FbVXDkL03UOxzvqjy5nidP7D1xc-SBGSBw"
}
    ]
}
```

![image](https://github.com/user-attachments/assets/75a9c1f9-97e8-4af0-8114-4d02bb53a2e9)

Sau khi chỉnh sửa JWT, bạn sử dụng private key của mình để ký lại JWT.

Chọn Sign trong editor và hoàn tất việc tạo ra token mới.

![image](https://github.com/user-attachments/assets/3ee6b79d-1733-44e2-a63f-1c31e412e657)

Copy JWT mới đã được ký và gửi lại đến server để truy cập trang quản trị /admin.

Do server không kiểm tra tính hợp lệ của URL trong trường jku và không xác minh nguồn gốc của khóa công khai, nó sẽ tải khóa công khai từ URL mà bạn chỉ định (máy chủ của bạn).

![image](https://github.com/user-attachments/assets/fdc35c6a-962e-4932-9a36-c57a84b85dd2)

Thành công
