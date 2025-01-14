## Challenge 1: Exploiting path mapping for web cache deception
## Challenge 2: Exploiting path delimiters for web cache deception
## Challenge 3: Exploiting origin server normalization for web cache deception
## Challenge 4: Exploiting cache server normalization for web cache deception
## Challenge 5: Exploiting exact-match cache rules for web cache deception

# So sánh hai bài Lab: Web Cache Deception  

| **Tiêu chí**                          | **Lab: Exploiting origin server normalization for web cache deception** | **Lab: Exploiting cache server normalization for web cache deception** |
|---------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Tên bài**                           | Origin server normalization                                            | Cache server normalization                                             |
| **Mục tiêu**                          | Tìm API key của người dùng `carlos`.                                   | Tìm API key của người dùng `carlos`.                                   |
| **Kiến thức cần thiết**               | - Hiểu cách origin server normalize đường dẫn URL.                     | - Hiểu cách cache server normalize đường dẫn URL.                      |
|                                       | - Phát hiện rule cache của thư mục tĩnh.                               | - Phát hiện sự khác biệt trong cách hiểu các ký tự delimiter.          |
|                                       | - Khai thác normalization bởi origin server.                           | - Khai thác normalization bởi cache server.                            |
| **Phương pháp điều tra**              | Sử dụng Burp Suite để gửi các yêu cầu HTTP đến origin server và phân tích phản hồi. | Sử dụng Burp Suite để gửi các yêu cầu HTTP đến cache server và phân tích phản hồi. |
| **Xác định endpoint mục tiêu**        | Đường dẫn: `/my-account`.                                              | Đường dẫn: `/my-account`.                                              |
| **Khám phá delimiter**                | - Sử dụng Burp Intruder để kiểm tra các ký tự delimiter tiềm năng sau `/my-account`. | - Sử dụng Burp Intruder để kiểm tra các ký tự delimiter như `#`, `?`, `%23`. |
|                                       | - Tìm thấy ký tự `?` là delimiter cho origin server.                   | - Tìm thấy ký tự `%23` là delimiter phù hợp với cache server.           |
| **Khác biệt normalization**           | Origin server decode và xử lý các `dot-segment` như `..%2f`.           | Cache server decode và xử lý các `dot-segment`.                        |
| **Quy tắc cache tĩnh**                | Cache áp dụng quy tắc dựa trên tiền tố `/resources`.                   | Cache áp dụng quy tắc dựa trên tiền tố `/resources`.                   |
| **Cách tấn công**                     | - Thêm đoạn `..%2fmy-account` vào đường dẫn `/resources`.              | - Sử dụng `%23` trong URL để khai thác cache server.                   |
|                                       | - Cache server không decode `..%2f`, nhưng origin server decode được.  | - Cache server decode `..%2f` và chấp nhận quy tắc cache.              |
| **Payload khai thác**                 | ```javascript                                                         | ```javascript                                                          |
| `<script>                                                                  | `<script>                                                               |
| document.location="https://YOUR-LAB-ID.web-security-academy.net/resources/..%2fmy-account"</script>` | document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account%23%2f%2e%2e%2fresources"</script>` |
|                                       | ```                                                                    | ```                                                                     |
| **Kết quả**                           | API key được cache và có thể truy cập qua URL đã khai thác.            | API key được cache và có thể truy cập qua URL đã khai thác.            |
