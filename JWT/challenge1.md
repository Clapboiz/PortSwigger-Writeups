![image](https://github.com/user-attachments/assets/6e9c95d6-f179-41dc-83d6-dd1004aa93f3)

Như bạn có thể thấy thì challenge này nó kêu là do không có sự xác minh nào cho chữ kí của jwt dẫn đến kẻ tấn công có thể thay đổi giá trị nào bất kì mà cũng đều không bị bắt.

Tức là 1 token phải đáp ứng được tính toàn vẹn. tức là dữ liệu sau khi bị sửa đổi thì server phải bắt được.

![image](https://github.com/user-attachments/assets/81e22951-d1d6-4e5d-acc4-8ab74474f74e)

1 request sau khi được bắt bởi burp thì ta đã thấy có username của `wiener` rồi, bây giờ chúng ta hãy tiến hành đổi username này thành `administrator` và gửi lại request xem bypass được không nhé.

![image](https://github.com/user-attachments/assets/14ae4d5f-1194-4699-b547-2d1eac63e92b)

![image](https://github.com/user-attachments/assets/3a315ed5-4668-499f-a966-020a8b530a9f)

Tiến hành thay cookie vào trang web và xóa user carlos thôi v:

![image](https://github.com/user-attachments/assets/0839637c-cbba-40b1-99d2-c596a96b3ed2)

Vậy là thành công.

