![image](https://github.com/user-attachments/assets/8ada8e2a-1f15-4ea8-bc10-a9b62db91e33)

```
Oracle: dbms_pipe.receive_message(('a'),10)
Microsoft: WAITFOR DELAY '0:0:10'
PostgreSQL: SELECT pg_sleep(10)
MySQL: SELECT sleep(10)
```

Tiếp tục test nhé, test xem dbms của nó là gì?

![image](https://github.com/user-attachments/assets/1b2f3730-5ffd-4b8f-b1a1-b08b5e568d59)

dbms là PostgreSQL và nó đã bị time based

![image](https://github.com/user-attachments/assets/065c8d19-1012-4de2-9064-b554541705e0)

Vì đề đã cho biết username là administrator rồi nên ta test thôi, thì time based nó đã hoạt động.

