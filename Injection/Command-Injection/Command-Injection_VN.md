# OS command injection
## OS command injection, simple case
Đầu tiên đọc challenge thì ta có thể thấy được rằng họ kêu để giải được challenge này thì chỉ cần thực thi lệnh `whoami` để xác định tên của người dùng hiện tại đang thực thi lệnh trong hệ thống

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/89315bee-548d-4666-b807-46860d29799e)

Như họ có mô tả là command injection được thấy ở trong `product stock checker` thì ta cũng thử truy cập vào như 1 user bình thường thì ta có thấy được 1 button `check stock`. Khi ta bấm vào thì ta vào burpsuit và check thử phương thức `POST` mà ta vừa gửi lên.

Thì ta nhìn thấy ở dòng thứ 19, nơi mà command sẽ được thực thi. Và theo em được biết thì ta có thể `inject command` bằng cách sử dụng `; xuống dòng && ||`, etc.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b8d675a2-34f7-4340-8edc-95f05b21e61a)

Bây giờ chúng ta hãy thử inject = cách sử dụng `;` và `whoami` như mô tả challenge.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b88efb37-136c-4e3c-897f-732928c2d841)

Vậy là đã giải thành công challenge này.

## Blind OS command injection with time delays
Theo như mô tả của challenge này thì vul nằm ở `feedback function` và sử dụng command injection để gây ra một độ trễ 10 giây.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/d3caf1ea-013b-4dac-b667-40a8e1f1481e)

Chúng ta hãy thử gửi 1 feedback bình thường lên và dùng burpsuit exploit cái request ta vừa gửi

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b97a5f1b-76f5-4d3c-b573-3f508367eaf1)

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/5aee72a7-24e6-492a-9f3a-c123b0f34710)

Như em đã có nói ở trên thì có khá nhiều cách để nối dài câu command như `backstick`, `||`, `;`, etc thì trong challenge này thì ta có 1 vài cách để khai thác thì 1 trong những cách đó là ta dùng `backstick`, nó được gọi là `Command substitution`, khi dùng `Command substitution` thì ta có thể đặt ở bất cứ vị trí nào. và ta đã giải được challenge này.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/74d7bc6e-8d21-4f37-879f-ca882136710f)

Chúng ta cũng còn 1 cách nữa đó chính là chúng ta check từng trường dữ liệu được nhập vào xem trường nào sẽ không filter và khi đó ta có thể inject vào.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/edb6c538-e554-4105-8cf5-ee7c3a1365fe)

Ta có thể thấy nếu đặt tại trường dữ liệu này thì dường như nó đã bị dev chặn

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/c7edf51d-fe2f-4d77-8f07-fa1a4d4d760e)

Tại trường gmail thì dường như không bị chặn.

Ta được biết có 1 số cách để `delay 10s`, trong bài này ta dùng được các cách là `sleep 10` và `ping -c 11 127.0.0.1` 

`-c 11`: Đây là tùy chọn để chỉ định số gói tin ping được gửi đi. Trong trường hợp này, nó là 11 gói tin thì thời gian mà ta ping khi dùng option `-c 11` là hơn 10s

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/8e07ccdf-40c4-42fc-b62d-fec15b2618af)

## Blind OS command injection with output redirection
Goal của challenge này là thực thi lệnh whoami, chuyển hướng kết quả ra file trong `/var/www/images/`, và truy xuất kết quả qua `URL ảnh`.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/50e87b5d-3105-42be-8c4b-517c97781bf4)

Ta tiến hành thực thi whoami và chuyển hướng qua file `/var/www/images/xyz.txt`

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/1f477b87-0b30-4f7d-a37b-841cc69a1f29)

Và ta truy cập vào url chứa images và sửa lại thành `xyz.txt` từ đó giải thành công challenge

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/bfee55e1-5c69-41fe-b6e2-742e13f9c7ab)

# Path traversal
## File path traversal, simple case
Goal của challenge này là truy xuất nội dung của file `/etc/passwd` thông qua lỗ hổng path traversal trong chức năng hiển thị ảnh sản phẩm.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/18114ed1-2b6f-4d2a-873f-391137fb943d)

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/b347fb17-8c5b-4406-90be-c2ac305ba37c)

Khi ta test thử mở file tại `/etc/passwd` thì server báo lỗi không tìm thấy file

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/05a6f659-2469-421c-bcd0-6a5c695535aa)

Ta test thử sử dụng `../` để back lại thư mục root (`/`), dựa vào url ta có thể đoán được hiện tại ta đang ở `var/www/html` chính vì thế ta chỉ cần `../../../`, và khi pentest cách để back về root nhanh nhất là ta sử dụng `../` nhiều nhất có thể để back về root để chắc chắn 100%

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/21cabfad-7d31-4755-8c15-32e1ac1f38bf)

Từ đó ta giải được challenge
## File path traversal, traversal sequences blocked with absolute path bypass
![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/33144b71-6f11-45dc-80ce-a44ae11f4ce4)

Bypass bằng cách sử dụng đường dẫn tuyệt đối để truy xuất nội dung file /etc/passwd.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/5cf4cc2b-44b1-405d-a702-ac94a571d31e)

## File path traversal, traversal sequences stripped non-recursively
![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/cb8d7abf-9379-49e7-aff6-fc4bf9052a9d)

Bypass việc loại bỏ `../` không đệ quy để truy xuất nội dung file /etc/passwd.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/024f07d8-7c77-4ece-b871-43e35c779a73)

Chính vì thể ta sẽ sửa lại thành `....//` để khi filter nó sẽ thành `../` tại vì theo mô tả của challenge là nó không đệ quy

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/f8e2be45-95b1-4c63-81e1-bdd3cb913bf7)
