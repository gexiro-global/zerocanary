<p align="center">
  <a href="https://zerocanary.com">
    <img src="https://zerocanary.com/assets/og/og-card.png?v=3" alt="ZeroCanary — Sovereign Fiduciary Continuity & Client-Side Encrypted Dead Man's Switch" width="100%" />
  </a>
</p>

<p align="center">
  <a href="https://zerocanary.com"><img src="https://img.shields.io/badge/Platform-zerocanary.com-0d1117?style=for-the-badge&logo=shield&logoColor=C9A45C&labelColor=161b22&color=21262d" alt="zerocanary.com"></a>
  <a href="https://zerocanary.com/press"><img src="https://img.shields.io/badge/Press_%26_Media-Brand_Kit-0d1117?style=for-the-badge&logo=readthedocs&logoColor=C9A45C&labelColor=161b22&color=21262d" alt="Press & Media"></a>
  <a href="https://www.linkedin.com/showcase/zerocanary/"><img src="https://img.shields.io/badge/LinkedIn-ZeroCanary-0d1117?style=for-the-badge&logo=linkedin&logoColor=C9A45C&labelColor=161b22&color=21262d" alt="LinkedIn"></a>
  <a href="https://x.com/zerocanary_com"><img src="https://img.shields.io/badge/X-@zerocanary__com-0d1117?style=for-the-badge&logo=x&logoColor=C9A45C&labelColor=161b22&color=21262d" alt="X @zerocanary_com"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Encryption-AES--256--GCM_(WebCrypto)-10B981?style=flat-square" alt="AES-256-GCM">
  <img src="https://img.shields.io/badge/KDF-PBKDF2--SHA256_(600k)-0284C7?style=flat-square" alt="PBKDF2 600k">
  <img src="https://img.shields.io/badge/Auth-SCRAM--SHA256_%2B_Threshold_secp256k1-6366F1?style=flat-square" alt="SCRAM + Threshold secp256k1">
  <img src="https://img.shields.io/badge/Attachments-Multi--File_%E2%89%A450_MB-14B8A6?style=flat-square" alt="Multi-File <= 50 MB">
  <img src="https://img.shields.io/badge/Recovery-Air--Gapped_.html-D97706?style=flat-square" alt="Air-Gapped HTML">
</p>

---

# ZeroCanary

**Client-side encrypted fiduciary continuity vault, Dead Man's Switch, and air-gapped recovery architecture for private individuals, founders, family offices, and legal counsel worldwide.**

ZeroCanary enables asset owners to seal succession directives, recovery credentials, corporate continuity instructions, and multi-file binary archives (`.pdf`, `.zip`, `.7z`, `.key`, `.jpg`, `.docx`, up to `50 MB` per deposit, auto-bundled in-browser) before any byte leaves the device. No user account, email registration, or plaintext key custody is required.

> **Repository Scope:** This repository serves as the official public architectural specification, verification reference, and security disclosure hub for **ZeroCanary** (`https://zerocanary.com`). Production edge infrastructure, threshold notary canisters, and client enclaves are maintained in sovereign private infrastructure by Gexiro Global Enterprises Ltd.

---

## Core Cryptographic & Dual-Plane Continuity Architecture

| Capability | Technical Implementation | Operational Guarantee |
| :--- | :--- | :--- |
| **Client-Side Zero-Knowledge Sealing (`<= 50 MB` Multi-File)** | Native browser W3C WebCrypto (`AES-256-GCM`, `PBKDF2-HMAC-SHA-256` at `600,000` iterations) + in-browser multi-file `PKZIP` bundling | Plaintext directives, files, and passwords never leave the client browser. |
| **Dual-Plane Zero-Knowledge Custody & Threshold Notary** | Sovereign European Union zero-knowledge object custody (`AES-256-GCM` ciphertext streams) + autonomous decentralized threshold notary (`SHA-256` commitments & `secp256k1` release attestations) | Zero plaintext visibility at the storage layer combined with tamper-evident on-chain countdown and release verification. |
| **Envelope v3 Three-Role Key Separation** | Independent DEK key-wrapping (`ownerWrap`, `onlineWrap`, `offlineAirgapWrap`) | Owners assign a dedicated **Recipient Unlock Password** for heirs or legal counsel without sharing their **Owner Main Password** or **Emergency Duress Password**. |
| **Replay-Resistant Two-Way Check-Ins** | Mutual challenge-response `SCRAM-SHA-256` proofs bound to action, payload digest, timestamp, and single-use server nonces | Owners confirm presence, extend timers (`1h` to `365d`), edit instructions, and add or replace encrypted attachments while preserving recipient key-wraps. |
| **Zero-Oracle Coercion Shield (Plausible Deniability)** | Indistinguishable `HEARTBEAT_VERIFIED` duress flow + decoy cover note + decoy offline kit + `24h` public `423 Locked` shield | Under physical coercion, an attacker sees a routine check-in and harmless cover note while authorized counsel receives an HMAC-signed webhook with an immediate recovery token (`?ert=`). |
| **Standalone Air-Gapped Offline Recovery Kit (`.html`)** | Self-contained, zero-dependency HTML + WebCrypto decryptor with built-in multilingual UI | Embeds ciphertext up to `20 MB` directly inside the `.html` file for 100% air-gapped offline decryption (`file:///`) and streams larger `20–50 MB` encrypted archives from EU zero-knowledge custody upon release. |
| **Fiduciary Handover Toolkit** | Printable Safe / Notary Handover Certificate + RFC 5545 `.ics` check-in schedule + `24h` pre-expiry webhook alert | Designed for physical safe-deposit envelopes, estate attorneys, and institutional continuity binders. |

