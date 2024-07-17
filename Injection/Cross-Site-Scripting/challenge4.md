![image](https://github.com/user-attachments/assets/61f54cea-b570-41c3-bfe2-ae26c51a16ca)

Ta có thể thấy lần này nó query kiểu khác. Tá có thể thấy được dường như có lỗ hổng trong này. Không có bất kì filter gì hết, vì thể ta có thể inject vào. 

![image](https://github.com/user-attachments/assets/979e4b75-73c2-436c-911d-5e85fa2f98cd)

Tuy nhiên khi ta thử tag js vào thì dường như nó đã bị filter. Giờ ta thử các tag khác nhé, tại vì có rất nhiều tag có thể chạy js mà.

![image](https://github.com/user-attachments/assets/371657b8-63b0-4948-ae1b-e6e585b3bb67)

Và đúng như giả thuyết của ta, đã exploit thành công.

Đây là payload:

```
<img src=x onerror="alert(1)">
```

![image](https://github.com/user-attachments/assets/90e5d5a8-8d0e-451b-8fe6-ac0100c1403b)
