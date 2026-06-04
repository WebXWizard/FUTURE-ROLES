# QA Answer Framework

Use this structure when answering interview or project questions:

```txt
Context -> Requirement -> Risk -> Test design -> Execution -> Defect handling -> Result
```

## Example

Question:

```txt
How would you test a login page?
```

Answer structure:

```txt
I first read the requirement and acceptance criteria.
Then I identify risks such as invalid access, locked accounts, session handling, and security.
I create positive, negative, boundary, UI, API, database, security, and browser compatibility scenarios.
I prepare test data for valid user, invalid user, locked user, and reset password user.
During execution, I capture evidence and log defects with clear steps, expected result, actual result, severity, and screenshots.
Finally, I retest fixed defects and run regression around authentication and session flow.
```

## Strong QA Language

- I validate the requirement against acceptance criteria.
- I prioritize based on business risk.
- I separate test scenario, test case, and test data.
- I capture reproducible evidence.
- I retest the fix and run regression on related areas.
- I communicate impact, not only the error.

