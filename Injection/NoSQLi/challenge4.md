![image](https://github.com/user-attachments/assets/2241fee5-c9be-411f-92b7-99df1799d0bc)

![image](https://github.com/user-attachments/assets/7018a76f-386e-43b8-b114-311f08a3ceb9)

![image](https://github.com/user-attachments/assets/5d615b55-dc50-44c3-b284-584ecdb4a253)

```
{"username":"carlos","password":{"$ne":"sssss"}}
```

Nó thông báo như thế có nghĩa là nosqli đã được chèn vào :")

![image](https://github.com/user-attachments/assets/e80d919e-2900-4d25-ac66-ed80f1abfc32)

Tiếp tục thêm điều kiện true vào, thì where nó vẫn đang được thực thi.

Ta sẽ lợi dụng where để bruteforce. Bạn có suy nghĩ bruteforce kiểu gì không :"))

Thì tôi có vd:

```
{
    "_id": "abc123",
    "username": "carlos",
    "password": "hashed_password",
    "resetToken": "XYZ789"
}
```

Mục tiêu: Tìm được resetToken, vì nó cho phép đặt lại mật khẩu.

+ Object.keys(this)[1]: Lấy tên trường thứ hai (username).
+ .match('^.{§§}§§.*'): So sánh ký tự tại vị trí số §§ (để brute-force ký tự).

Payload 1: Số thứ tự ký tự trong tên trường (0 → 20).

Payload 2: Các ký tự (a-z, A-Z, 0-9).

Chạy Intruder attack → Lọc phản hồi "Account locked" để tìm ra tên trường.

Tiếp tục với Object.keys(this)[2], Object.keys(this)[3]... để liệt kê tất cả các trường.

![image](https://github.com/user-attachments/assets/2c825e34-2325-45a9-b6e6-3f3a0fe1aa70)

Đó với trường thứ 1 thì ta tìm được field là username rồi, bạn nhớ sắp xếp theo thứ tự nhé

![image](https://github.com/user-attachments/assets/b4abdcde-feba-4f70-9576-07a1d335a3af)

Tiếp theo, bạn cần bấm vào forgot passwd -> reset passwd rồi mới bruteforce đc trường tokenID nhé.

![image](https://github.com/user-attachments/assets/b2f4165c-9de7-4ac2-8158-b4940d28f96a)

Sắp xếp theo thứ tự ta được `changePwd`

![image](https://github.com/user-attachments/assets/4c5d2b8f-ed5a-4e36-87eb-4cd325c38304)

Đó, sau khi ta bruteforce thì ta được chuỗi như trên: `fce0d09cb2026597`

![image](https://github.com/user-attachments/assets/4ad957e4-02c4-4418-8070-e780c791c493)

![image](https://github.com/user-attachments/assets/59cecba5-1607-4d0c-a1cc-5ccda5cb4597)

Vậy là thành công rồi đó :3
