![image](https://github.com/user-attachments/assets/82a8c3da-1870-4ea1-b66e-26023e81832b)

Challenge này khá giống challenge trước nhưng lần này nó đã giống đa số trường hợp thực tế hơn nó sẽ không ánh xạ các url không tồn tại trên hệ thống, ta tiến hành fuzz phía sau `/my-account` với các kí tự đặc biệt xem nó nhận cái gì 

![image](https://github.com/user-attachments/assets/193330b6-34b0-4c83-9871-c0cc18c884ab)

Tiến hành fuzz thì thấy chỉ có `; và ?` được chấp nhận nhưng thử tiếp thì chỉ có `;` nó được cache. `?` không được có lẽ là vì nó chỉ được chấp nhận bởi origin server mà không được chấp nhận bởi cache server

![image](https://github.com/user-attachments/assets/0e2996d8-6981-4d37-b34d-8005817e9fa6)

Tiến hành khai thác với `;` thôi.

```
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account;wcd.js"</script>
```

![image](https://github.com/user-attachments/assets/a0bcc4d7-62f3-458b-a61b-dc2f86ebb164)

![image](https://github.com/user-attachments/assets/6811db0e-c637-43df-8d71-e08d1a9f83f3)

![image](https://github.com/user-attachments/assets/0d4da1b7-c45b-4bcf-9ad6-381f1c4302a3)

Vậy là thành công
