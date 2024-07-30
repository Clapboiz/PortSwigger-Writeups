![image](https://github.com/user-attachments/assets/1077433f-498e-4f07-8f65-f346af3698eb)

Đây là mô tả của challenge.

Thì challenge này đã có nói qua là lỗi ở phần hiển thị image.

Traversal Sequences Stripped: Ứng dụng cố gắng ngăn chặn tấn công bằng cách loại bỏ hoặc chặn các chuỗi path traversal như ../. Tuy nhiên, cách thức này không phải lúc nào cũng hiệu quả nếu không được thực hiện cẩn thận.

Superfluous URL-decode: Sau khi loại bỏ các chuỗi path traversal, ứng dụng vẫn tiếp tục giải mã URL một cách không cần thiết.

Thì dựa vào đây thì ta có thể đoán là nó đã filter `../`

![image](https://github.com/user-attachments/assets/48fe05f3-04dd-465b-8476-7d8d39d3b0e6)

![image](https://github.com/user-attachments/assets/42cafaea-9389-457d-a385-ff459bf41a8d)

Đúng như vậy, và khi ta encode 1 lần thì nó cũng filter, vậy thì ta thử encode 2 lần xem sao nào.

![image](https://github.com/user-attachments/assets/08cce343-355a-4de0-b8a5-532cc8275951)

Và đây là payload:

```
%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66etc/passwd
```
