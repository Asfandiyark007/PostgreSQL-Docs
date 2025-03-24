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
