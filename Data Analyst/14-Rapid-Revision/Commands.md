# Commands

## SQL

```sql
SELECT customer_id, COUNT(*) AS orders
FROM orders
GROUP BY customer_id;
```

## Python

```python
df.groupby("month")["revenue"].sum()
df.merge(customers, on="customer_id")
df.isna().sum()
```

