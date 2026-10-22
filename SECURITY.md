# Security and demo-use guidance

This is coursework, not an audited service. No supported-release programme or response deadline is established here.

## Immediate review priorities

- All auth routes are permitted publicly, including the controller's administrator-registration path. Do not expose it as a production provisioning flow.
- Database credentials and the JWT signing key are committed. If used for real infrastructure, rotate them and review history/exports. Removing current text alone does not remove historical copies. The overlay does not change configuration.
- Resource reads are public under the declared rules, including employee names, emails and salary fields. Do not use real employee data.
- Login returns distinct user-not-found and password-failure messages. No rate limiting, password policy, token revocation or account lockout is supplied in these paths.
- Request models have no supplied validation constraints. Registration's existence check is not proof of a database uniqueness constraint or concurrency-safe registration.
- Duplicate bean definitions and differing CORS declarations require effective-runtime verification. CORS is not an authorisation boundary.
- Security TRACE logging is enabled. Review logging and redaction before handling real tokens or personal data.

These are static observations, not executed exploit results or a complete audit. No fixes are included.

Use a verified private maintainer channel for sensitive reports if available, or request one without publishing secrets. No dedicated security mailbox or enabled private-reporting feature was confirmed. Use synthetic reproductions and redact connection strings, passwords and tokens.
