![image](https://github.com/user-attachments/assets/e84b1f15-9318-460d-98fb-8d8a98e78e14)![image](https://github.com/user-attachments/assets/33ab9200-592c-4590-bc80-86c7044af08e)

![image](https://github.com/user-attachments/assets/5118957d-450f-4df5-a351-5d612ad349fc)

Khi ta nháy vào thì nó đã bị lỗi, bạn có thể thấy được câu truy vấn của nó luôn đó, thì tiến hành giờ ta test comment luôn nhé.

![image](https://github.com/user-attachments/assets/0add179c-12b1-4314-b447-5f6cd619ad5c)

Chứng tỏ web này bị sqli.

![image](https://github.com/user-attachments/assets/17a9722f-b77f-4c2c-a3e4-10368806e1d4)

Bạn có thể thấy khi tôi chèn sqli or 1=1 vào để nó luôn đúng thì nó thành công nhưng chả nhả ra data cho chúng ta. Những cái data phía dưới chỉ là data bình thường thôi nhé, còn data mà bị sqli thường nó sẽ trả về dưới dạng text nhìn đặc trưng lắm.

Nên ta biết được đây là blind sqli 

![image](https://github.com/user-attachments/assets/59a891f4-654f-4f17-8319-29a534ebd336)

```
SELECT IF(1=1, (SELECT table_name FROM information_schema.tables), 'a')
```

**IF(condition, true_value, false_value)**

Nếu 1=1, truy vấn sẽ thực hiện SELECT table_name FROM information_schema.tables, tức là lấy danh sách các bảng trong database.

Nếu điều kiện sai, nó sẽ trả về 'a'.

=> Vì 1=1 luôn đúng, câu truy vấn sẽ cố lấy danh sách bảng.

Ta có thể thấy nó đang trả lỗi đến inf, liệu rằng nó đang giới hạn kí tự??

![image](https://github.com/user-attachments/assets/7fd03b30-4089-409b-acb0-2b80fc94a217)

Đúng thật, nó đang giới hạn số kí tự :"))

Vậy còn cách nào không :"??

Ta sử dụng CAST() nhé, CAST() là một hàm trong SQL dùng để chuyển đổi kiểu dữ liệu. Nó giống như việc bạn chuyển đổi kiểu dữ liệu trong lập trình, ví dụ:

+ Trong Python: int("123") để chuyển "123" thành số nguyên.
+ Trong C/C++: (int) 3.14 để chuyển float thành int.
+ Trong SQL: CAST('123' AS INT) để chuyển chuỗi "123" thành số.

Tại sao hacker dùng CAST() khi khai thác SQL Injection?

Trong Blind SQL Injection, hacker thường không thấy dữ liệu trực tiếp mà chỉ có thể dựa vào phản hồi của server (ví dụ: có lỗi hay không).

Nếu hacker cố gắng lấy dữ liệu bằng cách dùng CAST() để ép kiểu sang số, thì:

+ Nếu dữ liệu là số, không có lỗi xảy ra.
+ Nếu dữ liệu là chữ (text), SQL sẽ báo lỗi → giúp hacker biết rằng có dữ liệu tồn tại.

![image](https://github.com/user-attachments/assets/6625fa66-a113-4255-8274-eaf2a27c8ab9)

Đấy nó không có lỗi gì nhé, tức là query của chúng ta bình thường, bây giờ hãy tiến hành khai thác.

![image](https://github.com/user-attachments/assets/8e959ea0-7098-439e-a8a2-26bea8940872)

Nó vẫn báo lỗi, nó bảo là chỉ trả về 1 dòng thôi. Đơn giả, chúng ta chỉ cần limit nó lại là đc.

![image](https://github.com/user-attachments/assets/eadadc91-852b-4f6c-8264-4103a1c53f9f)

Đó tự nhiên nó nhả ra tên username luôn r :">

Vậy giờ thì lấy passwd thôi.

![image](https://github.com/user-attachments/assets/1048adeb-d95e-4feb-baac-40ddfb5aefa2)

Vậy là thành công nhé.

Payload:

```
' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

![image](https://github.com/user-attachments/assets/7510ae2b-dcf6-43d9-98df-decd9907ef98)
