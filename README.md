# From Human Token to Authority
### What Unico's public interfaces reveal about identity, authentication and transaction evidence

**Public-source technical notebook · 27 September 2026**  
**Author:** Slava Solodkiy · [solodkiy.cv](https://www.solodkiy.cv/unico.html)  
**Scope:** Unico Human Token, Multi Accounts, Smart Re-Authentication / Smart Revalidation, transaction evidence, and a small architectural contrast with World ID 4.0.

> **Knowing who the human is is not the same as knowing what they authorised.**

This repository is intentionally small. It is not an audit of Unico and not a product ranking. It records what current public material establishes, what it only suggests, what remains unknown, and the five smallest sandbox experiments that would turn the highest-value unknowns into observations.

No live Unico system was probed. No credentials were used. No authentication was bypassed. `UNKNOWN` means the reviewed public evidence does not distinguish the competing architectural models.

## The architecture in one view

```text
HUMAN
  │
  ▼
IDENTITY                     Human Token
Who is this recurring human?  face → personId
  │
  ▼
AUTHENTICATION               Smart Revalidation
Is the expected human         reference + context → decision
acting now?
  │
  ├────────────── missing layer ──────────────┐
  ▼                                           ▼
AUTHORITY / MANDATE                          DELEGATE / AGENT
Who may act? Under what                      human or software
scope, budget, time window                   acting for a principal
and revocation state?                         │
  └───────────────────────────────────────────┘
                      │
                      ▼
TRANSACTION
What exact economic action was approved?
                      │
                      ▼
EVIDENCE
Can a third party verify the whole chain later?
```

The interesting boundary is between **authentication** and **authority**. Publicly documented Unico capabilities are already strong on recognition and adaptive re-authentication; the next unresolved problem is proving permission for a specific action, especially when an AI agent acts for a human or organisation.

## Five things that matter most

1. **Human Token is a recognition primitive.** A selfie resolves to an opaque `personId`; the user does not first declare an identity in the Human Token flow.
2. **The scope of `personId` is still public-knowledge UNKNOWN.** It may be global, tenant-scoped, API-key-scoped, or a tenant alias of a global internal identity.
3. **Multi Accounts is semantically different.** It is an operator/segment-scoped 1:N duplicate check keyed by `clientReference`; public docs do not state that it shares a namespace with `personId`.
4. **Smart Revalidation is about transaction-time authentication, not authority.** It uses a reference process or image plus `useCase` and context; the deciding tier is not exposed in the documented result.
5. **Public docs do not show a third-party-verifiable signed decision receipt.** Unico exposes process records, selfies and evidence PDFs; the phrase “cryptographic chain of custody” is a vendor claim whose concrete externally verifiable artifact is not documented publicly.

## Repository map

| File | Purpose |
|---|---|
| [`technical-truth-map.md`](technical-truth-map.md) | Canonical `CONFIRMED / LIKELY / UNKNOWN / WRONG` map + five questions for Gui |
| [`evidence-ledger.md`](evidence-ledger.md) | Compact evidence ledger with primary-source links |
| [`experiments.md`](experiments.md) | Five sandbox tests, ordered by information gain |
| [`sources.md`](sources.md) | Source list and evidence discipline |
| [Visual notebook](https://slavasolodkiy.github.io/Unico-human-token-to-authority/) | GitHub Pages version |

## Selected related work

Only the closest context — not a full portfolio.

| Work | Why it is relevant here |
|---|---|
| [Digital Identity](https://www.solodkiy.cv/digital-identity.html) | 82-company landscape, reusable identity, proof-of-personhood and prior World ID research |
| [Compliance & AML](https://www.solodkiy.cv/compliance.html) | KYC/KYB/KYCC, EDD and the regulated evidence context behind identity decisions |
| [Provisional Authority & Deferred Controls](https://www.solodkiy.cv/Provisional-Authority.html) | Caps, TTL, revocation and hash-chained evidence — adjacent to the mandate layer proposed here |
| [Sovereign Decision Plane](https://www.solodkiy.cv/Sovereign-Decision-Plane.html) | Separating model inference from deterministic/formal authority controls |
| [Local AI lab](https://www.solodkiy.cv/tech.html) | Hands-on local inference, evals and formal-method experiments |
| [Regulated fintech & banking](https://www.solodkiy.cv/fintech.html) | Product and compliance-first banking context where identity becomes consequential |

## A possible next layer — an Authority Receipt

This is an **original design sketch**, not a claim about Unico or World ID.

A regulated relying party eventually needs a portable object that links identity evidence, a concrete authentication event, a mandate and the exact transaction that was authorised.

```json
{
  "principalRef": "pairwise:...",
  "identityEvidenceRef": "idp-process:...",
  "authenticationEventRef": "auth:...",
  "mandateRef": "mandate:...",
  "transactionDigest": "sha256:...",
  "decision": "ALLOW",
  "policyVersion": "policy:...",
  "occurredAt": "2026-09-27T16:00:00Z",
  "evidenceDigest": "sha256:...",
  "issuerSignature": "..."
}
```

The important design choice is that `principalRef` should ideally be **pairwise / RP-scoped**, not a global biometric join key. The receipt should prove *authority for an action*, not create a new surveillance identifier.

## Reading order

1. Open the [visual notebook](https://slavasolodkiy.github.io/Unico-human-token-to-authority/) — ~90 seconds.
2. Read [`technical-truth-map.md`](technical-truth-map.md) — the canonical v1.
3. Use [`experiments.md`](experiments.md) only when sandbox access exists.

## Versioning

- **v1.0 — Public evidence edition:** current repository.
- **v1.1 / v2.0 — Sandbox validated edition:** after the five experiments in `experiments.md`.

That distinction is deliberate: the open questions are part of the result, not unfinished work.
