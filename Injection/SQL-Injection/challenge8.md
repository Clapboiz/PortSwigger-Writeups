![image](https://github.com/user-attachments/assets/e5a0a786-4936-4309-a9c3-dfc6e91f2b5d)

Ở challenge này thì cũng khá giống challenge 7 nhưng ở đây thì nó bắt phải có chuỗi mà nó cung cấp trong câu query.

![image](https://github.com/user-attachments/assets/7bc79179-ec11-4f98-8198-306096ec2ab5)

![image](https://github.com/user-attachments/assets/6a7e9ca7-90ca-4d49-847b-694f751e2e26)

Ta xác định được có 3 cột trong câu query.

![image](https://github.com/user-attachments/assets/60a9d052-3c88-4a2c-9b5b-67cbab88bba7)

Tại sao lại không được nhỉ??. 

Thay thế từng NULL trong truy vấn bằng một chuỗi ngẫu nhiên do lab cung cấp, ví dụ 'du7CFR'.

Nếu có lỗi 500, chứng tỏ cột đó không hỗ trợ dữ liệu dạng chuỗi.

Khi tìm được cột trả về 200 OK, tức là cột đó hỗ trợ chuỗi.

Tiếp tục xem sao.

![image](https://github.com/user-attachments/assets/3a71dcc5-ba69-4f20-b48b-fd3e39c9f383)

Vậy là đã giải thành công.
