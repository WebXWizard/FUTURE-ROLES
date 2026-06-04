# Data Validation

Data validation checks whether the data shown in UI or API is correct in the database.

Check:

- Created data saved correctly.
- Updated data changed correctly.
- Deleted data removed or marked inactive.
- Duplicate records not created.
- Required fields are not null.
- Values match business rules.
- Dates and time zones are correct.
- Amount calculations are accurate.

Example:

```txt
After placing an order, verify order ID, user ID, amount, status, payment ID, and timestamp in the database.
```

