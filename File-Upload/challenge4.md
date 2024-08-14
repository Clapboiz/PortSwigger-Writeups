![image](https://github.com/user-attachments/assets/cc407db8-dcab-4905-a68c-42af96146bdf)

![image](https://github.com/user-attachments/assets/b2c7dde8-ab0e-4523-a5c6-42fce340503d)

Ta có thể thấy rằng challenge này nó đã dùng black list, nó không cho up file thực thi lên v:.

Liệu còn cách nào không?

### CÁCH 1
Chợt nhận ra mod php nó có thể xử lí các dạng đuôi file như `.php, .phar, .phtml`.

![image](https://github.com/user-attachments/assets/e6d9fdac-efd1-4dd6-acb5-e1f97a3e4aee)

Có vẻ như thành công.

![image](https://github.com/user-attachments/assets/34c90087-4af7-40b7-9d62-776a08c627eb)

![image](https://github.com/user-attachments/assets/ffb1bd0c-4d72-4400-93ca-b248d3b81712)

Done!

### CÁCH 2
Chúng ta có thể chỉnh sửa .htaccess không v:??

![image](https://github.com/user-attachments/assets/589573f6-914f-4303-8a37-d87340263588)

Đó chúng ta chỉnh như thế, giờ ta có thể upload file có đuôi .clap được rồi, mod php lần này nó sẽ hiểu là file thực thi tương tự như `.php`.

![image](https://github.com/user-attachments/assets/610b51b6-e568-4039-808d-f4f5489c1d0c)

![image](https://github.com/user-attachments/assets/c8142b5a-3aa7-46b9-bb0d-914e45dc14a0)

Done !
