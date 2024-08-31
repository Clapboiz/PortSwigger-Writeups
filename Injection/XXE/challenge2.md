![image](https://github.com/user-attachments/assets/7f579d77-2c84-42a6-9229-47582ff68a9e)

Như challenge trước chỉ là 1 cái hệ quả mà chúng ta có thể làm với xxe thôi (Đọc file, list file trong hệ thống [File Disclosure])

Thì ở challenge này tác giả kêu chúng ta hãy làm xxe dẫn đến hệ quả ssrf đi v:.

![image](https://github.com/user-attachments/assets/e2f9378b-2d35-47e4-bf83-f24abf3c6ed4)

Bạn đang không biết tại sao nó lại là latest chứ gì v:

Quay ngược lại nhé v:.

![image](https://github.com/user-attachments/assets/ec485e54-6616-4446-81a3-f308743d0e73)

Bạn có thấy abc bên request không v:, nó cũng trả về abc bên response luôn đó. Điều này có nghĩa là gì?

Bất cứ điều gì chúng ta nhập bên request thì nó sẽ thực thi và trả về bên response. Ở trường hợp trên tôi load 1 external entity vào thì nó sẽ thực thi và trả về output cho tôi v:.

Tức là latest nó là 1 api của thằng ec2 đó.

Thì giờ ta cứ chui vào url đó xem có gì hot không.

![image](https://github.com/user-attachments/assets/098df068-edcc-4500-a713-0fcb9a00994a)

Nó lại lòi ra thêm dir của url đó.

![image](https://github.com/user-attachments/assets/4f90af0d-5862-4c99-bf35-bb9384b8ac16)

Hãy cứ tiếp tục làm như thế cho đến khi nó vào đc 1 cái api nhé

![image](https://github.com/user-attachments/assets/350adbb4-169d-47a4-b925-eb585e8e9daa)
