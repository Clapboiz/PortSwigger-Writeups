## File path traversal, traversal sequences stripped non-recursively
![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/cb8d7abf-9379-49e7-aff6-fc4bf9052a9d)

Bypass việc loại bỏ `../` không đệ quy để truy xuất nội dung file /etc/passwd.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/024f07d8-7c77-4ece-b871-43e35c779a73)

Chính vì thể ta sẽ sửa lại thành `....//` để khi filter nó sẽ thành `../` tại vì theo mô tả của challenge là nó không đệ quy

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/f8e2be45-95b1-4c63-81e1-bdd3cb913bf7)
