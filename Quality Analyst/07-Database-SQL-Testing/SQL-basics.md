# SQL Basics

Common SQL commands for QA:

```sql
SELECT * FROM users;
SELECT id, email FROM users WHERE email = 'test@example.com';
SELECT COUNT(*) FROM orders WHERE status = 'PAID';
SELECT * FROM orders ORDER BY created_at DESC;
```

Useful concepts:

- Table
- Row
- Column
- Primary key
- Foreign key
- `WHERE`
- `JOIN`
- `GROUP BY`
- `ORDER BY`
- `COUNT`
- `SUM`
- `MAX`
- `MIN`

QA habit:

- Always validate expected database changes after create, update, delete, and workflow completion.

