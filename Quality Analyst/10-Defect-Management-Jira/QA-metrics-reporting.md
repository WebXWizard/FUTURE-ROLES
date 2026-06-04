# QA Metrics And Reporting

QA metrics help explain test progress and release risk.

Common metrics:

- Test cases planned
- Test cases executed
- Pass count
- Fail count
- Blocked count
- Defects by severity
- Defects by status
- Defect density
- Test coverage
- Automation pass rate

Daily QA status format:

```txt
Today tested: checkout payment and order confirmation.
Passed: 18
Failed: 3
Blocked: 1
Critical defects: 1
Risk: payment retry flow not testable due to environment issue.
Next: retest fixes and run regression on order history.
```

