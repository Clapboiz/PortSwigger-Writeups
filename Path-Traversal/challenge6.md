![image](https://github.com/user-attachments/assets/c72d7565-69e0-4d22-a74f-dbc13fd00699)

Lần này vẫn ở images.

Ta có thể thấy lần này nó sẽ check đuôi file.

![image](https://github.com/user-attachments/assets/0d63979f-c0f0-406d-b274-55280473752a)

Đó fail.

Chúng ta sẽ lợi dụng `null byte` (null byte characters (%00, \x00)) để bypass

![image](https://github.com/user-attachments/assets/e4246a3c-d9a1-44f8-81b8-2754fddb94db)

Đó như ví dụ trên đó. là lí do tại sao chỉ được thêm vào cuối, bởi khi gặp null byte thì nó sẽ ngưng và chỉ thực hiện phần trước null byte

![image](https://github.com/user-attachments/assets/be0713a0-a5a3-4d67-a657-c11a7bd059e2)

Payload:

```
../../../../etc/passwd%00a.jpg
```

### REFERENCES
[1]. https://www.thehacker.recipes/web/inputs/null-byte-injection
