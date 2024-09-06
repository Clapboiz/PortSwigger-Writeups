# SSTI
## Challenge 1: Basic server-side template injection
## Challenge 2: Basic server-side template injection (code context)
## Challenge 3: Server-side template injection using documentation
## Challenge 4: Server-side template injection in an unknown language with a documented exploit
## Challenge 5: Server-side template injection with information disclosure via user-supplied objects
## Challenge 6: Server-side template injection in a sandboxed environment
## Challenge 7: Server-side template injection with a custom exploit
# Các Template Engine Web Phổ Biến Liên Quan Đến SSTI
## 1. Jinja2 (Python)
- **Ngôn ngữ**: Python
- **Framework**: Flask, Django (có thể sử dụng)
- **Mô tả**: Jinja2 là engine template mạnh mẽ thường dùng trong Flask và Django. Do hỗ trợ cú pháp linh hoạt, nó dễ bị khai thác nếu có lỗ hổng.
- **Cú pháp**: 
    ```jinja
    {% for item in list %}
    {{ variable }}
    {% endfor %}
    ```

## 2. Django Template (Python)
- **Ngôn ngữ**: Python
- **Framework**: Django
- **Mô tả**: Mặc dù Django Template không linh hoạt như Jinja2, nó vẫn có khả năng bị khai thác SSTI trong một số trường hợp nhất định.
- **Cú pháp**:
    ```django
    {% if user.is_authenticated %}
    {{ user.username }}
    {% endif %}
    ```

## 3. Blade (PHP - Laravel)
- **Ngôn ngữ**: PHP
- **Framework**: Laravel
- **Mô tả**: Blade rất phổ biến trong các ứng dụng Laravel. Dù Blade an toàn hơn trong xử lý các dữ liệu đầu vào, nhưng vẫn có thể tiềm ẩn rủi ro nếu không kiểm soát tốt.
- **Cú pháp**: 
    ```blade
    @if(auth()->check())
    {{ $variable }}
    @endif
    ```

## 4. Smarty (PHP)
- **Ngôn ngữ**: PHP
- **Mô tả**: Smarty có thể bị lợi dụng để thực hiện các cuộc tấn công SSTI nếu dữ liệu đầu vào không được lọc đúng cách.
- **Cú pháp**: 
    ```smarty
    {foreach $array as $item}
    {$variable}
    {/foreach}
    ```

## 5. Thymeleaf (Java - Spring)
- **Ngôn ngữ**: Java
- **Framework**: Spring Boot
- **Mô tả**: Thymeleaf có thể bị tấn công SSTI nếu không được cấu hình cẩn thận trong các ứng dụng web dựa trên Spring Boot.
- **Cú pháp**: 
    ```thymeleaf
    th:if="${user != null}"
    th:text="${user.name}"
    ```

## 6. EJS (JavaScript)
- **Ngôn ngữ**: JavaScript
- **Mô tả**: EJS cho phép nhúng JavaScript trực tiếp vào các template, điều này dễ dẫn đến tấn công SSTI nếu không xử lý đúng dữ liệu đầu vào.
- **Cú pháp**: 
    ```ejs
    <% if (user) { %>
    <%= user.name %>
    <% } %>
    ```

## 7. Handlebars (JavaScript)
- **Ngôn ngữ**: JavaScript
- **Mô tả**: Handlebars nổi tiếng về tính an toàn, nhưng nếu bị cấu hình sai, nó vẫn có khả năng bị tấn công SSTI.
- **Cú pháp**: 
    ```handlebars
    {{#if user}}
    {{user.name}}
    {{/if}}
    ```

## 8. Pug (JavaScript)
- **Ngôn ngữ**: JavaScript
- **Mô tả**: Pug (trước đây là Jade) có cú pháp rút gọn nhưng cũng có thể bị khai thác SSTI nếu không cẩn thận trong việc xử lý dữ liệu người dùng.
- **Cú pháp**: 
    ```pug
    if user
      p #{user.name}
    ```

## 9. Liquid (Ruby - Shopify)
- **Ngôn ngữ**: Ruby
- **Mô tả**: Liquid thường được sử dụng trên các nền tảng thương mại điện tử như Shopify và có thể dễ bị tấn công SSTI nếu không xử lý đúng cách các biến và đối tượng.
- **Cú pháp**: 
    ```liquid
    {% if user %}
    {{ user.name }}
    {% endif %}
    ```

## 10. Razor (C# - ASP.NET)
- **Ngôn ngữ**: C#
- **Framework**: ASP.NET, ASP.NET Core
- **Mô tả**: Razor là engine template của ASP.NET và nếu không được cấu hình đúng, nó có thể bị tấn công SSTI thông qua đầu vào không an toàn.
- **Cú pháp**: 
    ```razor
    @if (User.Identity.IsAuthenticated)
    {
        <p>@User.Identity.Name</p>
    }
    ```

### Testing
![image](https://github.com/user-attachments/assets/9aac94bc-2044-458d-8d6f-aa73f94e4f1d)
