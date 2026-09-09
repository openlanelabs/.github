# Security Policy

## Supported versions

| Version | Supported |
|---|---|
| `main` (pre-release) | ✅ security fixes |
| tagged releases | ✅ latest minor only |

## Reporting a vulnerability

**Please do not open public issues for security vulnerabilities.**

Email **security@openlane.dev** (PGP key published at `https://openlane.dev/.well-known/pgp.txt` once live).

Include:
- Type of issue (XSS, IDOR, RLS bypass, SSRF, injection, auth flaw, etc.)
- Full paths of affected files + reproduction steps
- Potential impact, including how an attacker might exploit it
- Version / commit SHA

### What to expect

- Acknowledgement within **48 hours**
- Assessment + severity rating within **5 business days**
- Fix timeline based on severity:
  - **Critical** (RLS bypass, auth bypass, RCE): patch within 7 days
  - **High**: patch within 30 days
  - **Medium/Low**: next scheduled release
- Credit in the release notes (opt-in)

## Scope

In scope:
- `openlanelabs/openlane` and all first-party code
- Self-hosted deployment defaults we ship (docker-compose, Helm)
- Our published packages and container images

Out of scope:
- Hosted cloud instances — report those to the same address but under your tenant SLA
- Attacks requiring physical access or compromised admin credentials
- Volume-based attacks (DoS) on our own infrastructure
- Social engineering of our team

## Hardening expectations for self-hosters

- Run with the provided `docker-compose.yml` defaults — RLS is enforced at the DB layer
- Do not disable `app.workspace_id` session variables
- Keep VaultS3 presigned-URL expiry short (default 15 min)
- Rotate all secrets; we never need your credentials to debug
