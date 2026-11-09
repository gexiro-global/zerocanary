<p align="center">
  <a href="https://zerocanary.com">
    <img src="https://zerocanary.com/assets/og/og-card.png" alt="ZeroCanary — Sovereign Fiduciary Continuity & Client-Side Encrypted Dead Man's Switch" width="100%" />
  </a>
</p>

<p align="center">
  <a href="https://zerocanary.com"><img src="https://img.shields.io/badge/Platform-zerocanary.com-0d1117?style=for-the-badge&logo=shield&logoColor=C69B4B&labelColor=161b22&color=21262d" alt="zerocanary.com"></a>
  <a href="https://zerocanary.com/press"><img src="https://img.shields.io/badge/Press_%26_Media-Brand_Kit-0d1117?style=for-the-badge&logo=readthedocs&logoColor=C69B4B&labelColor=161b22&color=21262d" alt="Press & Media"></a>
  <a href="https://www.linkedin.com/showcase/zerocanary/"><img src="https://img.shields.io/badge/LinkedIn-ZeroCanary-0d1117?style=for-the-badge&logo=linkedin&logoColor=C69B4B&labelColor=161b22&color=21262d" alt="LinkedIn"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Encryption-AES--256--GCM_(WebCrypto)-10B981?style=flat-square" alt="AES-256-GCM">
  <img src="https://img.shields.io/badge/KDF-PBKDF2--SHA256_(600k)-0284C7?style=flat-square" alt="PBKDF2 600k">
  <img src="https://img.shields.io/badge/Auth-SCRAM--SHA256_%2B_Ed25519-6366F1?style=flat-square" alt="SCRAM + Ed25519">
  <img src="https://img.shields.io/badge/Recovery-100%25_Air--Gapped_.html-D97706?style=flat-square" alt="Air-Gapped HTML">
</p>

---

# ZeroCanary

**Client-side encrypted fiduciary continuity vault, Dead Man's Switch, and air-gapped recovery architecture for private individuals, founders, family offices, and legal counsel.**

ZeroCanary enables asset owners to seal succession directives, recovery credentials, corporate continuity instructions, and encrypted binary attachments (`.pdf`, `.zip`, `.key`, `.txt`) inside the browser before any byte leaves the device. No user account, email registration, or plaintext key custody is required.

> **Repository Scope:** This repository serves as the official public architectural specification, verification reference, and security disclosure hub for **ZeroCanary** (`https://zerocanary.com`). Production edge workers, canister infrastructure, and client enclaves are maintained in sovereign private infrastructure by Gexiro Global Enterprises Ltd.

---

## Core Cryptographic & Continuity Architecture

| Capability | Technical Implementation | Operational Guarantee |
| :--- | :--- | :--- |
| **Client-Side Zero-Knowledge Sealing** | Native browser WebCrypto (`AES-256-GCM`, `PBKDF2-HMAC-SHA-256` at `600,000` iterations, `Ed25519` seal signatures) | Plaintext directives, files, and passwords never leave the client browser. |
| **Envelope v3 Cryptographic Role Separation** | Independent DEK key-wrapping (`ownerWrap`, `onlineWrap`, `offlineAirgapWrap`) | Owners can assign a dedicated **Recipient Unlock Password** for heirs or legal counsel without sharing their **Owner Main Password** or **Emergency Duress Password**. |
| **Replay-Resistant Two-Way Check-Ins** | Challenge-response `SCRAM-SHA-256` proofs bound to action, payload digest, timestamp, and single-use server nonces | Owners confirm presence, extend timers (`1h` to `365d`), edit instructions, and replace encrypted attachments while preserving recipient key-wraps. |
| **Zero-Oracle Coercion Shield (Plausible Deniability)** | Indistinguishable `HEARTBEAT_VERIFIED` duress flow + decoy cover note + decoy offline kit + `24h` public `423 Locked` shield | Under physical coercion, an attacker sees a routine check-in and harmless cover note while authorized counsel receives an HMAC-signed webhook with an immediate recovery token (`?ert=`). |
| **100% Air-Gapped Offline Recovery Kit (`.html`)** | Self-contained, zero-dependency HTML + WebCrypto bundle operating from `file:///` offline | Designated recipients can decrypt released instructions and binary files on an air-gapped machine even without internet connectivity. Includes built-in localization (`EN`, `DE`, `ES`, `FR`, `PL`). |
| **Decentralized Threshold Continuity Notary** | Autonomous on-chain commitment anchoring + threshold `secp256k1` release attestation | Independent public proof verification by `SHA-256` digest without exposing sealed metadata while active. |
| **Fiduciary Handover Toolkit** | Printable Safe / Notary Handover Certificate + RFC 5545 `.ics` check-in schedule + `24h` pre-expiry webhook alert | Designed for physical safe-deposit envelopes, estate attorneys, and institutional continuity binders. |

