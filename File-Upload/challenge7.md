![image](https://github.com/user-attachments/assets/a7e1054e-b0a6-4cef-9ca9-5560e20c1fa5)

Không thể upload được và dường như thông báo nó cũng chung chung, quay lại challenge thì ta có thể thấy được rằng đây là challenge `race condition`.

Nói sơ qua thì `race condition` là khi server không đồng bộ được dữ liệu. Tức là ví dụ như có 1 mặt hàng mà nó chỉ còn 1 sản phẩm, nhưng tại cùng 1 thời điểm thì 2 người lại bấm mua và kết quả 2 người vẫn mua được, thì nó dẫn đến trường hợp `race condition`. Để đọc chi tiết thì bạn có thể tham khảo google hoặc link `reference` tôi để ở dưới nhé.

Tiến hành khai thác thì ý tưởng là chúng ta hãy gửi 2 gói post và get ở cùng 1 thời điểm.

![image](https://github.com/user-attachments/assets/0f881505-781d-4431-9766-7d9b99e3e22e)

Ta có thể thấy dó là gói post, còn gói get thì làm sao biết nó ở đâu ??

![image](https://github.com/user-attachments/assets/0618ed65-ddfb-40dd-acf8-ce508cbe0d90)

Lợi dụng tính năng preview thì ta `open link to new tab` để kiếm v:

![image](https://github.com/user-attachments/assets/784a5db1-7446-4fa6-bf43-427e122311d8)

Thì nó ở path này

![image](https://github.com/user-attachments/assets/ef56e54a-aea6-497d-a298-800fc7950f37)

Sửa lại như này v:

Giờ chúng ta hãy tạo 1 group nhé xong gửi cùng 1 thời điểm.

![image](https://github.com/user-attachments/assets/ee16f5a9-316c-4bc7-a79e-36436fed9e77)

![image](https://github.com/user-attachments/assets/7956f1cf-b8b5-4cc0-9a43-471e6960e39e)

Tiến hành gửi v:

![image](https://github.com/user-attachments/assets/180e5d2a-7c19-4bef-8372-6ed809ca3ff3)

Gửi lần đầu thì có lẽ sẽ không được, tại vì nó cần lưu cache nữa, bạn cứ bấm vài lần là sẽ được. Tại vì lần đầu khá lâu.

![image](https://github.com/user-attachments/assets/dab72248-fbaa-40b3-8a27-95fefed8cdae)

Thành công sau vài lần bấm v:

Nếu bạn muốn không muốn bấm tay thì bạn có thể viết code hoặc dùng intruder.

![image](https://github.com/user-attachments/assets/9170d43e-508d-41dd-a2b8-2b3bcea10039)

Nếu bạn muốn viết code thì đây.

```
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint, concurrentConnections=10,)

    request1 = '''<YOUR-POST-REQUEST>'''

    request2 = '''<YOUR-GET-REQUEST>'''

    # the 'gate' argument blocks the final byte of each request until openGate is invoked
    engine.queue(request1, gate='race1')
    for x in range(5):
        engine.queue(request2, gate='race1')

    # wait until every 'race1' tagged request is ready
    # then send the final byte of each request
    # (this method is non-blocking, just like queue)
    engine.openGate('race1')

    engine.complete(timeout=60)


def handleResponse(req, interesting):
    table.add(req)
```

Code này là code để bạn send vào `turbo intruder`, 1 extension của burpsuite bạn phải cài vào, nó khác với intruder thường là bạn có thể thay đổi được connection, thread,... khiến tốc độ bruteforce rất nhanh.
### REFERENCES
[1]. https://sec.vnpt.vn/2023/05/exploiting-file-upload-vulnerability-with-race-conditions-challenge-for-you/