---

## Lifecycle Flow

```text
[Browser Client (W3C WebCrypto)]
   │
   ├─ 1. Seal Deposit (Tab 1)
   │     ├─ Derive keys via PBKDF2-HMAC-SHA-256 (600,000 iterations)
   │     ├─ Bundle multi-file attachments (<= 50 MB) & encrypt with AES-256-GCM (Envelope v3)
   │     ├─ Stream ciphertext to EU Zero-Knowledge Custody & anchor SHA-256 on Threshold Notary
   │     ├─ Wrap DEK separately for Owner Main Password & Recipient Unlock Password
   │     ├─ Seal independent Decoy Cover Note under Emergency Duress Password
   │     └─ Export Air-Gapped Offline Recovery Kit (.html) + Notary Handover Certificate + .ics
   │
   ├─ 2. Periodic Check-In & Two-Way Edit (Tab 2)
   │     ├─ Main Password    ──► Mutual SCRAM-SHA-256 proof resets timer & unlocks live editor
   │     └─ Duress Password  ──► Displays Decoy Cover Note, activates 24h 423 Coercion Shield,
   │                             and dispatches HMAC-signed emergency counsel webhook (?ert=)
   │
   └─ 3. Continuity Disclosure & Recipient Recovery (Tab 4 / Standalone .html)
         ├─ Triggered on countdown expiration (00:00:00) or authorized emergency token
         └─ Recipient unlocks directive & files locally using Recipient Unlock Password
```

---

## Continuity Plans & Global Settlement

ZeroCanary operates worldwide on anonymous bearer continuity passes (`ZC-...`) without user accounts or recurring auto-charge traps.

| Tier | Cadence & Scope | Settlement |
| :--- | :--- | :--- |
| **Evaluation Sandbox** | `$0` · `1-hour` test cadence · client-side encryption, three-role passwords & offline kit verification | Instant access (`No card required`) |
| **Private Sovereign Pass** | `$49` (`3m`) · `$89` (`6m`) · `$149` (`12m`) · up to `10` active deposits · `24h–365d` cadences · multi-file attachments (`<= 50 MB`) + `30-day` grace | **Active:** Stripe Institutional Checkout (`Apple Pay`, `Google Pay`, `Payment Cards`, `Instant Bank Transfers`) |
| **Law Firm & Family Office (`COUNSEL`)** | `$490 / year` · **unlimited** active client deposits · multi-file attachments (`<= 50 MB`) · HMAC webhook automation & B2B VAT invoice | **Active:** Stripe Institutional B2B Checkout |
| **Sovereign Crypto Settlement** | `BTC · USDC · ETH` non-custodial bearer pass issuance without banking intermediaries | **Planned Roadmap** |

---

## Public Verification & Machine-Readable Specifications

- **Live Enclave & Continuity Console:** [https://zerocanary.com](https://zerocanary.com)
- **Official Brand Identity (Fiduciary Shield):** [https://zerocanary.com/press#brand-assets](https://zerocanary.com/press#brand-assets)
- **Official LinkedIn Showcase:** [https://www.linkedin.com/showcase/zerocanary/](https://www.linkedin.com/showcase/zerocanary/)
- **Official X Channel:** [https://x.com/zerocanary_com](https://x.com/zerocanary_com) (`@zerocanary_com`)
- **Standalone SHA-256 Proof Lookup:** [https://zerocanary.com/tools/sha256-notary](https://zerocanary.com/tools/sha256-notary)
- **Continuity Readiness & Bus-Factor Audit:** [https://zerocanary.com/tools/continuity-score](https://zerocanary.com/tools/continuity-score)
- **Architecture Briefings:** [https://zerocanary.com/briefings](https://zerocanary.com/briefings)
- **LLM & Technical Architecture Summary:** [https://zerocanary.com/llms.txt](https://zerocanary.com/llms.txt)
- **Vulnerability Disclosure Policy (RFC 9116):** [https://zerocanary.com/.well-known/security.txt](https://zerocanary.com/.well-known/security.txt) · [SECURITY.md](SECURITY.md)

---

## Legal & Governance

Operated by **[Gexiro Global Enterprises Ltd](https://gexiro.com)** (Gibraltar). Sovereign European Union zero-knowledge ciphertext custody paired with decentralized threshold timestamp notarization.

© Gexiro Global Enterprises Ltd. All rights reserved.
