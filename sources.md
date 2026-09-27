# Sources and evidence discipline

**Snapshot date:** 27 September 2026.

This repository is a public-source architecture notebook, not a security audit. Statements in the truth map are intentionally narrower than the underlying research corpus.

## Unico — primary sources

### Human Token / identity
- [Human Token](https://developer.unico.io/capabilities/human-token)
- [Create process — API contract](https://developer.unico.io/developers/api-reference/api/post-processes)
- [Get process — API contract](https://developer.unico.io/developers/api-reference/api/get-process)
- [Liveness](https://developer.unico.io/capabilities/liveness)
- [Document reuse and capture](https://developer.unico.io/capabilities/document-reuse-and-capture)
- [Fraud Risk Classification](https://developer.unico.io/capabilities/fraud-risk-classification)
- [Multi Accounts](https://developer.unico.io/capabilities/multi-accounts)
- [KYC Magic Link / Trully](https://developer.unico.io/products/sign-up/kyc-magic-link/index)

### Smart Revalidation / evidence
- [Smart Revalidation capability](https://developer.unico.io/capabilities/smart-revalidation)
- [Smart Revalidation product](https://developer.unico.io/products/step-up-authentication/smart-revalidation/index)
- [Create process — Web & SDK](https://developer.unico.io/developers/api-reference/web-sdk/post-process)
- [Get process — Web & SDK](https://developer.unico.io/developers/api-reference/web-sdk/get-process)
- [Get selfie](https://developer.unico.io/developers/api-reference/web-sdk/get-selfie)
- [Get Evidence Set](https://developer.unico.io/developers/api-reference/web-sdk/get-evidence-set)
- [Webhook setup/security](https://developer.unico.io/developers/webhooks-and-events/setup)
- [Android SDK release notes](https://developer.unico.io/developers/sdks-and-tools/android/resources/release-notes)
- [Card-not-present verification / IDPay](https://developer.unico.io/developers/regional-solutions/card-not-present-verification)

### Unico statements / privacy
- [Smart Re-Authentication launch release](https://www.unico.io/releases/neutralizing-genai-threats-unico-launches-smart-step-up-authentication-to-shield-platforms-against-deepfakes)
- [An internet with more humanity](https://www.unico.io/releases/an-internet-with-more-humanity)
- [Smart Revalidation marketing](https://www.unico.io/product/continuous-authentication/smart-revalidation)
- [Unico privacy centre](https://devcenter.unico.io/privacy/)

## World ID — architectural contrast only
- [World ID concepts](https://docs.world.org/world-id/concepts)
- [World ID 4.0 migration](https://docs.world.org/world-id/4-0-migration)
- [IDKit integration](https://docs.world.org/world-id/idkit/integrate)
- [World ID credentials](https://docs.world.org/world-id/idkit/credentials)
- [World ID 4.0 technical specification](https://github.com/worldcoin/world-id-protocol/blob/main/docs/world-id-4-specs/README.md)
- [AgentKit](https://docs.world.org/agents/agent-kit/integrate)
- [Human in the loop](https://docs.world.org/agents/human-in-the-loop/integrate)

## Status labels

- **CONFIRMED / OBSERVED** — directly supported by reviewed public docs/code/policy.
- **VENDOR CLAIM** — marketing or policy language whose technical mechanism is not exposed in the reviewed interface material.
- **LIKELY / INFERRED** — our architectural interpretation of observed facts.
- **UNKNOWN** — public evidence does not distinguish the competing models.
- **CONTRADICTED** — two official surfaces disagree or describe materially different behavior.
- **WRONG** — an interpretation that the accumulated evidence does not support and should not be repeated.

## Important limitation

“Not found in reviewed public documentation” is not equivalent to “does not exist”. The five sandbox experiments exist specifically to turn the highest-value unknowns into observations.
