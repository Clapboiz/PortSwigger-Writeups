## Challenge 1: Detecting NoSQL injection
## Challenge 2: Exploiting NoSQL operator injection to bypass authentication
## Challenge 3: Exploiting NoSQL injection to extract data
## Challenge 4: Exploiting NoSQL operator injection to extract unknown fields
## OPERATOR
### **1. Toán tử so sánh (Comparison Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$eq`      | Bằng (=) | `{ "age": { "$eq": 25 } }` |
| `$ne`      | Không bằng (!=) | `{ "age": { "$ne": 25 } }` |
| `$gt`      | Lớn hơn (>) | `{ "age": { "$gt": 18 } }` |
| `$gte`     | Lớn hơn hoặc bằng (>=) | `{ "age": { "$gte": 18 } }` |
| `$lt`      | Nhỏ hơn (<) | `{ "age": { "$lt": 18 } }` |
| `$lte`     | Nhỏ hơn hoặc bằng (<=) | `{ "age": { "$lte": 18 } }` |
| `$in`      | Có trong danh sách (giống `IN` trong SQL) | `{ "age": { "$in": [18, 20, 25] } }` |
| `$nin`     | Không có trong danh sách | `{ "age": { "$nin": [18, 20, 25] } }` |

---

### **2. Toán tử logic (Logical Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$and`     | Điều kiện AND | `{ "$and": [ { "age": { "$gt": 18 } }, { "city": "Hanoi" } ] }` |
| `$or`      | Điều kiện OR | `{ "$or": [ { "age": { "$gt": 18 } }, { "city": "Hanoi" } ] }` |
| `$not`     | Phủ định điều kiện | `{ "name": { "$not": { "$eq": "Lap" } } }` |
| `$nor`     | Phủ định cả danh sách điều kiện (giống `NOT (A OR B)`) | `{ "$nor": [ { "age": { "$gt": 18 } }, { "city": "Hanoi" } ] }` |

---

### **3. Toán tử đánh giá (Evaluation Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$regex`   | Tìm kiếm theo biểu thức chính quy | `{ "username": { "$regex": "^admin" } }` |
| `$expr`    | So sánh hai field trong document | `{ "$expr": { "$gt": [ "$salary", "$avgSalary" ] } }` |
| `$jsonSchema` | Xác thực dữ liệu theo JSON Schema | `{ "$jsonSchema": { "bsonType": "object", "properties": { "age": { "bsonType": "int" } } } }` |
| `$mod`     | Chia lấy dư (giống `%` trong toán học) | `{ "age": { "$mod": [2, 0] } }` (Tìm số chẵn) |
| `$text`    | Tìm kiếm toàn văn (Full-text search) | `{ "$text": { "$search": "security" } }` |
| `$where`   | Chạy JavaScript tùy chỉnh | `{ "$where": "this.age > 18" }` |

---

### **4. Toán tử mảng (Array Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$all`     | Chứa tất cả các giá trị trong mảng | `{ "tags": { "$all": ["mongodb", "security"] } }` |
| `$elemMatch` | Điều kiện cho ít nhất một phần tử trong mảng | `{ "grades": { "$elemMatch": { "score": { "$gt": 80 } } } }` |
| `$size`    | Kiểm tra độ dài của mảng | `{ "tags": { "$size": 3 } }` |

---

### **5. Toán tử phần tử (Element Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$exists`  | Kiểm tra field có tồn tại không | `{ "email": { "$exists": true } }` |
| `$type`    | Kiểm tra kiểu dữ liệu của field | `{ "age": { "$type": "int" } }` |

---

### **6. Toán tử bitwise (Bitwise Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$bitsAllSet`  | Kiểm tra tất cả các bit cụ thể được bật | `{ "flags": { "$bitsAllSet": 6 } }` |
| `$bitsAnySet`  | Kiểm tra ít nhất một bit cụ thể được bật | `{ "flags": { "$bitsAnySet": 6 } }` |
| `$bitsAllClear`| Kiểm tra tất cả các bit cụ thể bị tắt | `{ "flags": { "$bitsAllClear": 6 } }` |
| `$bitsAnyClear`| Kiểm tra ít nhất một bit cụ thể bị tắt | `{ "flags": { "$bitsAnyClear": 6 } }` |

---

### **7. Toán tử cập nhật (Update Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$set`     | Cập nhật giá trị field | `{ "$set": { "age": 30 } }` |
| `$unset`   | Xóa field | `{ "$unset": { "nickname": "" } }` |
| `$inc`     | Tăng giá trị số | `{ "$inc": { "score": 10 } }` |
| `$mul`     | Nhân giá trị số | `{ "$mul": { "salary": 1.1 } }` |
| `$rename`  | Đổi tên field | `{ "$rename": { "oldName": "newName" } }` |
| `$min`     | Giữ giá trị nhỏ nhất | `{ "$min": { "age": 25 } }` |
| `$max`     | Giữ giá trị lớn nhất | `{ "$max": { "age": 25 } }` |
| `$currentDate` | Cập nhật giá trị ngày hiện tại | `{ "$currentDate": { "lastLogin": true } }` |

---

### **8. Toán tử gán giá trị (Aggregation Operators)**
| **Toán tử** | **Ý nghĩa** | **Ví dụ** |
|------------|------------|-----------|
| `$add`     | Cộng giá trị số hoặc ngày tháng | `{ "$add": [ "$price", 5 ] }` |
| `$subtract`| Trừ giá trị số hoặc ngày tháng | `{ "$subtract": [ "$total", "$discount" ] }` |
| `$multiply`| Nhân giá trị số | `{ "$multiply": [ "$salary", 1.1 ] }` |
| `$divide`  | Chia giá trị số | `{ "$divide": [ "$price", 2 ] }` |
| `$round`   | Làm tròn giá trị số | `{ "$round": [ "$score", 2 ] }` |

---

## Cách phòng chống  

| **Phương pháp** | **Mô tả** |
|-----------------|----------|
| **Không chấp nhận JSON làm input** | Chỉ cho phép chuỗi đơn giản, không cho phép `{ "$ne": "" }`. |
| **Dùng bind parameters** | Không truyền trực tiếp input vào truy vấn MongoDB. |
| **Kiểm tra dữ liệu đầu vào** | Lọc bỏ các toán tử MongoDB như `$ne`, `$regex`, `$or`, `$and`... |

# REFERENCES
[1]. https://www.bmc.com/blogs/mongodb-operators/
