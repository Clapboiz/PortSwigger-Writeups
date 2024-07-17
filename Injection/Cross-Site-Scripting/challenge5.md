![image](https://github.com/user-attachments/assets/4d9c5695-9d6f-4466-ac8e-9c21303b985d)

Ta có thể thấy tại challenge này thì nó filter khá cùi. Ta có thể thấy được rằng nó `returnPath=/post`. Nhưng value `/post` có thể bị thay đổi và dường như nó gắn với nút back nhưng bằng 1 cách nào đó mà dev nó code lên luôn cả url :")). ẩn thì không ẩn mà lại show ra. Dơ mặt cho hacker đấm.

![image](https://github.com/user-attachments/assets/66485182-0f4c-4091-8288-6b01e5d77732)

Thì ta hãy thử sửa xem thế nào.

Thì ta có thể thấy được rằng đây là `dom base xss` vì thế ta cứ thử test vài payload xem sao.

![image](https://github.com/user-attachments/assets/e40b72c2-51bf-4591-b18b-2cf10d2a97c5)

![image](https://github.com/user-attachments/assets/573abad5-e33b-40a2-8779-7e295cc468e6)

Đều không được :")

![image](https://github.com/user-attachments/assets/4c1c1c60-2ee2-40c6-a998-59f96bda189d)

Ta có thể đoán được 1 số cách attack khi inject lên url thì ta có thể dùng `url scheme js` và `javascript:` là 1 trong số cách đó. Vì thế nên ta thành công attack.

Payload:

```
javascript:alert(1)
```
