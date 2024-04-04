# OS command injection
## OS command injection, simple case
Đầu tiên đọc challenge thì ta có thể thấy được rằng họ kêu để giải được challenge này thì chỉ cần thực thi lệnh `whoami` để xác định tên của người dùng hiện tại đang thực thi lệnh trong hệ thống

![image](https://gist.github.com/assets/112185647/9d2ddd46-bd37-4a91-9836-e1eee8645b4e)

Như họ có mô tả là command injection được thấy ở trong `product stock checker` thì ta cũng thử truy cập vào như 1 user bình thường thì ta có thấy được 1 button `check stock`. Khi ta bấm vào thì ta vào burpsuit và check thử phương thức `POST` mà ta vừa gửi lên.

Thì ta nhìn thấy ở dòng thứ 19, nơi mà command sẽ được thực thi. Và theo em được biết thì ta có thể `inject command` bằng cách sử dụng `; xuống dòng && ||`, etc.


![image](https://gist.github.com/assets/112185647/67bf31d2-d30f-485c-b418-aec44ff11c32)

Bây giờ chúng ta hãy thử inject = cách sử dụng `;` và `whoami` như mô tả challenge.

![image](https://gist.github.com/assets/112185647/e340fb94-1519-409d-baa3-dd96c0c9d9df)

Vậy là đã giải thành công challenge này.
