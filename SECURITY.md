# Security Policy & Coordinated Vulnerability Disclosure

ZeroCanary is engineered around client-side zero-knowledge cryptography (`AES-256-GCM`, `PBKDF2-HMAC-SHA-256` at `600,000` iterations, `Ed25519` seal signatures, and `SCRAM-SHA-256` challenge-response authentication).

## Reporting a Vulnerability

If you discover a cryptographic, authentication, plausible-deniability oracle, cross-origin, or edge-infrastructure vulnerability affecting `https://zerocanary.com`, **do not open a public GitHub issue**.

Report findings privately to:

- **Email:** `security@zerocanary.com`
- **Canonical Policy (RFC 9116):** `https://zerocanary.com/.well-known/security.txt`

Please include:
1. Affected endpoint, URL parameter, or client-side cryptographic flow.
2. Deterministic, non-destructive reproduction steps.
3. Security impact assessment (confidentiality, integrity, plausible-deniability oracle, or availability).

## Scope & Safe Harbor

- **In Scope:** `https://zerocanary.com`, `/api/v1/*` continuity endpoints, Envelope v3 key-wrapping, SCRAM check-in verification, Duress plausible-deniability protections, and the standalone Offline Recovery Kit (`.html`).
- **Out of Scope:** Volumetric denial-of-service (`DoS/DDoS`), social engineering, physical attacks, or automated destructive scanning against third-party payment processors.

We acknowledge valid reports promptly and remediate verified cryptographic or authorization issues with top priority.
