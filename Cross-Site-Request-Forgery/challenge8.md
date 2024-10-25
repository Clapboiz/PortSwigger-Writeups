![image](https://github.com/user-attachments/assets/422b8a01-5fee-4cb2-929b-e6a7a395c20e)

Lần này thì challenge nó là samesite: strict :">, và nhiệm vụ vẫn là đổi email.

![image](https://github.com/user-attachments/assets/a58cd4a3-6177-4c54-9257-df1bd47d86fa)

Thì giờ tôi nhắc lại cho bạn lí thuyết về samesite

SameSite là thuộc tính của cookie giúp kiểm soát cách cookie được gửi trong các yêu cầu đến từ các trang web khác nhau nhằm giảm thiểu nguy cơ tấn công CSRF:

+ SameSite=Lax: Cookie sẽ được gửi khi người dùng điều hướng từ trang khác bằng phương thức GET (ví dụ nhấp vào link). Tuy nhiên, các yêu cầu POST từ trang khác sẽ không gửi cookie, giúp ngăn chặn CSRF trong một số trường hợp.
+ SameSite=Strict: Cookie chỉ được gửi nếu yêu cầu xuất phát từ cùng một trang web, tức là không có cross-site requests nào có thể gửi cookie. Điều này bảo vệ cao hơn khỏi CSRF nhưng có thể làm giảm trải nghiệm người dùng.
+ SameSite=None: Cookie sẽ được gửi trong mọi yêu cầu (ngay cả từ cross-site), nhưng yêu cầu sử dụng HTTPS với thuộc tính Secure.

Vậy nó set là strict rồi, làm sao đây???

Điều này có nghĩa là bất kỳ yêu cầu nào đến từ trang web khác (cross-site), dù là GET hay POST, sẽ không gửi cookie đi. Đó là lý do tại sao khi dùng SameSite=Strict, dù bạn giả lập GET thành POST (ví dụ bằng _method), cookie cũng không được gửi nếu yêu cầu đó bắt nguồn từ một trang web khác.

![image](https://github.com/user-attachments/assets/e2ba0ac3-6248-4f78-adfd-37c3e1b81317)

![image](https://github.com/user-attachments/assets/2cb0a5bd-df2d-45af-a13e-7ca3929b2136)

Tiến hành gửi 1 comment thì ta có thể thấy được là sau khi comment thì dường như trang web nó lại thực hiện redirect về vài post có param là `postid`. Và như ta nhìn thấy thì `postid` nó đang không có biện pháp bảo vệ gì, dẫn đến ta có thể đoán được rằng chỗ này có khả năng xảy ra path traversal.

Khi ta bấm vào:

```
https://0a950078046f5823d8bf2d5900db0094.web-security-academy.net/my-account/
```

Thì nó lại back về my-account 

![image](https://github.com/user-attachments/assets/b78ae92a-49b6-46d1-bf71-60996f0f5bdf)

Vậy thì giờ ta hãy lợi dụng nó để cho nó cùng site để còn bypass `samesite: strict` chứ. Nó yêu cầu là phải cùng 1 trang web mà, vì vậy thì ta lợi dụng path traversal để biến nó thành 1 request cùng 1 trang web.

![image](https://github.com/user-attachments/assets/c6e0a992-4f0c-49ac-8e0e-c27e53ee49fa)

<script>
    document.location = "https://0a950078046f5823d8bf2d5900db0094.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=abc@gmail.com%26submit=1";
</script>

Lí do tại sao tôi không cần phải giả lập post request bằng _method là vì challenge này nó chấp nhận get request v:

Và thành công

![image](https://github.com/user-attachments/assets/9fc18cd0-6ef2-4494-9eb2-3582340ae594)
