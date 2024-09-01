![image](https://github.com/user-attachments/assets/1ebb810f-a559-4d97-9843-c38102b855af)

![image](https://github.com/user-attachments/assets/e84d8eda-b196-424f-88af-d748a534c961)

![image](https://github.com/user-attachments/assets/7947f8fa-ecb3-4804-80f9-e289d9dd7fcf)

Ta nhận thấy challenge này có lỗ hổng xxe nhưng lại không cho dùng external dtd, vì vậy chúng ta hãy dùng internal xem sao.

![image](https://github.com/user-attachments/assets/64f9a0d1-2cbd-49c4-b6b3-cab9a28d8573)

1 sai lầm khi dev v:, giờ chúng ta hãy thử lợi dụng nó xem sao.

![image](https://github.com/user-attachments/assets/14ebe884-0118-4ca3-9ef4-7c93a63ae01e)

Bạn có để ý không, khi nó có file đó và khi nó không có thì response nó khác đúng chứ, vậy thì ta có thể khẳng định chắc là ta có thể khai thác được.

Ở đây, Hint chỉ ra rằng hệ thống có 1 DTD tại `/usr/share/yelp/dtd/docbookx.dtd` có chứa 1 entity tên `ISOamso`

Tiến hành chui vào xem.

![image](https://github.com/user-attachments/assets/55b2941a-6b4e-485b-90d2-5742e63fbe62)

Đúng là có thiệt, vậy câu hỏi đặt ra là lỡ sau này mình gặp web khác thì lúc đó làm gì có hint của challenge, làm sao ta tìm đc?

Ta kiếm seclisst và fuzz thoi v:

Đây là seclist mà tôi tìm được nè:

```
https://github.com/GoSecure/dtd-finder/blob/master/list/dtd_files.txt
```

Giải quyết được vấn đề này rồi nhé, tiến hành khai thác.

Payload:

```
<!DOCTYPE message [
<!ENTITY % local_dtd SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
<!ENTITY % ISOamso '
<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">
<!ENTITY &#x25; eval "<!ENTITY &#x26;#x25; error SYSTEM &#x27;file:///nonexistent/&#x25;file;&#x27;>">
&#x25;eval;
&#x25;error;
'>
%local_dtd;
]>
```

Parameter entity local_dtd chứa nội dung tệp `/usr/share/yelp/dtd/docbookx.dtd` là local DTD trên server.

Parameter entity ISOamso chứa định nghĩa: parameter entity file chứa nội dung tệp `/etc/passwd`, parameter entity eval chứa định nghĩa parameter entity error chứa nội dung /etc/passwd sau khi tham chiếu tới %file;
Gọi tham chiếu các entity.

![image](https://github.com/user-attachments/assets/c5f2c0b8-5491-4da4-a84f-6a92bf491739)


Kẻ tấn công có thể lợi dụng local DTD và kết hợp với internal DTD để kích hoạt các lỗi phân tích cú pháp XML, từ đó rò rỉ dữ liệu nhạy cảm. Kỹ thuật này rất hữu ích khi out-of-band connections bị chặn, tức là kẻ tấn công không thể tải external DTD từ một server từ xa.

Để thực hiện tấn công này, kẻ tấn công cần tìm ra một local DTD file phù hợp trên server. Điều này có thể thực hiện bằng cách thử tải các DTD file khác nhau từ internal DTD và kiểm tra các thông báo lỗi trả về. Ví dụ: trên các hệ thống Linux sử dụng GNOME, thường có một DTD file tại /usr/share/yelp/dtd/docbookx.dtd.

**Giải thích chi tiết payload**

```
Định nghĩa một XML parameter entity (local_dtd):

<!ENTITY % local_dtd SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">:

Đây là định nghĩa của một parameter entity tên là %local_dtd. Nó trỏ tới một local DTD file nằm trên hệ thống máy chủ tại đường dẫn /usr/share/yelp/dtd/docbookx.dtd.
Mục đích của việc này là để tải nội dung của DTD file này vào trong tài liệu XML hiện tại.

Redefine entity ISOamso:

<!ENTITY % ISOamso '...'>: Đây là một parameter entity khác được định nghĩa lại với tên %ISOamso. Nội dung của nó chứa các entity khác để khai thác lỗi phân tích cú pháp:

<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">:

Định nghĩa một parameter entity %file trỏ tới nội dung của file /etc/passwd trên hệ thống máy chủ.
<!ENTITY &#x25; eval "<!ENTITY &#x26;#x25; error SYSTEM &#x27;file:///nonexistent/&#x25;file;&#x27;>">:

Định nghĩa một parameter entity %eval chứa mã để gây ra một lỗi phân tích cú pháp. Lỗi này sử dụng một đường dẫn không tồn tại (file:///nonexistent/%file;), nơi mà %file trỏ tới nội dung của file /etc/passwd.
&#x25;eval; và &#x25;error;:

Đây là các tham chiếu tới parameter entity %eval và %error. %eval sẽ được thay thế bằng mã khai thác lỗi, và %error sẽ được xử lý, gây ra lỗi phân tích cú pháp.

Thực thi local DTD và kích hoạt lỗi:

%local_dtd;:

Sau khi định nghĩa các entity cần thiết, %local_dtd; được sử dụng để chèn nội dung của file local DTD (docbookx.dtd) vào tài liệu XML. Việc này sẽ include (bao gồm) tất cả các entity đã được định nghĩa lại.

Khi parser XML xử lý nội dung này, nó sẽ cố gắng thực thi các entity %eval và %error, dẫn đến lỗi phân tích cú pháp.
```

1. Xử Lý Entities Đã Định Nghĩa:
   
    Khi kẻ tấn công sử dụng một entity đã được định nghĩa sẵn trên server (như %local_dtd trong ví dụ của bạn), hệ thống có thể tin rằng các entities này đã được kiểm tra và không cần kiểm tra thêm, vì chúng đã tồn tại và được định nghĩa hợp lệ trên máy chủ.

3. Lỗ Hổng Do Không Kiểm Tra Toàn Bộ:

    Việc chỉ kiểm tra các entities đã có sẵn và bỏ qua các entities redefine có thể tạo ra lỗ hổng bảo mật. Kẻ tấn công có thể khai thác lỗ hổng này bằng cách redefine các entities cục bộ theo cách tạo ra lỗi hoặc truy xuất dữ liệu nhạy cảm.
