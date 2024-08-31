## Challenge 1: Exploiting XXE using external entities to retrieve files
## Challenge 2: Exploiting XXE to perform SSRF attacks
## Challenge 3: Blind XXE with out-of-band interaction
## Challenge 4: Blind XXE with out-of-band interaction via XML parameter entities
## Challenge 5: Exploiting blind XXE to exfiltrate data using a malicious external DTD
## Challenge 6: Exploiting blind XXE to retrieve data via error messages
## Challenge 7: Exploiting XInclude to retrieve files
## Challenge 8: Exploiting XXE via image file upload
## Challenge 9: Exploiting XXE to retrieve data by repurposing a local DTD
### XXE
Khai báo external entity chính là điểm mấu chốt trong kỹ thuật tấn công XXE. Vậy nó là gì ?

1. DTD định nghĩa cấu trúc và quy tắc cho tài liệu XML.
2. Entity là một đơn vị dữ liệu trong XML có thể tái sử dụng, bao gồm internal và external.
3. XML Parser là công cụ xử lý tài liệu XML, giúp chuyển đổi XML thành cấu trúc dữ liệu mà chương trình có thể sử dụng.

Đến đây thì khái niệm về External Entity đã tương đối rõ ràng. Câu hỏi là nó có thể làm được gì ?

1. Denial of service (Đây là một kiểu tấn công mang tên Billion laughs attack. Thực tế đây mới chỉ là Internal entity.)
2. File Disclosure (Đọc code, etc/passwd, ...)
3. SSRF
4. Access Control Bypass (Loading Restricted Resources — ví dụ với PHP)
   ![image](https://github.com/user-attachments/assets/a194df40-df81-492b-8e5a-64f5297b9e30)
### REFERENCES
[1]. https://viblo.asia/p/xml-external-entity-xxe-injection-07LKX97pZV4
[2]. https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection
