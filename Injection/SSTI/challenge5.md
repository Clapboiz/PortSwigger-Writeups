![image](https://github.com/user-attachments/assets/a968123c-5b28-4bb7-a77c-5b3ea2900f01)

![image](https://github.com/user-attachments/assets/4bbfc42d-beb1-42f8-b265-002df405a766)

Tiến hành đăng nhập với thông tin mà lab cung cấp và tiến hành fuzz nó với các kí tự đặc biệt thì ta biết được nó dùng `django template`.

Đọc docs thì ta biết được format của django là `{% %}`, và yêu cầu của challenge này là leak secret.

Mà để leak secret thì làm sao v:., làm sao biết nó ở đâu  mà leak

Tìm trên mạng thì biết được `{% debug %}` để leak info, tiến hành thử xem

![image](https://github.com/user-attachments/assets/23df7535-fac0-41f2-aa6e-4f126212a4ef)

Bạn thấy đấy hiện tại nó có 1 object là product

![image](https://github.com/user-attachments/assets/04de2c6b-f7ef-4f4c-85ce-4e1d1dc72e3c)

Nhưng khi đẩy payload `{% debug %}` vào để nó leak info thì nó lại xuất hiện 1 object mới đó là `settings`.

Và theo như tôi tìm hiểu thì các secret trong django mặc định nó sẽ được lưu ở biến `SECRET_KEY`. Vậy thì tiến hành đẩy payload vào thôi 

![image](https://github.com/user-attachments/assets/f7a598e6-b07c-47a1-af38-dddb490dd281)

![image](https://github.com/user-attachments/assets/d3e5b899-9ae1-4f0f-8125-109da6b299a0)

Vậy là thành công.

Payload:

```
{{ settings.SECRET_KEY }} 
```
# REFERENCES
[1]. https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#django-templates

[2]. https://dev.to/ashraf_zolkopli/decoupling-django-secret-key-65d
