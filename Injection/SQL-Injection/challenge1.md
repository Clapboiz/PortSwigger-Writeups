![image](https://github.com/user-attachments/assets/4b052ad9-315f-4547-a89f-ae27fffe09e7)

Ta nhìn thì cách để giải challenge này cũng khá đơn giản vì nó đã cho query rồi, giờ chúng ta chỉ cần `'` để đóng cái kí tự đó sau đó có thể dùng các câu lệnh inject của sql, hoặc các toán tử luận lí để chèn zô.

Payload:

```
' or 1 = 1--+
```

![image](https://github.com/user-attachments/assets/5497d3b5-e929-42cc-93a5-325603e94141)

Vậy là thành công rồi đó v:

Nếu như blackbox thì cứ thử `'` hoặc `"` hoặc `--+`,... bất cứ thứ gì liên quan đến sqli để check xem nó tồn tại không nhé.
