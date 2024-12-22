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

Nhưng bằng cách này thì không thể kí được tôi không hiểu tại sao, đọc 1 vài tài liệu thì nó kêu là do null byte, nhưng mà tôi nghĩ do burp của tôi phiên bản thấp quá, tại vì tôi thấy người ta vẫn kí được bình thường. Và tôi cũng đã sử dụng kí bằng empty key, jwt.io nhưng đều không được, ai biết thì có thể cho tôi biết với nhé :<<<

Thôi thì bây giờ chúng ta dùng jwt_tool để tạo payload phù hợp nhé.

```
python .\jwt_tool.py eyJraWQiOiI0YWIzMTE0ZS1kMjBlLTRjYWItYTMwOS05M2Q1OTI1MWY4NjUiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTczNDg0NDUyOCwic3ViIjoid2llbmVyIn0.7_Lcb_SxXBOOyrpL53wAGgQboLLWT3Jm90varKOjdaU -I -hc kid -hv '../../../dev/null' -pc sub -pv administrator -S hs256 -p ''
```

Thì giờ tôi giải thích sơ qua cho bạn hiểu nhé.

-I: Kích hoạt chế độ "Injection Mode" để sửa đổi hoặc chèn dữ liệu.

-hc kid: Header Claim (hc) được sửa đổi là kid.

-hv '../../../dev/null': Giá trị (hv) chèn vào kid là '../../../dev/null'.

Đây là một kỹ thuật tấn công bằng cách trỏ kid đến một file không hợp lệ nhằm bỏ qua khóa ký.
+ -pc sub: Payload Claim (pc) được sửa đổi là sub.
+ -pv administrator: Giá trị mới (pv) của sub là "administrator".

Mục đích là nâng quyền từ "wiener" thành "administrator".
+ -S hs256: Chỉ định thuật toán ký là HS256.
+ -p '': Chỉ định khóa bí mật (secret) là một chuỗi rỗng ('').

![image](https://github.com/user-attachments/assets/7d04ad0b-f409-4e88-a9c8-9491179c81ec)

![image](https://github.com/user-attachments/assets/17681da6-4d21-44af-a07b-67543d705417)

![image](https://github.com/user-attachments/assets/5976cf3e-472b-4da0-88f2-22e7205d7207)

Vậy là đã thành công rồi nè.
