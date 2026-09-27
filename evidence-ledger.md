# Compact evidence ledger

All material claims below are grounded in public sources reviewed on 27 September 2026.

**Legend:** `OBSERVED` · `VENDOR CLAIM` · `INFERRED` · `UNKNOWN` · `CONTRADICTED`

| # | Claim | Status | Primary source |
|---|---|---|---|
| E1 | Human Token returns `idFace.personId` from a selfie; the Human Token page says identity is output, not input. | OBSERVED | [Human Token](https://developer.unico.io/capabilities/human-token) |
| E2 | Human Token page says omit `subject.code`; generic `/processes/v1` Onboarding reference marks identity fields required. | CONTRADICTED | [Human Token](https://developer.unico.io/capabilities/human-token) · [Create process](https://developer.unico.io/developers/api-reference/api/post-processes) |
| E3 | Unico describes `personId` as stable/opaque and tells the RP to store it with the user record. | OBSERVED as vendor contract claim; unverified empirically | [Human Token](https://developer.unico.io/capabilities/human-token) |
| E4 | Public docs do not state whether `personId` is global, tenant/API-key/branch scoped, or aliased. | UNKNOWN | Reviewed developer corpus |
| E5 | Raw-base64 API capture cannot itself invoke the documented liveness capability. | OBSERVED | [Liveness](https://developer.unico.io/capabilities/liveness) |
| E6 | Human Token marketing/blog language describes liveness-protected face tokenisation. | VENDOR CLAIM / tension with E5 on raw API path | [An internet with more humanity](https://www.unico.io/releases/an-internet-with-more-humanity) |
| E7 | Multi Accounts searches within an operator's base and a `clientReferenceSegment`; `clientReference` is RP supplied. | OBSERVED | [Multi Accounts](https://developer.unico.io/capabilities/multi-accounts) |
| E8 | Public docs do not document a direct `personId` ↔ Multi Accounts relationship. | UNKNOWN | Reviewed developer corpus |
| E9 | Unico documents cross-client document reuse. | OBSERVED | [Document reuse and capture](https://developer.unico.io/capabilities/document-reuse-and-capture) |
| E10 | Fraud Risk Classification refers to “global network history”. | OBSERVED | [Fraud Risk Classification](https://developer.unico.io/capabilities/fraud-risk-classification) |
| E11 | Unico-owned Trully exposes `unique_face_id_v2` and cross-company face counters in a separate Mexico surface. | OBSERVED | [KYC Magic Link](https://developer.unico.io/products/sign-up/kyc-magic-link/index) |
| E12 | `duiType = 3` is labelled “Internal Unico identifier”; an error string references `idnsv2/GetPublicID`. | OBSERVED clues; relation to `personId` UNKNOWN | [Create process](https://developer.unico.io/developers/api-reference/api/post-processes) · [Web create process](https://developer.unico.io/developers/api-reference/web-sdk/post-process) |
| E13 | Smart Revalidation uses `references[]` with prior process ID or Base64 image. | OBSERVED | [Web create process](https://developer.unico.io/developers/api-reference/web-sdk/post-process) |
| E14 | Smart Revalidation exposes `useCase`, `authenticationId`, final result and reference linkage. | OBSERVED | [Get process](https://developer.unico.io/developers/api-reference/web-sdk/get-process) |
| E15 | Smart Revalidation public material says only the final result is exposed; liveness/tier internals are not separately returned. | OBSERVED | [Smart Revalidation](https://developer.unico.io/products/step-up-authentication/smart-revalidation/index) |
| E16 | Marketing names a FIDO2/passkey tier; Android SDK 6.11.0 says passkey integration was removed. | CONTRADICTED / product-state unclear | [Smart Revalidation marketing](https://www.unico.io/product/continuous-authentication/smart-revalidation) · [Android release notes](https://developer.unico.io/developers/sdks-and-tools/android/resources/release-notes) |
| E17 | `useCase` has financial-transaction categories; general `contextualization` fields are described as user-facing context. | OBSERVED | [Smart Revalidation capability](https://developer.unico.io/capabilities/smart-revalidation) · [Web create process](https://developer.unico.io/developers/api-reference/web-sdk/post-process) |
| E18 | IDPay explicitly carries transaction identity/order/card/value fields and a separate evidence/chargeback flow. | OBSERVED | [Card-not-present verification](https://developer.unico.io/developers/regional-solutions/card-not-present-verification) |
| E19 | Finished Web/SDK processes can expose a watermarked selfie and Evidence Set PDF. | OBSERVED | [Get selfie](https://developer.unico.io/developers/api-reference/web-sdk/get-selfie) · [Get Evidence Set](https://developer.unico.io/developers/api-reference/web-sdk/get-evidence-set) |
| E20 | Reviewed public docs do not document a signed decision object, public JWKS, signed webhook, hash manifest or trusted timestamp for the decision/evidence bundle. | OBSERVED absence in reviewed docs | [Webhooks](https://developer.unico.io/developers/webhooks-and-events/setup) · [Get Evidence Set](https://developer.unico.io/developers/api-reference/web-sdk/get-evidence-set) |
| E21 | Unico marketing says Smart Re-Authentication creates a “cryptographic chain of custody”. | VENDOR CLAIM | [Launch release](https://www.unico.io/releases/neutralizing-genai-threats-unico-launches-smart-step-up-authentication-to-shield-platforms-against-deepfakes) |
| E22 | World ID 4.0 exposes scoped identifiers (nullifier; optional per-RP `session_id`) rather than being identifier-free. | OBSERVED | [World ID concepts](https://docs.world.org/world-id/concepts) · [4.0 migration](https://docs.world.org/world-id/4-0-migration) |
| E23 | World AgentKit / HITL are adjacent agent primitives, but the documented stack lacks a full mandate object with scope/budget/expiry/revocation. | OBSERVED + architectural inference | [AgentKit](https://docs.world.org/agents/agent-kit/integrate) · [Human in the loop](https://docs.world.org/agents/human-in-the-loop/integrate) |
