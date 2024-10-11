![image](https://github.com/user-attachments/assets/6258fda1-58d5-4e4d-986b-e69b24682c68)

Ứng dụng lại cho chỉnh sửa display name, tiến hành fuzz xem sao.

![image](https://github.com/user-attachments/assets/6f3b7044-fad0-493c-aeef-476ea7c60f30)

Sau khi fuzz với các kí tự đặc biệt thì ứng dụng này đang dùng template `Twig`.

Kiếm docs của nó và đọc thôi.

Và đây là 1 số format của nó:

```
{{7*7}} = 49

${7*7} = ${7*7}

{{7*'7'}} = 49

{{1/0}} = Error

{{foobar}} Nothing
```

Tiến hành test thử các payload thì ta biết được server nó đang dùng `blog-post-author-display=user.first_name}}{{7*7&csrf=1JyWQBBxi287mHfFvZYZR9nyHRsmwjpz`

![image](https://github.com/user-attachments/assets/4cdb080d-128f-4dce-9bc8-855aeb045597)

![image](https://github.com/user-attachments/assets/ac745804-b08a-42f4-a024-28f9c5d1906a)

Và tôi tiến hành tìm cách gọi hàm để RCE thì tìm được 1 số cách để khai thác.

![image](https://github.com/user-attachments/assets/d4f5c1bd-189f-4c60-b2c5-a4b73078b929)

Tiến hành thử thì dường như nó bị lỗi. Vì vậy cách chúng ta gọi hàm nguy hiểm để RCE đã phá sản, liệu còn cách nào không?? Để ý thì ứng dụng cho chúng ta upload avatar kìa. test thử up 1 shell lên xem

![image](https://github.com/user-attachments/assets/6502b2a0-6de9-4cea-8246-f1847141555c)

Sau khi up 1 shell lên thì nó trả ra lỗi và nó báo luôn cho chúng ta path ảnh mới ảo ma lazada, chưa hết, nó còn bày cho chúng ta là content type của ứng dụng check v:.

![image](https://github.com/user-attachments/assets/9a0ef58c-7d3c-4273-a2b4-bf450b9457e2)

Điều thú vị nữa là thay vì nó deny luôn ngay từ khúc upload thì nó lại nhận request và in ra cái lỗi tào lao kia :")), ai đời lại in ra functions nơi mà file ảnh sẽ được up lên thế kia v:, dơ mặt cho hacker đấm.

Vậy bây giờ ta hãy tận dụng và gọi đến hàm `setAvatar()` ở SSTI xem thử nào, ta để ý rằng hàm đó nó cần 2 arguments, 1 là file names, 2 là mine type. Mục đích là để file up lên luôn là hình ảnh, nhưng nó filter theo kiểu tào lao này dẫn đến attacker có thể kiểm soát toàn bộ luồng request.

Tiến hành gọi đến functions setAvatar('/etc/passwd', 'image/jpg').

![image](https://github.com/user-attachments/assets/9543e899-c5d3-46cd-a402-3b4fa7db109f)

Truy cập vào image thì ta thấy được nó dã RCE thành công.

![image](https://github.com/user-attachments/assets/1ac2b18e-6d19-4303-8375-74556339bb1e)

Tiến hành set avatar là file mà chúng ta cần xóa. sau đó gọi hàm user.gdprDelete() để xóa nó.

![image](https://github.com/user-attachments/assets/7bd961c9-fe56-4006-ac4b-2d3e47f33579)

![image](https://github.com/user-attachments/assets/53d187a8-0633-430c-829f-dcc0cc615ee0)

Và thành công.
