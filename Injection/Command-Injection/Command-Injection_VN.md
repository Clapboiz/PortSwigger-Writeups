# OS command injection
## OS command injection, simple case
Đầu tiên đọc challenge thì ta có thể thấy được rằng họ kêu để giải được challenge này thì chỉ cần thực thi lệnh `whoami` để xác định tên của người dùng hiện tại đang thực thi lệnh trong hệ thống

![image](https://gist.github.com/assets/112185647/9d2ddd46-bd37-4a91-9836-e1eee8645b4e)

Như họ có mô tả là command injection được thấy ở trong `product stock checker` thì ta cũng thử truy cập vào như 1 user bình thường thì ta có thấy được 1 button `check stock`. Khi ta bấm vào thì ta vào burpsuit và check thử phương thức `POST` mà ta vừa gửi lên.

Thì ta nhìn thấy ở dòng thứ 19, nơi mà command sẽ được thực thi. Và theo em được biết thì ta có thể `inject command` bằng cách sử dụng `; xuống dòng && ||`, etc.


![image](https://gist.github.com/assets/112185647/67bf31d2-d30f-485c-b418-aec44ff11c32)

Bây giờ chúng ta hãy thử inject = cách sử dụng `;` và `whoami` như mô tả challenge.

![image](https://gist.github.com/assets/112185647/e340fb94-1519-409d-baa3-dd96c0c9d9df)

Vậy là đã giải thành công challenge này.

## Blind OS command injection with time delays
Theo như mô tả của challenge này thì vul nằm ở `feedback function` và sử dụng command injection để gây ra một độ trễ 10 giây.

![image](https://gist.github.com/assets/112185647/da3ff7b3-f504-4312-9d41-193a40716ed4)

Chúng ta hãy thử gửi 1 feedback bình thường lên và dùng burpsuit exploit cái request ta vừa gửi

![image](https://gist.github.com/assets/112185647/6c2f7558-1812-40c3-832d-fbca3c76f162)

![image](https://gist.github.com/assets/112185647/d55c08f7-3157-4a59-8601-91ae1befce0a)

Như em đã có nói ở trên thì có khá nhiều cách để nối dài câu command như `backstick`, `||`, `;`, etc thì trong challenge này thì ta có 1 vài cách để khai thác thì 1 trong những cách đó là ta dùng `backstick`, nó được gọi là `Command substitution`, khi dùng `Command substitution` thì ta có thể đặt ở bất cứ vị trí nào. và ta đã giải được challenge này.

![image](https://gist.github.com/assets/112185647/31cdc210-1a34-4c0c-a45d-12774c073964)

Chúng ta cũng còn 1 cách nữa đó chính là chúng ta check từng trường dữ liệu được nhập vào xem trường nào sẽ không filter và khi đó ta có thể inject vào.

![image](https://gist.github.com/assets/112185647/cde58349-e9df-462f-a6b3-edad4960464b)

Ta có thể thấy nếu đặt tại trường dữ liệu này thì dường như nó đã bị dev chặn

![image](https://gist.github.com/assets/112185647/68b54120-b220-47fa-9c84-201baf8cce47)

Tại trường gmail thì dường như không bị chặn.

Ta được biết có 1 số cách để `delay 10s`, trong bài này ta dùng được các cách là `sleep 10` và `ping -c 11 127.0.0.1` 

`-c 11`: Đây là tùy chọn để chỉ định số gói tin ping được gửi đi. Trong trường hợp này, nó là 11 gói tin thì thời gian mà ta ping khi dùng option `-c 11` là hơn 10s

![image](https://gist.github.com/assets/112185647/1ca952f2-7361-4a17-b4d5-48f09122449b)
## Blind OS command injection with output redirection
Goal của challenge này là thực thi lệnh whoami, chuyển hướng kết quả ra file trong `/var/www/images/`, và truy xuất kết quả qua `URL ảnh`.

![image](https://gist.github.com/assets/112185647/ddbf7630-5606-46e8-b2f4-f6d65a3f23a4)

Ta tiến hành thực thi whoami và chuyển hướng qua file `/var/www/images/xyz.txt`

![image](https://gist.github.com/assets/112185647/e9588893-1fe0-4bc9-bb04-85b550665ba4)

Và ta truy cập vào url chứa images và sửa lại thành `xyz.txt` từ đó giải thành công challenge

![image](https://gist.github.com/assets/112185647/9a4ea874-266c-47c5-880a-80f48afc131f)

# Path traversal
## File path traversal, simple case
Goal của challenge này là truy xuất nội dung của file `/etc/passwd` thông qua lỗ hổng path traversal trong chức năng hiển thị ảnh sản phẩm.

![image](https://gist.github.com/assets/112185647/f1b7d48e-1f10-4ba3-91a0-2a445ff47993)

![image](https://gist.github.com/assets/112185647/66026592-91eb-4f94-ab15-77042865945b)

Khi ta test thử mở file tại `/etc/passwd` thì server báo lỗi không tìm thấy file

![image](https://gist.github.com/assets/112185647/350391c0-d549-4b70-9d3f-52910061ce50)

Ta test thử sử dụng `../` để back lại thư mục root (`/`), dựa vào url ta có thể đoán được hiện tại ta đang ở `var/www/html` chính vì thế ta chỉ cần `../../../`, và khi pentest cách để back về root nhanh nhất là ta sử dụng `../` nhiều nhất có thể để back về root để chắc chắn 100%

![image](https://gist.github.com/assets/112185647/9429220d-9727-4fca-960d-2cc41f9806e4)

Từ đó ta giải được challenge
## File path traversal, traversal sequences blocked with absolute path bypass
![image](https://gist.github.com/assets/112185647/ae3f9cdf-72f7-4c88-a0d5-2f8ecffe474e)

Bypass bằng cách sử dụng đường dẫn tuyệt đối để truy xuất nội dung file /etc/passwd.

![image](https://gist.github.com/assets/112185647/d20f3c33-9c12-49ed-b7f5-0d8cbaae6e92)
## File path traversal, traversal sequences stripped non-recursively
![image](https://gist.github.com/assets/112185647/ddedce50-6af9-49e0-afa5-be434c82181b)

Bypass việc loại bỏ `../` không đệ quy để truy xuất nội dung file /etc/passwd.

![image](https://gist.github.com/assets/112185647/977435cb-29fb-47e5-8d09-da39cbb9eada)

Chính vì thể ta sẽ sửa lại thành `....//` để khi filter nó sẽ thành `../` tại vì theo mô tả của challenge là nó không đệ quy

![image](https://gist.github.com/assets/112185647/a0b002d6-e45f-430d-b9e1-414a16181a6d)