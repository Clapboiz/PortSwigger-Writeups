![image](https://github.com/user-attachments/assets/c3a78ea2-0991-47cb-b98e-999bc873b16c)

+ ?: Được sử dụng để bắt đầu query string, phần chứa các tham số gửi tới server. Ví dụ:

```
/my-account?param=value
``` 

=> Server thường không lưu trữ cache cho các URL có query string vì chúng đại diện cho các tham số động.

+ #: Chỉ được xử lý ở phía client (trình duyệt) và không bao giờ được gửi tới server. Ví dụ:

```
/my-account#section
```

=> Phần #section sẽ không xuất hiện trong request gửi tới server.

+ ;: Trong một số cấu hình server, ; được sử dụng làm phân cách để thêm thông tin phụ (extra path parameters). Ví dụ:

```
/my-account;extra-data
```

=> Một số server có thể bỏ qua phần sau dấu ; hoặc xử lý toàn bộ URL mà không nhận ra đây là dữ liệu bổ sung.

![image](https://github.com/user-attachments/assets/70ac6ba3-76b2-4ce6-99ca-fedf8247bd9e)

Tiến hành vào check thì có thể thấy được rằng khi người dùng truy cập vào robots.txt thì sẽ bị cache.

thì ta sẽ lợi dụng điều này để khai thác.

![image](https://github.com/user-attachments/assets/eb90e1e5-9c67-4345-9c9c-ce1649e1778c)

Rồi đã khai thác được

