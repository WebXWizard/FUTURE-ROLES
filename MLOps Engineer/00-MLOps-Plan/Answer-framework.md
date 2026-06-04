# Answer Framework

Use this structure:

```txt
ML use case -> Data flow -> Training workflow -> Deployment strategy -> Monitoring -> Failure handling -> Improvement
```

Example:

```txt
For a churn model, I would version data, train reproducibly, log experiments, register the best model, deploy it behind an API, monitor latency and prediction drift, and trigger retraining when data changes meaningfully.
```

