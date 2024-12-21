![image](https://github.com/user-attachments/assets/3e133245-2dc5-458e-ab04-1f2c5209211b)

Trong bài lab này, lỗ hổng bảo mật liên quan đến việc sử dụng JWT (JSON Web Tokens) để xác thực người dùng, cụ thể là việc sử dụng trường kid (Key ID) trong header của JWT. Trường này cho phép server xác định khóa công khai nào sẽ được sử dụng để xác minh chữ ký của JWT. Tuy nhiên, lỗ hổng xảy ra khi server không kiểm tra đầy đủ các ký tự trong kid, dẫn đến việc có thể khai thác path traversal để truy cập vào các tệp không được phép.

Sơ qua kiến thức lí thuyết về cách thức hoạt động của lỗ hổng

+ Trường kid trong header của JWT chỉ định ID của khóa mà server sẽ sử dụng để xác minh chữ ký của JWT. Thông thường, kid sẽ trỏ tới một khóa cụ thể trong cơ sở dữ liệu khóa của server.
+ Nếu server không kiểm tra hợp lệ các giá trị trong kid, kẻ tấn công có thể sử dụng kỹ thuật path traversal để chỉ định đường dẫn đến một tệp khóa trên hệ thống file của server mà không bị kiểm tra, từ đó có thể lấy khóa không mong muốn.

Tiến hành modify trường kid trỏ về `dev/null` xem sao nhé. /dev/null là một "thiết bị" đặc biệt trên hệ thống Unix/Linux, hoạt động như một "hố đen". Bất kỳ dữ liệu nào ghi vào đây sẽ bị bỏ qua, và nếu đọc từ nó, nó luôn trả về nội dung trống.

![image](https://github.com/user-attachments/assets/46fc5bae-890a-4553-a6d2-3d2326dcf7b5)

Tại sao lại chọn null byte (\x00, AA==) làm key?

+ Đơn giản và hiệu quả: Null byte là một giá trị đặc biệt nhưng hợp lệ, và dễ dàng được hệ thống chấp nhận khi ký JWT.
+ Đồng nhất với dữ liệu rỗng: Khi server đọc từ /dev/null, nó nhận về nội dung trống. Null byte (\x00) thường được sử dụng để "phỏng đoán" giá trị này, vì một số hệ thống xử lý giá trị rỗng giống như null byte.
+ Bypass ký tự đặc biệt: Null byte (\x00) rất đơn giản và ít bị chặn bởi các hệ thống lọc hoặc xử lý.

![image](https://github.com/user-attachments/assets/2354742f-10a5-4927-b47a-7ef813c32a79)
