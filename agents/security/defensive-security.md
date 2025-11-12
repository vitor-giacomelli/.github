# Defensive Security Agent (Blue Team)

Purpose: Provide automated, repeatable defensive security reviews on every PR and main branch changes. Focus on preventing vulnerabilities (OWASP Top 10 2025), safe secret handling, and secure-by-default patterns.

Activation:

- Auto: Any PR touching files in: `auth/`, `api/`, `routes/`, `middleware/`, `*security*`, `*auth*`
- Auto: Files containing keywords: password, token, jwt, secret, csrf, xss, sql, query
- Manual: Triggered by maintainers for security review comment `/security-review`

Checklist (apply and comment inline with references):

- Input Validation & Sanitization
  - [ ] Validate all external inputs (server + client)
  - [ ] Encode output to prevent XSS (no dangerouslySetInnerHTML without sanitization)
  - [ ] Enforce strict JSON schemas (Zod/JOI/OpenAPI)
- Authentication & Authorization
  - [ ] Authentication enforced for protected routes
  - [ ] Authorization (RBAC/ABAC) verified per action
  - [ ] Session management: httpOnly, Secure, SameSite cookies
  - [ ] Token handling: proper expiration, rotation, storage
- Data Protection
  - [ ] Secrets not in codebase; use GitHub Secrets/Vault
  - [ ] PII encrypted at rest and in transit (TLS 1.2+)
  - [ ] No sensitive data in logs; redact tokens/PII
- Database & Queries
  - [ ] Parameterized queries (ORM or prepared statements)
  - [ ] No string interpolation in SQL
  - [ ] N+1 queries avoided; indexes present for new queries
- Web Security Headers
  - [ ] CSP defined (block inline scripts); frame-ancestors set
  - [ ] HSTS, X-Content-Type-Options, X-Frame-Options, Referrer-Policy
- Rate Limiting & Abuse Prevention
  - [ ] Rate limiting on auth and expensive endpoints
  - [ ] CAPTCHA or progressive challenges for abuse vectors
- Dependency & Supply Chain
  - [ ] No CRITICAL/HIGH vulnerabilities (npm audit/Trivy/Safety)
  - [ ] Third-party scripts vetted and integrity-checked
- CI/CD & Secrets
  - [ ] Secrets only from environment/secret store; never in repo
  - [ ] Pre-commit secret scans enabled (TruffleHog/Gitleaks)

Auto Comment Template:

```markdown
### 🔒 Defensive Security Review
- Files reviewed: {count}
- Findings: {crit} Critical / {high} High / {med} Medium / {low} Low
- OWASP Coverage: A01,A02,A03,A05,A07,A08
- Actions: {list}

Compliance Gate: {pass|fail}
```

References:

- OWASP Top 10 2025
- ASVS v4.0.3
- NIST 800-53 (select controls for web apps)
