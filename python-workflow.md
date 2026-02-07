## Python Pipeline

```
    [ START ]
        │
  1.  PLANNING      (Requirements & Design)
        │
  2.  SETUP         (Virtual Env & Packages)
        │
  ┌─────┴────────┐
  │ 3. CODE      │ <───┐
  │      │       │     │
  │    RUN       │   DEBUG
  │      │       │     │
  │    TESTS ────┼─────┘
  └─────┬────────┘
        │ (Pass)
        ▼
  4.  REFACTOR      (Clean up code)
        │
  5.  RELEASE       (Docs & Deployment)
        │
     [ END ]
```
