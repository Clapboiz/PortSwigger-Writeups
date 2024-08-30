![image](https://github.com/user-attachments/assets/64acde92-687a-4a36-a1e8-efbcb7564ed0)

Ta có thể thấy được rằng ở challenge này nó là thuộc chủng loại `blind os command injection`. Với những loại này thì ta dùng burp collaborator.

Lý do tại sao ta phải dùng cái tool này thì bạn có thể xem sơ qua về cách 1 cái request nó hoạt động.

![image](https://github.com/user-attachments/assets/6ec0b886-35e9-4b17-b797-54f7eb4d0fc3)

Đó bạn thấy rõ chưa, vì server nó sẽ không trả về cái gì 

![image](https://github.com/user-attachments/assets/ff7480fa-498e-4177-927a-0b36edb91909)

Đó là lí do ta sinh ra thằng burp collaborator.

Khi đó, chúng ta sẽ cần tới một món “công cụ” nào đó, một công cụ hoàn toàn độc lập, một công cụ có thể truy cập thông qua một tên miền cụ thể. Trong payload tấn công SSRF, XXE, … chứa sự tương tác / gọi tới công cụ đó, và nếu chúng ta thu được một lời phản hồi rõ ràng, thì cũng đồng nghĩa rằng payload của chúng ta hoạt động. Và công cụ đó cũng sẽ có thể ghi chép lại thông tin chúng ta đang cần (Vì hệ thống chúng ta tấn công có phản hồi cái quái gì cho mình đâu). Như vậy chúng ta sẽ lấy được nội dung file, những thông tin cần thiết thông qua công cụ này. Một trong những lựa chọn đó là chức năng Burp Collaborator.

![image](https://github.com/user-attachments/assets/4aeb3f5b-0719-4b1f-9695-8b6b602b243d)

![image](https://github.com/user-attachments/assets/6b894ed2-82f2-4de8-89e0-e08e0d379194)

Việc nhận được một DNS lookup cho tên miền do Burp Collaborator tạo ra là một dấu hiệu rằng có một lỗ hổng liên quan đến DNS, ví dụ như SSRF (Server-Side Request Forgery) hoặc một loại lỗ hổng liên quan đến DNS khác trong hệ thống mà bạn đang pentest.

Vậy là xong v:

![image](https://github.com/user-attachments/assets/c2452c12-ec7d-4871-8289-18822fc703cb)
