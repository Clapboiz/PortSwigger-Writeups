![image](https://github.com/user-attachments/assets/9e70dec3-0006-4b2e-9c9a-499ed5fbb867)

![image](https://github.com/user-attachments/assets/26aae7cd-d6a2-44b5-b387-a86850c5c837)

Ta thử chèn Sqli via xxe thì thấy được rằng nó đã bị waf chặn.

Vậy là sao ta?, thử encode xem sao. nhưng vấn đề là encode kiểu gì ???

XML là một ngôn ngữ đánh dấu được sử dụng để lưu trữ và truyền tải dữ liệu. Một trong những tính năng của XML là hỗ trợ các ký tự đặc biệt được mã hóa dưới dạng hex entities. Vậy nên phải tùy trường hợp nào thì dùng encode đó, chứ k phải là cứ url, base64 đâu nhé. ví dụ như url thì url encode, HTML Entities Encoding sử dụng khi làm việc với HTML và cần hiển thị các ký tự đặc biệt.

Thì đây là câu trả lời.

Ta có thể dùng link ở dưới để encode.

![image](https://github.com/user-attachments/assets/d6970cb9-b9ce-41a1-af46-2b296166c9b3)

Đó thì ta đã có đc payload bị encode.

![image](https://github.com/user-attachments/assets/69e2b9bd-ae89-4e56-89fa-1c97b4598ba6)

Cách thứ 2 là chúng ta sẽ dùng extension burp.

![image](https://github.com/user-attachments/assets/dcb54e48-969e-4c95-88cb-a413aa447eec)

![image](https://github.com/user-attachments/assets/9b8d8bf5-5d06-47b3-b962-3d82f0971cc7)

![image](https://github.com/user-attachments/assets/28f8ef64-1757-47aa-b152-08fa4dfae453)

Vậy là thành công rồi nhé.

## REFERENCES
[1]. https://coderstoolbox.net/string/#!encoding=xml&action=encode&charset=us_ascii
