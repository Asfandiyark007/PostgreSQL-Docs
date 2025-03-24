# 1. PostgreSQL Basics
## 1.1 Installation & Setup:
#### Install PostgreSQL:
* Linux/macOS: `sudo apt install postgresql` (Ubuntu) or `brew install postgresql` (Mac)

* Windows: Install via [official PostgreSQL installer](https://www.postgresql.org/download/).

Start and stop PostgreSQL service ( LINUX ):
<pre><code>sudo systemctl start postgresql
sudo systemctl stop postgresql
</code></pre>

For windows add the `PATH` to Environment Varibale in my case it was   `C:\Program Files\PostgreSQL\17\bin`

## Access PostgreSQL shell:
```console
psql -U postgres
```

## 1.2 Creating & Managing Databases:

#### Create a new database:
```sql
CREATE DATABASE myapp;
```

#### Connect to a database:
```sh
psql -U postgres -d myapp
```

#### List databases:
```sql
\l
```
#### Drop a database:
```sql
DROP DATABASE myapp;
```

