## File path traversal, simple case
Goal của challenge này là truy xuất nội dung của file `/etc/passwd` thông qua lỗ hổng path traversal trong chức năng hiển thị ảnh sản phẩm.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/18114ed1-2b6f-4d2a-873f-391137fb943d)

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b347fb17-8c5b-4406-90be-c2ac305ba37c)

Khi ta test thử mở file tại `/etc/passwd` thì server báo lỗi không tìm thấy file

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/05a6f659-2469-421c-bcd0-6a5c695535aa)

Ta test thử sử dụng `../` để back lại thư mục root (`/`), dựa vào url ta có thể đoán được hiện tại ta đang ở `var/www/html` chính vì thế ta chỉ cần `../../../`, và khi pentest cách để back về root nhanh nhất là ta sử dụng `../` nhiều nhất có thể để back về root để chắc chắn 100%

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/21cabfad-7d31-4755-8c15-32e1ac1f38bf)

Từ đó ta giải được challenge
