![image](https://github.com/user-attachments/assets/7a34d49d-883d-4782-8a68-fdf0d766564a)

![image](https://github.com/user-attachments/assets/1902870e-909c-447c-8698-82f13c62210e)

Ta có thể thấy được rằng lần này nó không dùng xml ở trong request nữa rồi :"?. Liệu còn cách nào không nhỉ.

Như ta được biết thì có 1 cách nữa để khai thác xxe đó chính là `XInclude`.

Và tôi cho bạn 1 vài thông tin về `XInclude` nhé:

Một số trang web không trực tiếp nhận dữ liệu XML từ người dùng, mà nhúng các dữ liệu người dùng vào document XML. Điều này khiến kẻ tấn công không thể chỉnh sửa payload XML theo mong muốn.

Ví dụ khi dữ liệu do người dùng gửi được hệ thống kết hợp vào một SOAP backend request, sau đó được xử lý bởi SOAP backend. Nên chúng ta không thể thực hiện tấn công XXE theo các hình thức được đề cập phía trên do không thể kiểm soát nội dung toàn bộ document XML, dẫn đên không thể tự định nghĩa hoặc làm thay đổi tính năng DOCTYPE. XInclude là một giải pháp tốt để thay thế các phương pháp tấn công phía trên, do XInclude là một phần của đặc tả XML cho phép tạo một document XML từ các sub-documents.

SOAP, viết tắt của Simple Object Access Protocol, là một giao thức nhắn tin đặc biệt được thiết kế để kết nối những ứng dụng chạy trên các hệ điều hành khác nhau. SOAP tạo ra một cầu nối mạnh mẽ qua ngôn ngữ XML và giao thức HTTP.

Đó tôi đã sơ qua cho bạn về kiến thức của `XInclude` rồi đó, tiến hành khai thác thôi.

![image](https://github.com/user-attachments/assets/91a3481f-02b1-4c5c-9652-54785ee96ce0)

Payload:

```
productId=<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>&storeId=1
``
### REFERENCES
[1]. https://viblo.asia/p/xxe-injection-vulnerabilities-lo-hong-xml-phan-6-oK9VyQd0VQR
