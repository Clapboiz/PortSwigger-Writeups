![image](https://github.com/user-attachments/assets/b66a0369-e78b-4f3e-b581-08de8449b337)

![image](https://github.com/user-attachments/assets/cc16552d-8149-42d8-b223-26335cc24fe9)

Sau khi test với nháy đơn thì xác định được ứng dụng bị sqli.

![image](https://github.com/user-attachments/assets/276c23ac-c98d-41f9-9684-2fb3b904894c)

Thử câu truy vấn hợp lệ nhưng không có tác dụng thực tế và nó vẫn báo lỗi, tức là khả năng bị sai, có thể là thiếu table.

Thử xem, ví dụ như dbms mssql, sql server xem, select schema table chẳng hạn. Nhưng cho nhanh thì tôi sẽ thử các cái nổi nổi như mysql, oracle nhất.

![image](https://github.com/user-attachments/assets/a14a1663-c0b3-477c-a2cc-4a84e570ed0d)

Đúng thật sau khi thử thì ta biết chắc chắn sqli này là oracle.

Nhưng tại sao phải dùng `||` nhỉ ?? Liệu có thể dùng cái khác không ???. Thì câu trả lời sẽ là có thể. dùng || để như trong trường hợp waf nó chặn union chẳng hạn. Và `||` trong trường hợp này là nó dùng để nối chuỗi mà thì cũng tương đương với mực đích dùng union thôi.

Tiến hành dùng union xem sao nhé.

![image](https://github.com/user-attachments/assets/581ccd39-a4a3-4388-844c-f21c5da5d196)

Đó đã thành công rồi kìa.

2 Payload tương đương

```
'||(SELECT+''+from+dual)||'
'union+select+''+from+dual--
```

![image](https://github.com/user-attachments/assets/6d89c50a-1e7e-409f-964f-0b130eef7373)

Chứng tỏ sqli đã được thực thi.






