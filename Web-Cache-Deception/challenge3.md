![image](https://github.com/user-attachments/assets/e4541657-ad14-473f-8869-6d98e190ab69)

Tiến hành khai thác thì ta cứ test thử như các challenge trước thôi 

![image](https://github.com/user-attachments/assets/faab7778-8ff9-4d1f-8088-a23d4f4e58a6)

Ta tiếp tục fuzz xem nó cho phép kí tự đặc biệt nào trong url thì ta thấy `?` sẽ là kí tự hợp lệ. Nhưng lần này nó không cache nữa.

Hmm, tiến hành sử dụng `../` để path traversal xem sao, xem trong quá trình di chuyển nó có cache hay không.

![image](https://github.com/user-attachments/assets/7403f5d4-22ab-4fa1-bfbc-287b6dbc571b)

Lần nó vẫn không cache?

![image](https://github.com/user-attachments/assets/c220a0ff-baee-49b6-91f5-ac528b16c24a)

Nhưng khi tôi đổi thành `resources` thì nó lại được v:, lí do tại sao nhỉ??

Máy chủ chuẩn hóa cả hai URL (/abc/..%2fmy-account và /resources/..%2fmy-account) thành /my-account.

+ Tuy nhiên, chỉ URL bắt đầu bằng /resources có khả năng bị lưu trữ trong bộ nhớ đệm (vì /resources có thể là một thư mục tài nguyên tĩnh với quy tắc bộ nhớ đệm đặc biệt).
+ Bộ nhớ đệm không xử lý URL /abc/..%2fmy-account và sẽ không lưu trữ kết quả từ yêu cầu này.

Đó, thì tiến hành tạo payload và gửi cho victim thôi.

```
<script>document.location="https://exploit-0ac300f704e9d71b8190333601980025.exploit-server.net/resources/..%2fmy-account?wcd"</script>
```

