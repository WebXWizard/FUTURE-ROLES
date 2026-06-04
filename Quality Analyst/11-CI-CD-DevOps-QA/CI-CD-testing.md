# CI/CD Testing

CI means Continuous Integration.

CD means Continuous Delivery or Continuous Deployment.

QA tests in CI/CD:

- Unit tests
- API tests
- Smoke tests
- Regression tests
- Security checks
- Performance smoke checks

Pipeline test flow:

```txt
Code change -> Build -> Unit tests -> API smoke -> UI smoke -> Deploy to QA -> Regression -> Release decision
```

QA value:

- Keep smoke suites fast.
- Keep regression suites meaningful.
- Investigate failures quickly.
- Separate test failure from environment failure.

