![image](https://github.com/user-attachments/assets/96b840d4-139d-48bb-a7f6-53e412de5703)

![image](https://github.com/user-attachments/assets/e4d34737-c4d4-426e-9acf-5d64f3f8aee4)

Chỉ có png, jpg mới được up lên. Chúng ta thử sửa content-type xem sao nhé.

![image](https://github.com/user-attachments/assets/08a51bda-2a62-428e-8c47-b6816ff9cdad)

Và chúng ta đã thử hết các cách ở trên nhưng vấn k hiệu quả, có thể do dev filter bằng cách check extension. Cho nên chúng ta hãy nghĩ thử xem có cách nào chèn extension .png ở cuối mà vẫn thực thi php được không.

Câu trả lời là chúng ta có thể sử dụng kí tự null byte `%00`.

![image](https://github.com/user-attachments/assets/44b114ba-0092-4ec1-91a2-a65d11a157d4)

![image](https://github.com/user-attachments/assets/110d7142-5a37-4841-ac0f-9508790f92a1)

Nhưng tại sao vẫn không vào được v:, Đó là vì kí tự null byte nó sẽ kết thúc chuỗi tại đó vì thế file chúng ta thực sự up lên server là `file-upload.php chứ không phải là file-upload.php%00.png` nên chúng ta chỉ cần sửa.

![image](https://github.com/user-attachments/assets/170c0ada-5b39-474f-a917-d71a0bc8e74f)

![image](https://github.com/user-attachments/assets/83c7ba52-255a-4bb5-a8cb-1c4269057ade)

Đó là thành công rồi v:
