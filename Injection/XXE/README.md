## Challenge 1: Exploiting XXE using external entities to retrieve files
## Challenge 2: Exploiting XXE to perform SSRF attacks
## Challenge 3: Blind XXE with out-of-band interaction
## Challenge 4: Blind XXE with out-of-band interaction via XML parameter entities
## Challenge 5: Exploiting blind XXE to exfiltrate data using a malicious external DTD
## Challenge 6: Exploiting blind XXE to retrieve data via error messages
## Challenge 7: Exploiting XInclude to retrieve files
## Challenge 8: Exploiting XXE via image file upload
## Challenge 9: Exploiting XXE to retrieve data by repurposing a local DTD
# XXE
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
5. XInclude
   XInclude (XML Inclusions) là một tiêu chuẩn của W3C (World Wide Web Consortium) dùng để cho phép bao gồm nội dung từ một tài liệu XML khác vào trong tài liệu XML hiện tại. XInclude giúp tái sử dụng nội dung XML, làm giảm sự trùng lặp và tăng tính linh hoạt của các tài liệu XML.

   Cú pháp của XInclude sử dụng các phần tử <xi:include> để chỉ định tài liệu XML nào cần được bao gồm và vị trí cần bao gồm nội dung trong tài liệu gốc. Dưới đây là một ví dụ minh họa cách sử dụng XInclude.

   **Ví dụ về XInclude:**

   **_Tài liệu chapter1.xml:_**

   ```
   <!-- chapter1.xml -->
   <chapter>
       <title>Chapter 1: Introduction to XML</title>
       <content>This is the content of chapter 1.</content>
   </chapter>
   ```
   
   **_Tài liệu book.xml:_**

   ```
   <!-- book.xml -->
   <book xmlns:xi="http://www.w3.org/2001/XInclude">
       <title>XML Guide</title>
       <xi:include href="chapter1.xml"/>
   </book>
   ```

   Trong ví dụ trên, tài liệu book.xml sử dụng phần tử <xi:include> để bao gồm nội dung của tài liệu chapter1.xml. Khi tài liệu book.xml được xử lý bởi một bộ phân tích hỗ trợ XInclude, nội dung của chapter1.xml sẽ được chèn vào vị trí của <xi:include>.

   **_Sau khi xử lý XInclude, tài liệu book.xml sẽ trông như sau:_**

   ```
   <book xmlns:xi="http://www.w3.org/2001/XInclude">
       <title>XML Guide</title>
       <chapter>
           <title>Chapter 1: Introduction to XML</title>
           <content>This is the content of chapter 1.</content>
       </chapter>
   </book>
   ```

   Như vậy, nội dung từ tài liệu chapter1.xml đã được bao gồm vào trong tài liệu book.xml tại vị trí của phần tử <xi:include>.

   XInclude rất hữu ích trong các tình huống mà bạn cần tái sử dụng nội dung XML trên nhiều tài liệu khác nhau hoặc muốn tổ chức tài liệu XML thành các phần nhỏ hơn để quản lý dễ dàng hơn.


# REFERENCES
[1]. https://viblo.asia/p/xml-external-entity-xxe-injection-07LKX97pZV4

[2]. https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection

[3]. https://viblo.asia/s/xml-external-entity-vulnerabilities-xxe-cac-lo-hong-xml-external-entity-BQyJKzR74Me

[4]. https://github.com/GoSecure/dtd-finder/blob/master/list/dtd_files.txt
