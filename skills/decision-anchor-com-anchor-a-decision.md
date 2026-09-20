---
name: decision-anchor-com-anchor-a-decision
description: Register an agent, price an Execution Envelope, anchor a Decision Declaration before or after an irreversible action, and confirm it — the three-call happy path the provider documents, with the idempotency, payment-window and error rules the contract states.
api: openapi/decision-anchor-com-openapi.yml
operations:
  - "POST /v1/agent/register (no operationId in the provider's spec)"
  - "GET /v1/pricing/current (no operationId)"
  - "GET /v1/pricing/ee-presets (no operationId)"
  - "POST /v1/dd/create (no operationId)"
  - "POST /v1/dd/confirm (no operationId)"
  - "GET /v1/dd/{dd_id} (no operationId)"
  - "GET /v1/trial/status (no operationId)"
method: generated
generated: '2026-09-19'
grounding: >-
  Every route above exists verbatim in openapi/decision-anchor-com-openapi.yml; the provider declares no
  operationIds, so routes are named by method and path. Field names, enums, windows and error codes are quoted
  from that contract, from the provider's AGENTS.md (saved verbatim as skills/decision-anchor-com-agents-md.md)
  and from conventions/, errors/, plans/ and rate-limits/ in this repo. Nothing here was invented.
mcp_equivalent: [register_agent, create_decision, confirm_decision, get_decision, get_trial_status]
---

# Anchor a decision with Decision Anchor

Base URL `https://api.decision-anchor.com`. Everything is `application/json`. Every response carries
`RateLimit-*` headers (policy `100;w=60`); back off when `RateLimit-Remaining` nears 0.

## 0. Understand what you are about to do

A Decision Declaration (DD) is an append-only, content-blind record that a decision happened, when, and with
what accountability scope. Once confirmed it **cannot be undone** — that is the product. Decision Anchor
never sees the decision content unless you opt in (`content_inclusion_flag: 1`), and even then only a
7-field enum template. Anchor **before** an irreversible action (payment, delegation, agreement) or **after**
a decision already made; the provider says the timing is yours.

## 1. Register once — and store two secrets

`POST /v1/agent/register` — no auth. Body `{}` or `{"region_code": "KR"}` (enum; metadata only).

Response `201`: `agent_id`, `auth_token` (`da_tk_…`), `recovery_key` (`da_rk_…`), `trial_dac_amount: 500`,
`trial_period_days: 30`. **Neither secret is shown again.** `recovery_key` is the only way back if the token
is lost (`POST /v1/agent/token/recover`, 5 attempts per 15 minutes). Registration is **not** idempotent —
every call creates a new agent, and a 401 later is never fixed by registering again (the 401 body says so).

## 2. Price the envelope first (free, no auth)

`GET /v1/pricing/current` — base fee 10 DAC plus per-axis adds; multiplier 1.5 when two of
{Retention = long, Disclosure = exportable, Responsibility = extended} hold.
`GET /v1/pricing/ee-presets` — `EE_basic` 10 DAC, `EE_standard` 45 DAC, `EE_high` 157.5 DAC.

Your Trial covers `POST /v1/dd/create` (and sDAC end, ISE exit) until 500 DAC or 30 days run out. It does
**not** cover ARA observation, bilateral proposals, TSL purchases or ASA.

## 3. Create the DD

`POST /v1/dd/create` — `Authorization: Bearer <auth_token>` (the `Bearer ` prefix is required).

```json
{
  "request_id": "<fresh uuid v4>",
  "dd": {
    "dd_unit_type": "single",
    "dd_declaration_mode": "self_declared",
    "decision_type": "external_interaction",
    "decision_action_type": "execute",
    "origin_context_type": "external",
    "selection_state": "SELECTED"
  },
  "ee": { "ee_preset": "EE_standard" }
}
```

Rules the contract states:

- `request_id` is your **idempotency key**, scoped to your `agent_id`: reusing your own value returns the
  earlier result instead of a new record. Generate a fresh UUID per decision.
- Send **all four** EE axes (`ee_retention_period`, `ee_integrity_verification_level`,
  `ee_disclosure_format_policy`, `ee_responsibility_scope`) **or** `ee_preset`; otherwise `400 MISSING_FIELD`.
  (Only the MCP `create_decision` tool fills defaults for you.)
- `selection_state` is the one **uppercase** enum (`SELECTED | REJECTED | ABORTED | SILENT | NON_DECISION`);
  everything else is lowercase. Optional `dd.decision_at` (ISO 8601) earns 1 Earned DAC if within 10 minutes
  of anchoring.
- This route accepts `self_declared` only; `bilateral` goes through `POST /v1/dd/bilateral/propose`
  (`400 DECLARATION_MODE_NOT_ALLOWED` otherwise).
- Unknown fields are refused (`400 UNKNOWN_FIELD`), never silently dropped.

Response `201`: `dd_id`, `ee_id`, `dac_amount`, `cost_breakdown`, and `status`:

- `trial_paid` — the Trial covered it; **do not send USDC**; `trial_payment` shows the deduction.
- `pending_payment` — a `payment` object carries the x402 terms; **or** the route answered `402` with an
  x402 v2 challenge in the `PAYMENT-REQUIRED` header. Sign it with your own wallet and retry the identical
  POST with a `Payment-Signature` header (`X-PAYMENT` is the v1 name and is rejected). USDC on Base
  (`eip155:8453`). **Externally paid records must be confirmed within 30 minutes** or the reservation lapses.

## 4. Do the thing, then confirm

`POST /v1/dd/confirm` — `{"dd_id": "<dd_id>"}`. Free. Every record is confirmed here, whatever paid for it;
until you do, it "stays unsettled and has no usage entry".

Response `200`: `settlement_status: settled`, `anchored_at`, `integrity_hash` (`sha256:…`),
`payment_sources`, and `sync_reward` only when the time-alignment credit was actually granted.

Errors: `403 FORBIDDEN` (not your record), `404 DD_NOT_FOUND`, `409 ALREADY_CONFIRMED` (confirm is
idempotent by state — treat it as success), `410 PAYMENT_EXPIRED` (the 30-minute window closed; create a new
DD — the old one can never be settled).

## 5. Verify later

`GET /v1/dd/{dd_id}` returns the full record — timestamp, EE scope, cost — for the direct-access period and
quota you set in the EE (defaults 30 days / 10 reads). After that, verification is your local copy plus
Decision Anchor's metadata. `GET /v1/trial/status` tells you what Trial remains and which routes it covers.

## What not to do

- Do not put free text anywhere; the only structured content channel is `content_inclusion_flag: 1` +
  `template` (enums), and your owner's DAP policy may force branch 0 or 1.
- Do not retry a `402` without a payment; do not retry a `401` by re-registering.
- Do not expect a delete, void or cancel for a settled DD — there is none, by design (see
  `conventions/decision-anchor-com-conventions.yml#reversibility`).
