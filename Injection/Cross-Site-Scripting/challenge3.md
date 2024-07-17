![image](https://github.com/user-attachments/assets/9c9c9c46-d0fa-432a-8270-6313625f45ed)

Sau khi test chức năng và f12 lên để view source code thì ta có thể thấy được rằng dòng `57` sẽ là nơi xử lí query. Ta có thể thấy được query như sau query nó sẵn có trong hệ thống đang ở dạng `<img src="/resources/images/tracker.gif?searchTerms='+query+'">`.

Ta cũng có thể lợi dụng điểu này như việc khai thác các chủng lỗi injection khác như là thêm dấu `"`. Vậy giờ ta hãy kiểm chứng nhé!

![image](https://github.com/user-attachments/assets/1158ddbe-89f1-450b-bc7f-2767d7b2dbf7)

Đây là payload:

```
a" onload="alert(origin)"
```

```
"><svg onload=alert(1)>
```
