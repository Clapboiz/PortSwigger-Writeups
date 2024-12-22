![image](https://github.com/user-attachments/assets/af297625-c482-43b0-b5d4-ee03c5405261)

![image](https://github.com/user-attachments/assets/d0530a60-4e19-4af7-b1fb-ab9e6e90ffe8)

Ở challenge này thì qua quá trình recon ta biết được tồn tại file `jwks.json` trên server.

Lỗ hổng algorithm confusion xảy ra khi server không xử lý đúng cơ chế kiểm tra thuật toán (algorithm) trong JSON Web Token (JWT). Cụ thể, nếu server hỗ trợ nhiều thuật toán để ký và xác thực JWT, nhưng lại không kiểm tra hoặc xử lý cẩn thận, kẻ tấn công có thể đánh lừa server sử dụng một thuật toán khác để xác minh chữ ký, dẫn đến bypass xác thực.

Server sử dụng RSA để ký và xác minh JWT (thuật toán mạnh mẽ, bất đối xứng).

Tuy nhiên kẻ tấn công có thể lợi dụng để bypass việc kiểm tra này bằng cách lừa server và khi có được thông tin public key thì kẻ tấn công có thể đổi thuật toán khác để giả mạo trong trường hợp này attacker làm như sau:

JWT cho phép nhiều thuật toán ký (signing algorithms). Hai thuật toán phổ biến:

HS256: Sử dụng khóa đối xứng.
RS256: Sử dụng cặp khóa RSA (khóa riêng ký, khóa công khai xác thực).

Trong tấn công này, bạn sẽ thay đổi thuật toán ký từ RS256 sang HS256, lợi dụng việc server không kiểm tra kỹ thuật toán. Sau đó, sử dụng khóa công khai của server (thay vì khóa bí mật) để giả mạo token hợp lệ.

![image](https://github.com/user-attachments/assets/43a7a5af-5a35-4903-93d4-15684c6f1706)

Tiến hành copy public key này và chuyển sang dạng `PEM`

![image](https://github.com/user-attachments/assets/fd365b30-aeab-4f8f-adc9-ac5e1d9109be)

Tiến hành encode với base64 để chuẩn bị inject.

![image](https://github.com/user-attachments/assets/374dca4d-1d52-4e58-a480-31924a471fd3)

Tiến hành inject vào trường K.

![image](https://github.com/user-attachments/assets/db2acfff-34bc-4885-b499-6a2fc112da27)

Nhưng cách này vẫn đang không được, tôi chả hiểu kiểu gì luôn.

Tiến hành làm bằng jwt tool thôi.

```
python .\jwt_tool.py eyJraWQiOiJhYzY5YjI3NC1hN2ZjLTRiY2UtOGVkOS1lZjRkNjg1M2VkN2YiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTczNDg2NzQyNCwic3ViIjoid2llbmVyIn0.kWEPdcWaB7eFUM05Hr8sZtKdm1OMWlyXGD5O3FseD4_v4xu5PH647XU0q3k4NeaiKgDkZrGxxn8zzDvrYtkbg08shhaVhZZlBr7GzDw6_BhwuwGPOwKPEceCLT7lpleG3mXlOCBoshHcQydlpDNOgatMOYSK253iA4eve0zwsliiyCg_dqfmDPE6ilaT-ACQVfdXVw4W3KEcHBrsl2KIXDtLItuBVHiFjfCRKY_CzF5oY811vis7OjB22LQ1EXBXth4ykHeYYD0I6wXrVEzFzsXIRxJuN-x2DQUhoo1RtVM_EtcZ7M9FXA-gYQDFtyvPMnxNv4WkWvJpn97PvxpMAw -X k -pk .\Test.pem -I -pc sub -pv administrator
```

-X k: Yêu cầu sử dụng khóa ký (key manipulation mode).

-pk .\Test.pem: Chỉ định file chứa public key (Test.pem), được sử dụng để tạo chữ ký giả mạo trong quá trình đổi thuật toán từ RS256 sang HS256.

-I: Tùy chọn này kích hoạt chế độ interactive, cho phép bạn chỉnh sửa nội dung JWT trước khi ký lại.

-pc sub: Chỉ định chỉnh sửa trường sub trong payload.

-pv administrator: Thay giá trị của trường sub thành administrator.

![image](https://github.com/user-attachments/assets/4cad86b8-a147-40cd-a199-0b6b55fd2f19)

Vậy là thành công, à lưu ý phải copy public key dưới dạng pem trước nhé.

![image](https://github.com/user-attachments/assets/7c4746fc-82cb-438e-9747-b6cbb9cfcaeb)

Xong v:
