![image](https://github.com/user-attachments/assets/63bb6a3a-7703-46c5-bff3-4a8d6e4881ef)

![image](https://github.com/user-attachments/assets/e8912573-28cc-42f0-beeb-7e2c85339df9)

Chúng ta có thể thấy được rằng chúng ta không thể khai thác 1 cách bình thường, tức là sẽ theo flow nhờ server nó đọc giùm file /etc/passwd.

Nhưng trong bài này thì nó sẽ thực thi cái dtd mà chúng ta truyền vào và nếu lỗi thì nó sẽ nhả ra, không lỗi thì nó cứ trả về 1 cái gì đó rất chung chung (theo 1 template). Tất nhiên chả có ai nói cho bạn biết điều này đâu :"))). Cùng tôi chứng minh nhé.

![image](https://github.com/user-attachments/assets/6f108b36-1031-4840-9e28-fddc5c26b793)

Đây là khi bạn đưa vào 1 dtd có file không tồn tại đó v:. Nó chui vào folder đó nó tìm v: Và nó đã nói cho chúng ta biết, đây là dấu hiệu giúp chúng ta khai thác, tất nhiên trước đó chúng ta phải test oob attack với burp collaborator rồi và nó thành công rồi nhé.

![image](https://github.com/user-attachments/assets/7648adf8-d2ce-4763-9b30-ee84f11bc49b)

Đây là khi chúng ta đưa vào 1 dtd thực thi 1 lệnh hợp lệ v:, nó cứ báo chung chung như thế, vì thế ta biết được challenge này là via error messages

Tiến hành khai thác và đưa vào dtd lỗi nhé.

![image](https://github.com/user-attachments/assets/e0ce9ee5-2813-49d6-a456-58ee6a7b5a5b)

![image](https://github.com/user-attachments/assets/12d38c14-f745-4cba-9627-504d13ca7dc8)

Đó thành công r nhé V:.

![image](https://github.com/user-attachments/assets/6f5450e3-dc95-4275-a8cc-dee165e99965)

