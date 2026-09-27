# Unico Technical Truth Map v1

**Snapshot:** 27 September 2026  
**Scope:** Human Token · Multi Accounts · Smart Revalidation · transaction evidence · World ID 4.0 contrast

**Evidence rule:** `CONFIRMED` means directly supported by reviewed public docs/code/policy. It does **not** mean independently verified against a live production system.

---

## CONFIRMED

### C1 — Human Token is a face-resolution primitive
A documented Human Token call sends a selfie to `POST /processes/v1`; a successful response contains `idFace.personId` and `idFace.result = FOUND`. The Human Token page explicitly says the user does not declare an identifier: identity is the output of the call.

### C2 — `personId` is a durable RP-facing lookup key, but its scope is not documented
Unico describes it as stable and opaque and tells the relying party to store it alongside its own user record. Public docs do not say whether the same human gets the same value across tenants, API keys, branches or environments.

### C3 — Multi Accounts is a separate semantic primitive
Multi Accounts performs a segmented 1:N face search inside an operator's base. It uses the RP-supplied `clientReference` and a `clientReferenceSegment` configured by Unico in the API key. Public docs do not document a `personId` relationship.

### C4 — Unico has network-level / cross-client identity and fraud machinery in some products
Document reuse can cross client integrations; Fraud Risk Classification refers to “global network history”; Unico-owned Trully exposes `unique_face_id_v2` plus cross-company counters. These facts establish network-level capabilities somewhere in the stack. They do **not** establish that IDCloud `personId` is global across customers.

### C5 — Smart Revalidation uses a reference process/image, not `personId`
The documented reference is a prior process ID or an image (`REFERENCE_TYPE_PROCESS_ID` / `REFERENCE_TYPE_IMAGE_BASE64`). `authenticationId`, `useCase`, silent/device context and a final Smart Revalidation result are separate objects/concepts.

### C6 — The deciding authentication method is not exposed in the documented final result
Public Smart Revalidation material describes metadata/silent/facial tiers, while marketing also names a passkey tier. The public result exposes the final verdict but not the tier that decided, the signals that fired, or the recipe/model version.

### C7 — General Smart Revalidation does not publicly establish cryptographic binding to a concrete transaction
`useCase` is a category. General `contextualization` fields are documented as context shown to the user. IDPay is the clear documented exception: it binds identity to an order, value and card context and has its own evidence/chargeback workflow.

### C8 — Evidence exists, but no public RP-verifiable signed decision receipt was found
Public interfaces expose process records, a watermarked selfie and an Evidence Set PDF. Reviewed docs do not document a JWS/COSE decision object, public JWKS, signed webhook, PDF signature profile, hash manifest or trusted timestamp that lets a third party verify the decision independently of Unico.

### C9 — World ID 4.0 is not identifier-free
World returns scoped identifiers: a nullifier associated with user/RP/action semantics and, for session proofs, a stable per-RP `session_id`. The architectural difference is **scoping and unlinkability design**, not “identifier vs no identifier”.

### C10 — Neither Unico nor World documents a complete AI-agent mandate primitive
Neither public stack provides the full chain: principal → delegated agent → machine-readable scope/budget/time window → revocation → transaction → durable authority evidence. World has adjacent AgentKit / human-in-the-loop primitives; Unico publicly names the agent-human problem but does not expose a mandate API.

---

## LIKELY — useful hypotheses, not facts

### L1 — Best-fit `personId` model: global internal identity + customer-facing scoped alias
This model best reconciles Unico's network-level identity/fraud capabilities with tenant isolation and jurisdiction-specific controller/processor boundaries. It remains inference until a two-tenant test or Unico's answer resolves it.

### L2 — Human Token and Multi Accounts probably share at least part of the same biometric/matching infrastructure
They solve different product questions and may have different namespaces or indexes. “Shared infrastructure” must not be simplified into “same database”.

### L3 — Human Token should be treated as recognition; liveness/presence is a separate assurance property
Unico documents that liveness cannot be invoked through a raw-base64 API image alone, while Human Token accepts raw Base64. Therefore the safest public interpretation is: `personId` identifies/resolves a face; proof that a live person was present depends on the capture path.

### L4 — Unico's product progression is moving from identity to contextual authentication to transaction assurance
Human Token → Smart Revalidation → IDPay is a coherent progression. The next architectural layer is authority: *was this actor permitted to perform this exact action?*

### L5 — “Cryptographic chain of custody” may have an internal implementation not described publicly
The correct conclusion is not “it does not exist”, but “the reviewed public material does not expose the independently verifiable artifact behind the phrase”.

---

## UNKNOWN — highest-value questions

### U1 — What is the exact scope of `personId`?
Global across Unico, tenant-scoped, API-key/segment-scoped, branch-scoped, or a tenant alias of a global identity?

### U2 — What is the storage/namespace relationship among Human Token, Multi Accounts and network-history signals?
Shared identity graph, shared matcher with separate namespaces, or separate stores?

### U3 — What side effect does first-time Human Token recognition create?
Does the first capture enrol a network identity, tenant identity, product-local record, or something else?

### U4 — What integrity mechanism exists inside a real Evidence Set?
Does the PDF contain an embedded signature, timestamp or manifest that is simply absent from the API reference?

### U5 — What is the lifecycle after deletion, false merge, account closure or re-enrolment?
What happens to the face vector/template, `personId` mapping, Multi Accounts state, network history and downstream relying parties?

---

## WRONG — claims we should not repeat

- **WRONG:** “`personId` is proven global across every Unico customer.”
- **WRONG:** “Multi Accounts is the Human Token identity database.”
- **WRONG:** “Every Human Token result proves a live human was present at capture time.”
- **WRONG:** “General Smart Revalidation cryptographically binds exact transaction parameters.”
- **WRONG:** “The Evidence Set is publicly documented as a signed cryptographic receipt.”
- **WRONG:** “World gives a proof but no identifier.”
- **WRONG:** “World cross-RP correlation is mathematically impossible without qualifications.”
- **WRONG:** “`personId` is a mandate” or “`clientReference` is a delegated agent.”

---

# Five questions for Gui

1. **`personId` scope** — For the same human, would two different Unico customers receive the same `personId`, pairwise identifiers, or does Unico maintain a global identity internally and expose customer-specific aliases?
2. **One graph or several?** — Are Human Token, Multi Accounts and the network-history fraud signals ultimately resolving against the same underlying biometric identity graph, or are those deliberately separate namespaces/stores?
3. **Recognition vs presence** — Since raw Base64 Human Token calls cannot invoke SDK liveness, should `personId` fundamentally be understood as recognition of the face, while proof of live presence is a separate property of the capture path?
4. **Transaction evidence** — What exactly is the technical artifact behind “cryptographic chain of custody” in Smart Re-Authentication? Can an RP later verify a signed object binding authentication event + transaction parameters + time + policy/version, or is that provenance currently maintained inside Unico?
5. **The next layer** — You already solve “who is this human?” and increasingly “is this the same human acting now?”. How are you thinking about proving that this human — or an AI agent acting for them — had authority for this exact action under a specific mandate?
