![image](https://github.com/user-attachments/assets/5adb5d88-7a4e-46ff-86e4-736982fd2869)

Do lỗi trong cách triển khai, server dễ bị khai thác bằng cách thay đổi thuật toán từ RS256 (RSA) sang HS256 (HMAC-SHA256), dẫn đến việc có thể sử dụng public key của server như một secret key để giả mạo token.

Ở challenge này ta có thể thấy nó khá giống challenge 7 là ý tưởng đều thay đổi thuật toán kí khác nhưng điểm khác nhau là ở challenge này nó không để lộ public key trên server thì giờ làm sao.

Bước 1: Lấy 2 JWT

+ Đăng nhập bằng tài khoản wiener:peter để có một token hợp lệ.
+ Gửi yêu cầu đến /my-account để lấy JWT hiện tại (có trong cookie session).
+ Đăng xuất và đăng nhập lại, lặp lại quy trình để lấy một JWT khác.

=> Mục đích: Sử dụng hai JWT này để tính toán giá trị n trong public key RSA.

Tiếp theo chúng ta có thể dùng tool của portswigger hoặc tool `rsa_sign2n`

Tool portswigger:

```
docker run --rm -it portswigger/sig2n <token1> <token2>
```
Công cụ này sẽ dựa trên 2 token bạn cung cấp để tính toán giá trị n của public key RSA.

Kết quả đầu ra:
+ Một hoặc nhiều giá trị n.
+ Public key ở định dạng X.509 và PKCS1.
+ Một JWT giả mạo được ký bằng mỗi public key.

Tiếp theo sẽ kiểm tra xem JWT nào hợp lệ:

+ Sử dụng JWT giả mạo (tampered JWT) thay thế cookie session trong Burp Repeater.

Gửi yêu cầu đến /my-account.

+ Nếu nhận phản hồi 200 (truy cập thành công), thì đây là public key đúng.
+ Nếu nhận phản hồi 302 (chuyển hướng đến /login), thử public key khác.

![image](https://github.com/user-attachments/assets/1828c680-7353-40fa-9746-d1bd0bc57d97)

![image](https://github.com/user-attachments/assets/e44f44c0-4e6d-4f0d-9083-4c233813ebaa)

![image](https://github.com/user-attachments/assets/5a46b461-2860-41ae-9087-6f94884d8625)

Như ta có thể thấy thì token 2 sẽ là token không hợp lệ, vì thế public key của token 1 mới đúng.

Bước 3: Tạo symmetric key

Sử dụng public key đã xác định được từ bước trước:

+ Chuyển public key (Base64) vào Burp Suite > Tab JWT Editor Keys > Tạo Symmetric Key mới.
+ Thay giá trị k trong JWK (JSON Web Key) bằng public key của server (ở dạng Base64).

=> Mục đích: Sử dụng public key làm secret key để ký JWT.

![image](https://github.com/user-attachments/assets/eab56350-19c7-4e2a-8ab4-85b2ad36f3e0)

Hiện tại thì có 2 cái và mình đã biết token 1 mới đúng vì thể nên ta phải chọn public key của token 1 là file pem 1.

Tiến hành encode nó bằng base64 để sửa đổi thuật toán kí tiếp theo.

![image](https://github.com/user-attachments/assets/b3610736-d50f-41a9-b7df-9ecbacd267c2)

![image](https://github.com/user-attachments/assets/8932d9a4-36cf-4b92-977e-2c7b98c08401)








