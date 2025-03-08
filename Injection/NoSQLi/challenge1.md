![image](https://github.com/user-attachments/assets/5adf8a32-d717-4648-9878-4ca7dd0d0058)

Tiến hành fuzz các kí tự đặc biệt xem có chuyện gì xảy ra không?

```
!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

![image](https://github.com/user-attachments/assets/48d2a6da-c389-47b4-9000-2ecff6f59390)

Thì ta biết được nó bị lỗi, tiến hành thu hẹp lại.

![image](https://github.com/user-attachments/assets/87ef1268-03d8-4f43-a9ac-fa574f13b289)

![image](https://github.com/user-attachments/assets/5d2b8ac3-ead4-4e90-bc42-98de6ccfe600)

khi ta nháy đơn thì nó đã bị lỗi, tuy nhiên 2 nháy vẫn tiếp tục bị, thì ta có thể đoán được rằng dường như nó k phải sqli, tại vì nếu như sqli thì nó đã đóng lại và đây sẽ là 1 truy vấn hợp lệ.

![image](https://github.com/user-attachments/assets/a7bfd5e5-446b-49eb-b54b-4e15c53a47fd)

Thôi khỏi đoán nữa, nó đã thông báo ra luôn đây là mongodb rồi.

SQL sử dụng cú pháp truy vấn có cấu trúc, và việc chèn mã thường liên quan đến việc đóng chuỗi và thêm các điều kiện logic.

NoSQL làm việc với cấu trúc dữ liệu dạng key-value hoặc document, và việc chèn mã phải tuân theo cú pháp của JavaScript hoặc JSON, bắt buộc phải có ký tự hợp lệ: Vì NoSQL làm việc với các giá trị cụ thể (chuỗi, số, boolean), nên các giá trị như '' (chuỗi rỗng) hoặc Gifts'' (chuỗi không hợp lệ) sẽ gây ra lỗi.

![image](https://github.com/user-attachments/assets/45946551-47cc-45bc-8b23-d0c37f201617)

Vì thế nên bạn có thể thấy được khi ta 2 nháy thì nó vẫn có lỗi

![image](https://github.com/user-attachments/assets/ebd89695-0c98-49c2-bd36-90400662ac7d)

Và chỉ khi `'+'` được encode lại thành '%2B' thì mới thành công, các trường hợp khác như `'a', 'abc', 'xyz'` đều sẽ không được.

Lí do vì sao nhỉ ?

```
db.products.find({ category: 'Gifts' + '' })
```

Bạn có thể thấy ở trên là 1 ví dụ nosql được viết bằng mongoDB.

Nếu db.products.find({ category: 'Gifts`' + '`' })

Bạn có thể thấy được rằng chỗ tôi bôi đen chính là chỗ inject vào, còn lí do vì sao phải encode vì trên url thì `+` sẽ không được xem như là nối chuỗi mà nó sẽ là khoảng trắng, vì thế nó phải đc encode để backend không nhầm lẫn.

![image](https://github.com/user-attachments/assets/aefad43d-aa39-42d8-87f3-2e872035966f)

Toán tử && trong JavaScript (và trong MongoDB khi thực thi JavaScript) là toán tử logic AND. Thì cơ chế nó cũng khá giống and 1=1 trong sqli thôi.

```
console.log(true && false);  // false
console.log(true && true);   // true
console.log(false && true);  // false
console.log(false && false); // false
```

Tiếp theo ta thử cho truy vấn nó true xem sao.

![image](https://github.com/user-attachments/assets/04e1379f-b129-40a2-b4fb-b2a5e1ae23d5)

```
Gifts' && 1 && 'x
```

Thì lần này nó đã in ra sản phẩm, chứng tỏ đã bị nosqli.

Ta có thể thấy cả 3 đều là True hết thì nó đã nhả data v:, lí do tại sao lại cần tận `&&` trước và cả sau nhỉ???. Lí do là phía sau cần là để giữ đúng format v:. đơn giản vậy thôi.

```
'||1||'
```

![image](https://github.com/user-attachments/assets/71ecfda4-eefd-487a-84d5-a8307f18f6b0)

![image](https://github.com/user-attachments/assets/5a18a0cc-72be-4847-9984-e2618b66c8fc)

Vậy là thành công.

```
Payload 1: category=Gifts' && 1 && 'x
Payload 2: '||1||'
```

Ủa 2 payload này có gì khác nhau k nhỉ, tại sao 1 cái được và 1 cái không ?

**Payload 1:**

+ Nếu category = 'Gifts' có sản phẩm, thì điều kiện 1 không thay đổi kết quả.
+ Nếu category = 'Gifts' không có sản phẩm, thì không có gì được trả về.

**Payload 2:**

+ Điều kiện 1 luôn đúng.
+ category='Gifts' || 1 || 'x' khiến truy vấn không còn phụ thuộc vào danh mục Gifts nữa.

Vậy là thành công rồi.
