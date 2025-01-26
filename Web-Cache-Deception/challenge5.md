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

![image](https://github.com/user-attachments/assets/0d7d4fbd-bb5a-4e9e-9e40-33e91ca91b18)

![image](https://github.com/user-attachments/assets/eb90e1e5-9c67-4345-9c9c-ce1649e1778c)

Ta có thể thấy được chỉ có dấu `;` thì server nó mới cache. Rồi, bây giờ ta có thể khai thác tiếp.

```
<script>document.location="https://0a7700320423322480df67be00500056.web-security-academy.net/my-account;%2f%2e%2e%2frobots.txt"</script>
```

Sau khi gửi link cho nạn nhân và nạn nhân click vào thì ta truy cập vào thì nó đã cache rồi

![image](https://github.com/user-attachments/assets/3a50dfb0-0841-4ade-b04d-2fd3e7317e9d)

![image](https://github.com/user-attachments/assets/bbbd105b-a22c-4a4f-b601-1f6f0c4cfb03)

Tiến hành copy csrf token thôi và tạo payload csrf thôi.

![image](https://github.com/user-attachments/assets/08449540-9bab-47e0-81f2-5792f293c144)

Thay 2 cái này

![image](https://github.com/user-attachments/assets/3a4b1543-8c06-4a73-8756-e88f517a0b24)

Sau đó gửi lại cho người dùng =)), và thành công rồi
