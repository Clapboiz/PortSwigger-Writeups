![image](https://github.com/user-attachments/assets/aa2bb96f-7c8d-489c-9502-4e36d701f22c)

![image](https://github.com/user-attachments/assets/5be09988-5443-4e3e-b95b-0aaf54c00d92)

Có vẻ như nó đã bị chặn v:, đọc mô tả challenge thì có thể biết được lần này nó chặn 1 vài external entity.

Thì chúng ta đã vừa sử dụng `&` để tham chiếu, được biết thì xml có 1 cách tham chiếu khác nữa, đó là dùng `%`.

![image](https://github.com/user-attachments/assets/59e20c0e-339a-410a-8fe4-9eb0c77b0e18)

Bạn có thể xem thử cái này nè.

Vậy chúng ta bây giờ hãy thử khai thác với `%` xem sao nhé.

![image](https://github.com/user-attachments/assets/fdeb9c07-7991-42fa-8ed3-c07cda2d0df0)

![image](https://github.com/user-attachments/assets/c72bc7ee-92d3-4ae3-ad1a-ccbd93fa5fa2)

![image](https://github.com/user-attachments/assets/402f204c-7e37-42b6-bf4f-7bc6b63c2699)

Có thể thấy server nó trả về `"XML parsing error"`, nhưng cái này không sao hết, vì có thể code ra mà, cái chúng ta cần nhìn là nhìn ở layer dưới kia kìa, xem layer dưới nó có hoạt động không bằng cách dùng burp collaborator á, chứ k phải xem layer 7. Vì thế challenge này mới có tên là blind xxe

Vậy là thành công rồi nhé.


