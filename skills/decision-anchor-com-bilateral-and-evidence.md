---
name: decision-anchor-com-bilateral-and-evidence
description: Fix a shared responsibility boundary between two agents with a bilateral Decision Declaration, and later produce an external-audience evidence report or anomaly comparison for a decision — the dispute-side flows, with their payment and data-availability rules.
api: openapi/decision-anchor-com-openapi.yml
operations:
  - "POST /v1/dd/bilateral/propose (no operationId in the provider's spec)"
  - "GET /v1/dd/bilateral/received (no operationId)"
  - "GET /v1/dd/bilateral/sent (no operationId)"
  - "POST /v1/dd/bilateral/{agreement_id}/respond (no operationId)"
  - "GET /v1/ara/evidence-report (no operationId)"
  - "GET /v1/ara/anomaly-compare (no operationId)"
  - "GET /v1/dd/{dd_id}/lineage (no operationId)"
method: generated
generated: '2026-09-19'
grounding: >-
  Every route above exists verbatim in openapi/decision-anchor-com-openapi.yml (no operationIds are declared).
  Prices, sample requirements, windows and error codes are quoted from the contract, from
  /.well-known/x402.json and from the provider's AGENTS.md. Nothing here was invented.
mcp_equivalent: [propose_bilateral, get_evidence_report, compare_anomaly]
---

# Bilateral declarations and evidence reports

Base URL `https://api.decision-anchor.com`; `Authorization: Bearer <auth_token>` on every call (see the
anchor-a-decision skill for registration). Both agents in a bilateral flow need their own registration.

## A. Fix a boundary between two agents (delegation, handoff, agreement)

**Why:** "Agent A delegated a task to Agent B. The result was wrong. Who is responsible?" A bilateral DD
fixes the responsibility boundary at the point of delegation, outside both platforms (AGENTS.md).

1. **Proposer:** `POST /v1/dd/bilateral/propose` with `counterparty_agent_id`, a fresh `request_id`
   (idempotency key, scoped to you), the `dd` block (`dd_declaration_mode` is set by the path — do not send
   `self_declared` here) and the `ee` axes. This route is **not Trial-eligible**: it answers `402` with an x402
   v2 challenge (`$0.01` base per `/.well-known/x402.json`); sign and retry with `Payment-Signature`.
2. **Counterparty:** discover proposals with `GET /v1/dd/bilateral/received`; the proposer tracks
   `GET /v1/dd/bilateral/sent`.
3. **Counterparty:** `POST /v1/dd/bilateral/{agreement_id}/respond` with `{"accept": true}` or
   `{"accept": false}`. Rejection is the only reversal path; no proposal expiry and no proposer-side withdraw
   are documented.
4. On acceptance each side's declaration is recorded externally; confirm as usual with `POST /v1/dd/confirm`.
   Lineage across related records is readable at `GET /v1/dd/{dd_id}/lineage` (`parent_dd_id` links them).

Until 2026-08-25 the MCP `propose_bilateral` tool rejected every call (provider changelog); prefer the REST
route if an older client misbehaves.

## B. Produce evidence for one decision

`GET /v1/ara/evidence-report?dd_id=<uuid>` — "an external-audience evidence report for a decision,
structured for external audit review. Works from a single decision." **10 DAC, external USDC via x402 only**
— the Trial never covers ARA, and Earned DAC is not accepted on this route. Decision Anchor "does not
interpret, evaluate, or compare"; the report is factual metadata (timestamp, EE resolution, cost, settlement).

## C. Compare a decision against your own pattern

`GET /v1/ara/anomaly-compare?dd_id=<uuid>[&period_days=90]` — 5 DAC via x402. Returns `band_position`
(`within_band` / `outlier`) per dimension, statistical vocabulary only.

Precondition the contract states: **at least 2 decisions with attached decision metadata** (branch 1,
`content_inclusion_flag: 1`) in the window. Content-blind branch-0 decisions do not count. Until the sample
is met the call returns **`404 DATA_UNAVAILABLE` and no payment is requested** — data availability is
checked before any 402 is issued, so you are never charged for an empty observation.

## Payment rules for this skill

- Challenge arrives as HTTP `402`, header `PAYMENT-REQUIRED` (base64 x402 v2; body is a copy).
- Retry the identical request with `Payment-Signature`. `X-PAYMENT` (v1) is treated as unpaid.
- Identity is checked behind the payment gate: a signed retry without a valid bearer token still ends in
  `401` (provider changelog 2026-08-21). Send both.
- Your owner's DAB cap can reject external spending; read `GET /v1/dab/status`. A subordinate agent cannot
  raise it.
