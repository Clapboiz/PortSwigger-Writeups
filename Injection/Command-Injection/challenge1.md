## OS command injection, simple case
Đầu tiên đọc challenge thì ta có thể thấy được rằng họ kêu để giải được challenge này thì chỉ cần thực thi lệnh `whoami` để xác định tên của người dùng hiện tại đang thực thi lệnh trong hệ thống

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/89315bee-548d-4666-b807-46860d29799e)

Như họ có mô tả là command injection được thấy ở trong `product stock checker` thì ta cũng thử truy cập vào như 1 user bình thường thì ta có thấy được 1 button `check stock`. Khi ta bấm vào thì ta vào burpsuit và check thử phương thức `POST` mà ta vừa gửi lên.

Thì ta nhìn thấy ở dòng thứ 19, nơi mà command sẽ được thực thi. Và theo em được biết thì ta có thể `inject command` bằng cách sử dụng `; xuống dòng && ||`, etc.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b8d675a2-34f7-4340-8edc-95f05b21e61a)

Bây giờ chúng ta hãy thử inject = cách sử dụng `;` và `whoami` như mô tả challenge.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b88efb37-136c-4e3c-897f-732928c2d841)

Vậy là đã giải thành công challenge này.
