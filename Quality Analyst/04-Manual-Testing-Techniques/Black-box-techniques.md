# Black Box Techniques

Black box testing checks behavior without looking at internal code.

## Equivalence Partitioning

Divide input into valid and invalid groups.

Example:

```txt
Age 18-60 valid
Age below 18 invalid
Age above 60 invalid
```

## Boundary Value Analysis

Test near the edges.

Example:

```txt
17, 18, 19, 59, 60, 61
```

## Decision Table

Use when output depends on combinations of conditions.

## State Transition

Use when behavior changes based on state.

Example:

```txt
Active account -> Locked account -> Password reset -> Active account
```

