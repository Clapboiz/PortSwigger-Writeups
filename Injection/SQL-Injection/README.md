## Challenge 1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
## Challenge 2: SQL injection vulnerability allowing login bypass
## Challenge 3: SQL injection attack, querying the database type and version on Oracle
## Challenge 4: SQL injection attack, querying the database type and version on MySQL and Microsoft
## Challenge 5: SQL injection attack, listing the database contents on non-Oracle databases
## Challenge 6: SQL injection attack, listing the database contents on Oracle
## Challenge 7: SQL injection UNION attack, determining the number of columns returned by the query
## Challenge 8: SQL injection UNION attack, finding a column containing text
## Challenge 9: SQL injection UNION attack, retrieving data from other tables
## Challenge 10: SQL injection UNION attack, retrieving multiple values in a single column
## Challenge 11: Blind SQL injection with conditional responses
## Challenge 12: Blind SQL injection with conditional errors
## Challenge 13: Visible error-based SQL injection
## Challenge 14: Blind SQL injection with time delays
## Challenge 15: Blind SQL injection with time delays and information retrieval
## Challenge 16: Blind SQL injection with out-of-band interaction
## Challenge 17: Blind SQL injection with out-of-band data exfiltration
## Challenge 18: SQL injection with filter bypass via XML encoding

1. MySQL

Trong MySQL, thông tin về cơ sở dữ liệu, bảng và cột được lưu trong information_schema:

+ information_schema.tables: Chứa danh sách các bảng.
+ information_schema.columns: Chứa danh sách các cột.

2. PostgreSQL

Trong PostgreSQL, thông tin về cơ sở dữ liệu được lưu trong các bảng pg_catalog:

+ pg_catalog.pg_tables: Chứa danh sách các bảng.
+ pg_catalog.pg_attribute: Chứa danh sách các cột.

3. SQL Server

Trong SQL Server, thông tin về cơ sở dữ liệu được lưu trong bảng hệ thống:

+ sys.tables: Chứa danh sách các bảng.
+ sys.columns: Chứa danh sách các cột.

4. Oracle

Trong Oracle, thông tin về cơ sở dữ liệu, bảng và cột được lưu trong các dictionary views:

+ USER_TABLES: Chứa danh sách các bảng thuộc user hiện tại.
+ USER_TAB_COLUMNS: Chứa danh sách các cột trong các bảng của user hiện tại.
