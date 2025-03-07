![image](https://github.com/user-attachments/assets/5adf8a32-d717-4648-9878-4ca7dd0d0058)

Tiến hành fuzz các kí tự đặc biệt xem có chuyện gì xảy ra không?

```
!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

![image](https://github.com/user-attachments/assets/48d2a6da-c389-47b4-9000-2ecff6f59390)

Thì ta biết được nó bị lỗi, tiến hành thu hẹp lại.

![image](https://github.com/user-attachments/assets/87ef1268-03d8-4f43-a9ac-fa574f13b289)

![image](https://github.com/user-attachments/assets/5d2b8ac3-ead4-4e90-bc42-98de6ccfe600)

khi ta nháy đơn thì nó đã bị lỗi, tuy nhiên 2 nháy vẫn tiếp tục bị, thì ta có thể đoán được rằng dường như nó k phải sqli, tại vì nếu như sqli thì nó đã đóng lại và đây sẽ là 1 truy vấn hợp lệ.

![image](https://github.com/user-attachments/assets/a7bfd5e5-446b-49eb-b54b-4e15c53a47fd)

Thôi khỏi đoán nữa, nó đã thông báo ra luôn đây là mongodb rồi.

SQL sử dụng cú pháp truy vấn có cấu trúc, và việc chèn mã thường liên quan đến việc đóng chuỗi và thêm các điều kiện logic.

NoSQL làm việc với cấu trúc dữ liệu dạng key-value hoặc document, và việc chèn mã phải tuân theo cú pháp của JavaScript hoặc JSON, bắt buộc phải có ký tự hợp lệ: Vì NoSQL làm việc với các giá trị cụ thể (chuỗi, số, boolean), nên các giá trị như '' (chuỗi rỗng) hoặc Gifts'' (chuỗi không hợp lệ) sẽ gây ra lỗi.

![image](https://github.com/user-attachments/assets/45946551-47cc-45bc-8b23-d0c37f201617)

Vì thế nên bạn có thể thấy được khi ta 2 nháy thì nó vẫn có lỗi

![image](https://github.com/user-attachments/assets/ebd89695-0c98-49c2-bd36-90400662ac7d)

Và chỉ khi 





