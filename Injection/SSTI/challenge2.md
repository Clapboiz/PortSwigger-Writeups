![image](https://github.com/user-attachments/assets/4fb1f69c-82ba-442b-8f7f-a3b05dae7fdd)![image](https://github.com/user-attachments/assets/54e0a797-e78c-4b7d-8591-dc61ba3e0747)

Đến challenge này thì họ bảo họ dùng tornado template. Tiến hành đăng nhập vào và test chức năng xem lỗ hổng ở đâu?

![image](https://github.com/user-attachments/assets/d4206143-a2f6-4dd0-8ddb-125c36e7feb0)

Tiến hành viết comment thì ta thấy được nó hiện tên là `peter wiener`

![image](https://github.com/user-attachments/assets/d5453929-7144-461d-9261-6db56c0c8c5f)

Tiến hành xem thêm 1 vài chức năng thì ta có thể thấy được rằng ta có thể đổi name hiển thị theo các options dưới đây

![image](https://github.com/user-attachments/assets/fa6de35a-cfb6-4a0b-8ee8-97220dc49ec0)

Đúng rồi, tiến hành inject vào trường đổi thông tin display xem sao.

![image](https://github.com/user-attachments/assets/22b08bef-ff23-4c55-a538-82bc2446dd61)

![image](https://github.com/user-attachments/assets/094d3d99-30a9-45f5-9ce8-ad768979814c)

Tiến hành fuzz các kí tự đặc biệt thì ta có thể thấy được rằng ở đây nó sử dụng tornado template.

Tiếp theo thì ta biết được rằng format của tornado là `{{ }}` (những gì nằm giữa sẽ được server xử lí và ném lên UI hiển thị), và {% %} (những gì nằm ở giữa sẽ là nơi import libs python).

Vì thể để inject thì chúng ta sẽ gửi }} để đóng câu lệnh đầu tiên, sau đó {{ để inject ( ::)) đặc trưng của chủng lỗi injection rồi chứ gì, không nói dài dòng nữa).

![image](https://github.com/user-attachments/assets/55b4f65c-94f2-4ac1-b3b3-c5b341649855)

![image](https://github.com/user-attachments/assets/798916a1-1292-460e-822e-fd951ddda480)

Đấy, đã thành công.

Payload:

```
}}{% import os %}{{os.system('rm /home/carlos/morale.txt')
```
# REFERENCES
[1]. https://ajinabraham.com/blog/server-side-template-injection-in-tornado
