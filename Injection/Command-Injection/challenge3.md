## Blind OS command injection with output redirection
Goal của challenge này là thực thi lệnh whoami, chuyển hướng kết quả ra file trong `/var/www/images/`, và truy xuất kết quả qua `URL ảnh`.

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/50e87b5d-3105-42be-8c4b-517c97781bf4)

Ta tiến hành thực thi whoami và chuyển hướng qua file `/var/www/images/xyz.txt`

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/1f477b87-0b30-4f7d-a37b-841cc69a1f29)

Và ta truy cập vào url chứa images và sửa lại thành `xyz.txt` từ đó giải thành công challenge

![image](https://github.com/Clapboiz/PortSwigger-Writeups/assets/112185647/bfee55e1-5c69-41fe-b6e2-742e13f9c7ab)
