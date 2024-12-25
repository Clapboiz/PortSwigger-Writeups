![image](https://github.com/user-attachments/assets/bff64fca-bd92-4cfa-97e3-f1f77eb3e609)

Challenge này liên quan đến việc xử lý cache của ứng dụng. Attacker có thể lợi dụng điều này để lừa user truy cập một URL độc hại, khiến phản hồi từ server (chứa thông tin của user) bị lưu trữ vào cache.

Mục tiêu là đánh cắp api key của user `carlos`.

![image](https://github.com/user-attachments/assets/7ce21b6e-0485-41bd-b5e3-995d31a428eb)

Khi chúng ta thử với 1 path không tồn tại trên hệ thống thì dường như nó sẽ ánh xạ về thông tin của `/my-account`

![image](https://github.com/user-attachments/assets/74729db3-4977-473e-90b6-a25349150c9c)

Ta có thể thấy response của hai lần gọi đến URL `/my-account/xyz.js` khác nhau. Lần đầu tiên, server xử lý và lưu phản hồi vào cache `(header X-Cache: miss)`. Khi gửi lại yêu cầu đến cùng path trong vòng `<30s` (do server cấu hình `Control: max-age=30` chứ không phải server nào cũng thế), phản hồi được phục vụ từ cache `(header X-Cache: hit)`, và cũng lưu ý cái này chỉ có tác dụng đói với các file tĩnh thôi nhé, như các file `html, js, css,...` Nhưng chúng ta sẽ chỉ lợi dụng các file có thể thực thi được script như `html, js` thôi nhé.

Tiến hành chèn script nhé.

```
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account/wcd.js"</script>
```

Ý tường của việc này là lừa user carlos nhấn vào link này và nó sẽ chuyển hướng đến trang web của kẻ tấn công. Khi Carlos truy cập link, cache server lưu phản hồi từ `origin server (chứa API key của Carlos)`, việc còn lại chỉ là attacker sẽ bấm lại vào link dưới đây để truy xuất cache ra mà thôi.

```
https://YOUR-LAB-ID.web-security-academy.net/my-account/wcd.js
```

![image](https://github.com/user-attachments/assets/057b759d-ac18-4c51-8bd2-89169a4f6728)

![image](https://github.com/user-attachments/assets/e3f5c6ad-4bd7-46a5-980d-9cda7c11c6fa)

Vậy là đã thành công rồi.
