![image](https://github.com/user-attachments/assets/59c5ab64-2b70-4555-ac1a-103631a1ddde)

Tiến hành view thì thấy param `message` trên url và value của nó là `Unfortunately%20this%20product%20is%20out%20of%20stock` lại được render ra UI của web.

Tiến hành XSS thử xem thì thấy không được.

Tiếp theo ta fuzz thử các template xem có gì bất thường không.

![image](https://github.com/user-attachments/assets/00b955b7-e3fb-4bed-aafc-d7888cb2447c)

Thì biết được nó sử dụng ERB template.

Tiến hành ném payload vào xem.

![image](https://github.com/user-attachments/assets/187ef6cf-f026-46c0-a78f-41122e7ea7af)

Nó ở path này, tiến hành đẩy payload vào cho nó xóa file.

![image](https://github.com/user-attachments/assets/73bfe4a9-9d45-4950-bde4-ab0e96dd5bfb)

Vậy là thành công.

Payload: 

```
<%= system('rm -rf /home/carlos/morale.txt') %>
```
