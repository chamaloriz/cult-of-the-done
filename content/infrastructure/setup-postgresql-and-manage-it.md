---
title: Setup PostgreSQL and manage it
created: 2025-09-26
---
# Setup [PostgreSQL](https://www.postgresql.org/) and manage it

> [!warning] Work In Progress

```bash
sudo -u postgres psql
sudo -u postgres psql -d db
ssh -NL 1111:localhost:5432 server
sudo -u postgres pg_dump -U postgres -F c -b -v -f db.backup db
```

```sql
CREATE USER username WITH ENCRYPTED PASSWORD 'password';
CREATE DATABASE db;
GRANT ALL PRIVILEGES ON DATABASE db to username;
```
