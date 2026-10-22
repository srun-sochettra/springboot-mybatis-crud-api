# Contributing

Keep changes focused on the existing controller/service/MyBatis structure. Use synthetic employees, products and accounts in an isolated database.

Run the proposed wrapper checks and report actual results. The context smoke test does not establish API behaviour. Prioritise controlled administrator provisioning, effective bean wiring, missing schema, request validation and dependency compatibility before claiming a working secure service.

For mapper changes, test generated keys, null values, missing IDs and actual PostgreSQL round trips. For auth changes, test unauthenticated writes, USER/ADMIN permissions, invalid/expired tokens, duplicate registration and server-controlled roles. Never disable assertions or security checks just to obtain a passing build.

Describe the problem, focused change, checks, data impact and rollback in pull requests. Keep credentials, tokens, real employee records and generated target files out of commits. Follow [SECURITY.md](SECURITY.md) for sensitive reports.
