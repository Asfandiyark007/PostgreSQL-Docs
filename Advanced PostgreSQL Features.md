# Advanced PostgreSQL Features
A backend developer should know about PostgreSQL’s advanced features that go beyond standard relational databases

## JSON & JSONB (NoSQL Capabilities):
PostgreSQL supports JSONB, a binary format that is faster than regular JSON.

```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    details JSONB NOT NULL
);
```
### Insert JSON data:
```sql
INSERT INTO products (name, details) VALUES
('Laptop', '{"brand": "Dell", "RAM": "16GB"}');
```
### Query JSON fields:
```sql
SELECT * FROM products WHERE details->>'brand' = 'Dell';
```

## Transactions & ACID Compliance:
PostgreSQL ensures Atomicity, Consistency, Isolation, Durability (ACID), preventing data corruption.
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```
### If something goes wrong:
```sql
ROLLBACK;
```
###  Full-Text Search:
PostgreSQL supports powerful full-text search without external engines like Elasticsearch.
```sql
CREATE INDEX idx_search ON posts USING GIN(to_tsvector('english', title || ' ' || content));
SELECT * FROM posts WHERE to_tsvector('english', title || ' ' || content) @@ to_tsquery('database');
```
### CTEs (Common Table Expressions):
Improve query readability and efficiency.
```sql
WITH recent_posts AS (
    SELECT * FROM posts ORDER BY created_at DESC LIMIT 5
)
SELECT * FROM recent_posts;
```

# PostgreSQL Performance Optimization
### Query Optimization:
Use `EXPLAIN ANALYZE` to debug slow queries:
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';
```
### Connection Pooling:
For high-performance apps, use PgBouncer to manage PostgreSQL connections efficiently.
### Caching with Redis:
Reduce database queries by caching frequent results.
```python
import redis
cache = redis.Redis(host='localhost', port=6379, db=0)
cache.set('user:1', '{"id": 1, "username": "john"}')
```
## Security Best Practices:
### User Roles & Permissions:
Create a read-only user:
```sql
CREATE USER readonly WITH PASSWORD 'securepass';
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly;
```
### Prevent SQL Injection:
Always use parameterized queries:
```python 
cursor.execute("SELECT * FROM users WHERE email = %s", (email,))
```
### Encrypting Data:
Use pgcrypto to store sensitive data securely.
```sql
SELECT crypt('my_password', gen_salt('bf'));
```

## ORMs & PostgreSQL:
Most backend frameworks use Object-Relational Mappers (ORMs) to interact with PostgreSQL.
### SQLAlchemy (Python):
```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.orm import declarative_base, sessionmaker

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    username = Column(String, unique=True, nullable=False)

engine = create_engine("postgresql://user:password@localhost/mydb")
Base.metadata.create_all(engine)
```
### Backup & Restore:
Backup PostgreSQL database:
```sh
pg_dump -U postgres -d mydb > backup.sql
```
### Restore database:
```sh
psql -U postgres -d mydb < backup.sql
```