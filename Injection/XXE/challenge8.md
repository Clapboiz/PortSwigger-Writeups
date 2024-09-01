![image](https://github.com/user-attachments/assets/90a0c929-b6c9-43a1-aeba-c0c5a6ec8da7)

![image](https://github.com/user-attachments/assets/55b9d87d-a1b4-4679-a783-691f4a3b1e8d)

Sau khi up 1 bài post lên thì ta để ý rằng avatar mà ta vừa mới up lên nó đã hiện ngay ở đây

![image](https://github.com/user-attachments/assets/6d1b7801-5d47-48de-9ed8-303ec377d0c3)

Tiến hành open link in new tab để tí ta có thể khai thác nó.

Rồi bây giờ gác lại và tiến hành xem gói tin đó xem sao nhé.

![image](https://github.com/user-attachments/assets/7e79a24c-2722-4ab7-a23b-bf6cbe6cd936)

Ta có thể thấy khi ta up cái gì lên nó đều k trả về gì hết, và điều này dẫn đến ý nghĩ là cứ up đi, nó sẽ thực thi. Nhưng vấn đề là vào đâu để biết nó đã thực thi?? Ta cứ vào cái link avatar là biết ngay á mà.

Rồi bây giờ làm sao để khai thác đây, tại vì challenge này nó chỉ lấy định dạng của image chứ nó không chấp nhận bất cứ định dạng nào khác.

Chúng ta được biết định dạng svg nó dùng xml.

SVG (Scalable Vector Graphics) là một định dạng hình ảnh dựa trên XML. Điều này có nghĩa là các hình ảnh SVG được lưu trữ và mô tả dưới dạng văn bản XML, giúp chúng dễ dàng được tạo, chỉnh sửa và mở rộng.

Bây giờ hãy tiến hành khai thác nhé.

Payload:

```
<?xml version="1.0" standalone="yes"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]>
<svg width="160px" height="160px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
<text font-size="16" x="0" y="16">&xxe;</text>
</svg>
```

![image](https://github.com/user-attachments/assets/e1547079-2010-41f3-af22-f8a2c90d0d17)

![image](https://github.com/user-attachments/assets/63922417-cf09-445a-98bc-0c4fe94de7bb)

Vậy là đã thành công. Ý tưởng thì cũng chả có gì mới lạ, bạn thấy đó, cái đoạn chèn dtd vào thì chả có gì mới, nhưng cái ý tưởng svg nó là gọi tham chiếu đến cái dtd ở phía trên sau đó gán response vào thằng image. nó sử dụng text và link đó.

![image](https://github.com/user-attachments/assets/34f263c2-52ef-40db-8012-c938fb5fcbe9)

