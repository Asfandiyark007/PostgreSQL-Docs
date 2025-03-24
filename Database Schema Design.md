#  Database Schema Design
A backend developer should understand how to design a scalable database schema.

##  Creating Tables

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Relationships (Foreign Keys)
```sql
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id) ON DELETE CASCADE,
    title TEXT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
* One-to-Many Relationship: One user can have multiple posts.

* ON DELETE CASCADE: If a user is deleted, all their posts are deleted.

## Indexing for Performance
Indexes speed up queries on large table
```sql
CREATE INDEX idx_users_email ON users(email);
```
* B-Tree Indexes (default) improve performance for WHERE, JOIN, and ORDER BY queries.

* GIN Indexes are great for searching JSONB data.