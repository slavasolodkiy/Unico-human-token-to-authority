# Five sandbox experiments

These are **benign, consented validation tests**, not attack testing. Their purpose is to turn the five highest-value architectural unknowns into observations with the smallest possible number of calls.

## Ground rules

- Use only a Unico-provided sandbox or a production pilot explicitly authorised for biometric testing.
- Use consenting test subjects and the required biometric/privacy notices.
- Do not compare identifiers across independent companies unless Unico explicitly permits the test and the legal/contractual basis is clear.
- Where two tenants are involved, compare **HMACs of returned identifiers via a neutral test process**, not raw identifiers exchanged between controllers.
- Record request/response schema, timestamps, request IDs and environment; do not retain biometric images longer than necessary.

---

## X1 — Stability + channel semantics

**Question:** Is `personId` stable within one customer, and does it behave consistently across capture channels?

**Setup:** One tenant; same consenting person; repeated captures across different days/devices/lighting. Where supported, compare raw API, SDK and Web capture.

**Observe:**
- `personId` equality across captures;
- whether Web/SDK actually returns `personId` despite the current schema contradiction;
- whether the raw API result carries any evidence of liveness/presence.

**Resolves:** stability claim, Web/SDK contradiction, recognition-vs-presence boundary.

---

## X2 — Scope inside one tenant

**Question:** Is `personId` scoped by API key, product recipe, segment or branch?

**Setup:** Same tenant; two API keys / service accounts and, if available, two branches or `clientReferenceSegment`s.

**Observe:** same human → same or different `personId`.

**Interpretation:**
- difference across API keys/branches → a narrower namespace;
- equality → tenant-wide or broader, but not proof of global scope.

---

## X3 — Two-tenant scope test

**Question:** Is the RP-visible `personId` global or pairwise/scoped?

**Setup:** Two tenants under an explicitly permitted test arrangement.

**Observe:** same human under both tenants; compare neutral HMACs of the returned `personId` values.

**Interpretation:**
- equal → RP-visible global identifier;
- different → tenant-scoped identifier or per-tenant alias. A vendor answer is then needed to distinguish those two internal models.

**This is the highest-value experiment.**

---

## X4 — Human Token ↔ Multi Accounts interaction

**Question:** Do the two capabilities share underlying biometric state?

**Setup:** Same tenant. Run Human Token and Multi Accounts for the same consenting subject in both orders, using controlled `clientReference` values.

**Observe:**
- whether Human-Token-only capture affects a later Multi Accounts result;
- whether Multi Accounts enrolment changes Human Token resolution;
- whether any common identifiers/reference handles appear.

**Resolves:** shared graph vs shared matcher/separate namespace vs separate stores.

---

## X5 — Smart Revalidation + evidence forensics

**Question:** What is actually bound to an authentication decision, and what makes the evidence cryptographic?

**Setup:** One known reference identity. Run `LOGIN`, `FIN_TRANSACTIONS` and `CRITICAL_FIN_TRANSACTIONS` use cases on familiar and fresh devices, allowing silent and facial outcomes where the product routes them.

**Observe:**
- final result and `authenticationId`;
- whether a selfie exists (silent vs facial path);
- whether deciding tier / recipe / signals appear anywhere;
- Evidence Set contents.

**Offline Evidence Set checks:**
- PDF `/Sig` and `/ByteRange`;
- signer certificate chain;
- RFC 3161 timestamp / TSA;
- embedded hash manifest;
- metadata linking process, authentication event and transaction context.

**Resolves:** authentication-routing transparency and the concrete meaning of “cryptographic chain of custody”.
