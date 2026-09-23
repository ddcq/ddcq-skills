---
name: security-review
description: Review a proposed or existing code change for security and privacy risks. Use when a change touches authentication, authorization, cookies, tokens, user data, uploads, payments, external input, secrets, network boundaries, dependencies, or infrastructure.
---

# Security Review

Read project security rules and the complete relevant diff or proposal. Identify trust boundaries, actors, assets, sensitive data, entry points, and security assumptions. Check authentication and authorization, input validation, injection, output encoding, CSRF, SSRF, path traversal, secrets, cryptography, session and cookie settings, logging, privacy, dependency risk, rate limiting, abuse cases, and fail-open behavior.

For each finding, provide evidence and a concrete remediation:

```text
Security result: PASS | PASS WITH RESERVATIONS | FAIL

Points motivating decision:
- [decisive fact, checked control, or finding severity justifying result]

Finding: [critical|high|medium|low] path:line
- Threat:
- Preconditions:
- Impact:
- Evidence:
- Recommended remediation:
- Verification:
```

Do not call a change secure merely because no issue was found. State what was not verified. Always fill `Points motivating decision`, whatever the result: list decisive facts, verified controls, or highest-severity findings justifying `PASS`, `PASS WITH RESERVATIONS`, or `FAIL`. Do not expose secrets encountered during investigation, and do not modify code unless explicitly asked.
