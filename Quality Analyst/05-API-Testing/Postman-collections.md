# Postman Collections

Postman helps create, run, and organize API tests.

Useful features:

- Collections
- Environments
- Variables
- Pre-request scripts
- Tests tab
- Collection runner
- Export and import

Basic validations:

```javascript
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});

pm.test("Response has id", function () {
  const body = pm.response.json();
  pm.expect(body).to.have.property("id");
});
```

Good collection design:

- Group APIs by feature.
- Use environment variables for base URL and tokens.
- Add positive and negative cases.
- Document expected behavior.

