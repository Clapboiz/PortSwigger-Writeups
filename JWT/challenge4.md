![image](https://github.com/user-attachments/assets/fa49a640-6a0c-4b82-80d4-db3ea7e7bf46)

server đã triển khai sai cơ chế xác thực JWT với header JWK (JSON Web Key). vì vậy ta có thể tự tạo cặp khóa RSA (gồm public key và private key), sau đó tự ký JWT bằng private key của mình. Server sẽ sử dụng public key được nhúng trong phần jwk của JWT header để kiểm tra chữ ký, và vì server không xác minh nguồn gốc của public key, nó sẽ tin tưởng JWT này là hợp lệ.

Sơ qua kiến thức cho bạn hiểu cách mà JWT với JWK header nó hoạt động nhé.

JWK trong header: Một số server cho phép nhúng khóa công khai (public key) vào header của JWT để xác thực chữ ký. Điều này thường được thực hiện thông qua trường jwk trong header.

Vấn đề bảo mật: Server nên chỉ chấp nhận các JWK được lấy từ nguồn đáng tin cậy (ví dụ: từ cơ sở dữ liệu hoặc endpoint được xác định trước). Tuy nhiên, trong lab này, server không kiểm tra nguồn gốc của JWK mà tin tưởng bất kỳ JWK nào được nhúng trong header.

![image](https://github.com/user-attachments/assets/549f3401-9b02-4324-97da-f46eee7ed145)

Trong tab Keys của JWT Editor, bạn tạo một cặp khóa RSA mới (bao gồm private key và public key).

+ Private key dùng để ký (sign) JWT.

+ Public key sẽ được nhúng vào header của JWT để server sử dụng cho việc xác thực.

![image](https://github.com/user-attachments/assets/f88a781c-e632-4e60-b1eb-c3aafec642d2)

Nhúng JWK vào header:

+ Trong tab "Json Web Token", bạn chọn Attack -> Embedded JWK.
+ Thao tác này sẽ thêm trường jwk vào header JWT, chứa public key vừa tạo.

![image](https://github.com/user-attachments/assets/fc3ac803-448a-405f-9821-a8ef2445cb97)

Dùng private key để ký lại JWT, tạo ra một chữ ký hợp lệ dựa trên public key của bạn.

![image](https://github.com/user-attachments/assets/930314d0-b476-4aae-a43f-ea283f07d1c2)

![image](https://github.com/user-attachments/assets/7445590d-7376-4714-9cc9-4e0dff559de4)

Vậy là thành công rồi nhé v:
