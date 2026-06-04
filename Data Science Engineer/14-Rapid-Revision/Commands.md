# Commands

## SQL

```sql
SELECT segment, AVG(revenue)
FROM customers
GROUP BY segment;
```

## Python

```python
df.describe()
df.groupby("segment")["revenue"].mean()
```

