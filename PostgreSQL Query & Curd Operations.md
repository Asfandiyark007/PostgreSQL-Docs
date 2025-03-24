#  PostgreSQL Querying & CRUD Operations
### Insert Data:
```sql
INSERT INTO users (username, email, password) VALUES
('john_doe', 'john@example.com', 'hashed_password');
```
### Retrieve Data:
```sql
SELECT * FROM users WHERE username = 'john_doe';
```
### Update Data:
```sql
UPDATE users SET email = 'newemail@example.com' WHERE username = 'john_doe';
```
### Delete Data:
```sql
DELETE FROM users WHERE username = 'john_doe';
```
