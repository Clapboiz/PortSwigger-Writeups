![image](https://github.com/user-attachments/assets/513f9f50-2539-4a42-8fef-ef7b77eb005c)

![image](https://github.com/user-attachments/assets/388f25cf-510c-4600-83ed-25afc9dedf81)

challenge này thì khi chúng ta thay đổi thì dường như nó cũng đã check tính toàn vẹn của dữ liệu rồi nhưng liệu còn cách nào bypass không? Chúng ta được biết thì 1 số server kiểm tra chữ ký nếu thuật toán là HS256, RS256, hoặc các thuật toán khác, nhưng bỏ qua chữ ký nếu thuật toán là none. Đây là do cấu hình sai hoặc việc xử lý không đúng cách của server đối với thuật toán none.

Tiến hành check thử xem sao nhé v:

![image](https://github.com/user-attachments/assets/0a124eef-381b-4a9f-b803-2b0524845173)

Vậy là đã thành công rồi v:

![image](https://github.com/user-attachments/assets/e407ab22-3637-474f-8329-374e0d823ebe)

Thay cookie vào và xóa acc thôi, thành công
