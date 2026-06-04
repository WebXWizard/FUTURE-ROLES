# API Test Cases

API test case categories:

- Valid request
- Missing required field
- Invalid field format
- Invalid auth token
- Expired token
- Unauthorized role
- Duplicate data
- Boundary values
- Large payload
- Wrong method
- Wrong content type
- Response schema
- Database validation

Example for login API:

```txt
Valid email and password returns 200 and token.
Invalid password returns 401.
Missing email returns 400 with clear error.
Locked account returns 403.
```

API evidence:

- Request URL
- Method
- Headers
- Body
- Status code
- Response body
- Timestamp

