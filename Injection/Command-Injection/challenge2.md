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
