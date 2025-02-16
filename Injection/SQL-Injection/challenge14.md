![image](https://github.com/user-attachments/assets/4bc9f14a-fcf7-4a98-8ed7-ece15aa31cd1)

Nó yêu cầu mình gây ra time based 10s. Cứ thử hết sleep của các dbms nhé, sau khi thử thì ta biết được nó là postgresql sqli.

![image](https://github.com/user-attachments/assets/2c8c415a-ebbe-4f1e-b8fb-a48320ab1e35)

![image](https://github.com/user-attachments/assets/442e8433-6c74-4b13-a8b2-945f949917d3)

Vậy là thành công rồi đó.

Payload:

```
'||pg_sleep(10)--+
```
