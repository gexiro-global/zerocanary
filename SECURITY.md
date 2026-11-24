# Security Policy & Coordinated Vulnerability Disclosure

ZeroCanary is engineered around client-side zero-knowledge cryptography (`AES-256-GCM`, `PBKDF2-HMAC-SHA-256` at `600,000` iterations, mutual `SCRAM-SHA-256` challenge-response authentication, `HMAC-SHA-256` attestations, and decentralized threshold `secp256k1` release verification on ICP Mainnet).

## Reporting a Vulnerability

If you discover a cryptographic, authentication, plausible-deniability oracle, SSRF, cross-origin, or edge-infrastructure vulnerability affecting `https://zerocanary.com` or canister `sctry-7qaaa-aaaam-qjsuq-cai`, **do not open a public GitHub issue**.

Report findings privately to:

- **Security & Legal Desk:** `security@gexiro.com` / `legal@gexiro.com`
- **Canonical Policy (RFC 9116):** [https://zerocanary.com/.well-known/security.txt](https://zerocanary.com/.well-known/security.txt)

Please include:
1. Affected endpoint, URL parameter, canister method, or client-side cryptographic flow.
2. Deterministic, non-destructive reproduction steps.
3. Security impact assessment (confidentiality, integrity, time-lock bypass, plausible-deniability oracle, or availability).

## Verified Production Anchor & Scope

- **Active Edge Release:** `v1.2.5-p3-defense-in-depth` (`https://zerocanary.com`)
- **ICP Mainnet Notary Canister:** `sctry-7qaaa-aaaam-qjsuq-cai` (Live Wasm SHA-256: `b6b1721e7a64e5f92c2f05b8697b71e9c552b48ebd6289e5aac994b15c1033e6`)
- **In Scope:** `https://zerocanary.com`, `/api/v1/*` continuity endpoints, multi-file encrypted binary streaming (`/api/v1/vaults/:id/attachment`, up to `50 MB`), Envelope v3 three-role key-wrapping, SCRAM check-in verification, Duress plausible-deniability protections (`24h` coercion shield), the standalone Offline Recovery Kit (`.html`), and the client-side Zero-LLM In-RAM Navigator privacy boundary (`0` search queries sent over the network).
- **Out of Scope:** Volumetric denial-of-service (`DoS/DDoS`), social engineering, physical attacks, or automated destructive scanning against third-party payment processors (`Stripe`, `EVM RPCs`, `ICP Rosetta`).

We acknowledge valid reports promptly and remediate verified cryptographic or authorization issues with top priority.
