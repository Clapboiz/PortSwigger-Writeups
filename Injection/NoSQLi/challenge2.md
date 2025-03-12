![image](https://github.com/user-attachments/assets/691e58a9-6719-4251-8f3a-9302e7dd7fe9)

![image](https://github.com/user-attachments/assets/ce8e5331-9c40-429a-b873-f0ba8bb9882a)

Tiến hành thử với toán tử $ne `(!=)` thì ta có thể thấy được rằng nó đã bypass được login :>, tức là chỉ cần username khác rỗng thì nó sẽ pick đại 1 thằng username nào đó và nó check thằng password xem khớp thì nó login được thôi v:v:

![image](https://github.com/user-attachments/assets/50c5314f-5b5b-4583-858a-8f65e52a748e)

![image](https://github.com/user-attachments/assets/1f3b3d97-0a2d-41fe-a997-6b96022162e0)

Như chúng ta có thể thấy được rằng khi chúng ta dùng toán tử `$regex` thì đầu tiên nó sẽ check xem có username nào bắt đầu bằng chữ admin (ở trên) hoặc a (ở dưới) hay không?

Thì câu trả lời là có nên nó mới trả về url chứa username và cookie được cấp cho acc đó đấy

![image](https://github.com/user-attachments/assets/04a9243e-396f-461e-bad9-178ea2b7ed14)

Thì vậy là thành công.

Và bạn có thắc mắc tại sao có 2 cách trên không? :")) và nó khác nhau như này nè.

| Biểu thức regex      | Giải thích | Ví dụ khớp | Ví dụ không khớp |
|----------------------|-----------|------------|-------------------|
| `"admin.*"`         | Bắt đầu với `admin`, sau đó có thể là bất kỳ ký tự nào (`.`) xuất hiện bất kỳ số lần (`*`). | `admin`, `admin123`, `administrator`, `admin_test` | `user_admin`, `adm` |
| `"admin*"`          | Ký tự `n` có thể lặp lại nhiều lần (`*` chỉ ảnh hưởng đến ký tự trước đó). | `admin`, `adminn`, `adminnn` | `admin123`, `administrator`, `admin_test` |
| `"^admin"`          | Bắt đầu với `admin`, không yêu cầu ký tự sau. | `admin`, `admin123`, `administrator`, `admin_test` | `user_admin`, `adm` |
| `"^admin$"`         | Chính xác là `admin`, không có ký tự nào khác. | `admin` | `admin123`, `administrator`, `admin_test` |