---

## Lifecycle Flow

```text
[Browser Client (WebCrypto)]
   │
   ├─ 1. Seal Deposit (Tab 1)
   │     ├─ Derive keys via PBKDF2-SHA-256 (600,000 iterations)
   │     ├─ Encrypt directive + optional binary file with AES-256-GCM (Envelope v3)
   │     ├─ Wrap DEK separately for Owner Main Password & Recipient Unlock Password
   │     ├─ Seal independent Decoy Cover Note under Emergency Duress Password
   │     └─ Export Air-Gapped Offline Recovery Kit (.html) + Notary Handover Certificate + .ics
   │
   ├─ 2. Periodic Check-In & Two-Way Edit (Tab 2)
   │     ├─ Normal Password  ──► Resets Dead Man's Switch timer & unlocks live payload editor
   │     └─ Duress Password  ──► Displays Decoy Cover Note, activates 24h 423 Coercion Shield,
   │                             and dispatches HMAC-signed emergency counsel webhook (?ert=)
   │
   └─ 3. Continuity Disclosure & Recipient Recovery (Tab 4 / Air-Gapped .html)
         ├─ Triggered on countdown expiration (00:00:00) or authorized emergency token
         └─ Recipient unlocks directive & files locally using Recipient Unlock Password
```

---

## Continuity Plans & Settlement

ZeroCanary operates on anonymous bearer continuity passes (`ZC-...`) without user accounts or recurring auto-charge traps.

| Tier | Cadence & Scope | Settlement |
| :--- | :--- | :--- |
| **Evaluation Sandbox** | `$0` · `1-hour` test cadence · full client-side encryption & offline kit verification | Instant access (`No card required`) |
| **Private Sovereign Pass** | `$49` (`3m`) · `$89` (`6m`) · `$149` (`12m`) · up to `10` active deposits · `24h–365d` cadences · encrypted file attachments | **Active:** Stripe Institutional Checkout (`Card`, `Apple Pay`, `Google Pay`) |
| **Law Firm & Family Office (`COUNSEL`)** | `$490 / year` · **unlimited** active client deposits · B2B invoice receipt · HMAC webhook automation & notary certificates | **Active:** Stripe Institutional B2B Checkout |
| **Sovereign Crypto Settlement** | `BTC · USDC · ETH` non-custodial bearer pass issuance without card network footprint | **Planned Roadmap** |

---

## Public Verification & Machine-Readable Specifications

- **Live Enclave & Continuity Console:** [https://zerocanary.com](https://zerocanary.com)
- **Standalone SHA-256 Proof Lookup:** `https://zerocanary.com/?verify=<64-hex-sha256>`
- **Press & Brand Assets (`EN / DE / ES / FR / PL`):** [https://zerocanary.com/press](https://zerocanary.com/press)
- **LLM & Technical Architecture Summary:** [https://zerocanary.com/llms.txt](https://zerocanary.com/llms.txt)
- **Vulnerability Disclosure Policy (RFC 9116):** [https://zerocanary.com/.well-known/security.txt](https://zerocanary.com/.well-known/security.txt) · [SECURITY.md](SECURITY.md)

---

## Legal & Governance

Operated by **[Gexiro Global Enterprises Ltd](https://gexiro.com)** (Gibraltar). EU sovereign ciphertext storage jurisdiction with decentralized on-chain timestamp notarization.

© Gexiro Global Enterprises Ltd. All rights reserved.
