# ZeroCanary Technical Architecture & Cryptographic Verification Specification

> **Document Scope:** Public architecture, cryptographic trust boundaries, threat-model invariants, and external verification parameters for **ZeroCanary** (`https://zerocanary.com`). Proprietary source code is intentionally omitted from this repository.

---

## 1. Zero-Knowledge Threat Model & Sovereign Plane Separation

ZeroCanary separates **data confidentiality**, **ciphertext persistence**, and **temporal release authority** across independent boundaries:

| Plane | Responsible Component | Visibility Guarantee |
| :--- | :--- | :--- |
| **Client Enclave (RAM)** | User browser via native W3C WebCrypto API | Full plaintext directives, multi-file attachments (`<= 50 MB`), `Owner Main Password`, `Recipient Unlock Password`, and `Emergency Duress Password`. Plaintext and raw keys never leave device memory. |
| **EU Object Custody** | European Union R2 Bucket (`EU / eeur` jurisdiction) | Stores exclusively `AES-256-GCM` ciphertext envelopes (`Envelope v3`), encrypted `PKZIP` attachments, `SCRAM` verifier salts/stored-keys, and SHA-256 hashed license metadata. Zero plaintext visibility. |
| **Threshold Notary** | Autonomous ICP Mainnet Canister (`sctry-7qaaa-aaaam-qjsuq-cai`) | Records immutable `SHA-256` payload commitments, autonomous deadline sweep timestamps, and threshold `secp256k1` ECDSA release attestations. |

---

## 2. Envelope v3 Key Hierarchy (Three-Role Separation)

Each sealed deposit binds a randomly generated 256-bit Data Encryption Key (`DEK`) across three strictly separated roles:

1. **Owner Main Role (`ownerWrap`):**
   - Derived client-side via `PBKDF2-HMAC-SHA-256` (`600,000` iterations) with unique per-deposit salt.
   - Governs live check-ins and encrypted two-way deposit updates (`PUT /api/v1/vaults/:id`) authenticated with mutual `RFC 5802 SCRAM-SHA-256` challenge-response proofs bound to action, payload hash, timestamp, and single-use nonces.
2. **Recipient Online Role (`onlineWrap` + Server Time-Lock Share `wrappedReleaseKeyB64`):**
   - Derived from the independent **Recipient Unlock Password** chosen by the owner.
   - Prevents premature decryption before countdown expiration (`T=0`) or authorized emergency counsel release (`?ert=`), while ensuring the server alone cannot decrypt any deposit without the recipient's passphrase.
3. **Air-Gapped Offline Role (`offlineAirgapWrap`):**
   - Embedded inside the standalone `.html` Offline Recovery Kit so recipients holding the downloaded recovery file and Recipient Unlock Password remain permanently independent of live servers (`file:///` recovery for `20+` years).
4. **Decoy Cover Role (`duressSecret` / Decoy Envelope):**
   - Independent ciphertext note wrapped under the **Emergency Duress Password**, completely decoupled from primary vault key material.

---

## 3. Zero-Oracle Coercion & Duress Shield Invariants

Under physical, border, or legal coercion, entering the **Emergency Duress Password** enforces strict side-channel parity:

- **HTTP & UI Parity:** Returns `HTTP 200` with structurally identical `HEARTBEAT_VERIFIED` confirmation and displays only the plausible Cover Note (including a matching decoy `.html` recovery export).
- **24-Hour Public Shield:** Silently places the primary vault under a `24-hour` public `423 Locked` protection shield against automated countdown disclosure while preserving internal vault integrity.
- **Canister Side-Channel Elimination (`v1.2.4`):** Public canister health and telemetry queries normalize timing/count semantics so external observers cannot distinguish active check-in vs. duress freeze states by inspecting public canister metrics.
- **Out-of-Band Counsel Trigger:** Dispatches an optional `HTTPS` webhook payload to pre-designated legal counsel containing an emergency recovery token (`?ert=`), authenticated with `X-ZeroCanary-Timestamp` and `X-ZeroCanary-Signature` (`HMAC-SHA-256`) under strict SSRF validation (`HTTPS`-only, private/loopback/CGNAT/cloud-metadata ranges rejected, redirects disabled).

---

## 4. Zero-LLM In-RAM Navigator Privacy Contract

ZeroCanary's quick navigator (`Ctrl/Cmd + K` or `/`) runs **without** any remote LLM inference, vector API calls, or query logging:

- The static index (`public/assets/zc-navigator-index.json`) is fetched once on first interaction into browser memory.
- Query tokenization, BM25 ranking across `EN`, `DE`, `ES`, `FR`, and `PL`, and 13 deterministic security/workflow intent rules execute locally in RAM.
- Query strings typed by users generate **zero** outbound `fetch`, `XHR`, or `sendBeacon` requests (`0` bytes transmitted per search).

---

## 5. Independent Mainnet Verification Parameters

Auditors can verify the live ICP Mainnet notary canister state independently against Internet Computer public consensus:

| Parameter | Verified Production Value |
| :--- | :--- |
| **Canister Principal** | `sctry-7qaaa-aaaam-qjsuq-cai` |
| **Master Governance Anchor** | `3339665` |
| **Live Wasm Module SHA-256** | `b6b1721e7a64e5f92c2f05b8697b71e9c552b48ebd6289e5aac994b15c1033e6` |
| **Threshold ECDSA Public Key (`secp256k1`)** | `036e0032b752069dee0dbc076a4c4705e336199880678d0602340e56f304f1f96d` |
| **Edge Runtime Version** | `v1.2.7-sovereign-social-mesh` |
| **Object Custody Jurisdiction** | European Union (`EU / eeur`) |

---

## 6. Air-Gapped `.html` Offline Recovery Kit Format

Every sealed deposit produces a self-contained `.html` file operating strictly under `file:///` with zero external CDN scripts:

- **Built-in 5-Language UI:** Localized recovery workflow (`EN`, `DE`, `ES`, `FR`, `PL`) with zero network calls required for deposits `<= 20 MB`.
- **Hybrid Large-Archive Support (`20–50 MB`):** Larger binary archives stream ciphertext exclusively after release authorization and decrypt locally inside browser RAM via WebCrypto `AES-256-GCM`.
- **Edge Hardening (`v1.2.5`):** External payment verification (`Stripe`, `USDC` EVM RPCs, `ICP` Rosetta) enforces pre-image order intents (`secretCommitmentSha256`), block timestamp freshness checks, atomic cross-isolate locks with stale-lock TTL recovery, `256 KB` webhook payload limits, and `10s` upstream fetch timeouts.

---

**Operator:** Gexiro Global Enterprises Ltd (Gibraltar) · [https://zerocanary.com](https://zerocanary.com) · [SECURITY.md](SECURITY.md)