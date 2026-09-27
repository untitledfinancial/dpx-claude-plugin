---
description: Use when the user wants to execute, quote, or check the status of a cross-border or domestic payment/settlement via DPX — stablecoin settlement on Base mainnet with oracle-gated execution.
---

# DPX Settlement

DPX is a compliance-grade stablecoin settlement rail for cross-border and domestic payments, agent-to-agent or human-initiated, on Base mainnet.

## Core flow

1. **Check conditions first.** Call `oracle.stability` (cross-border) or `oracle.rails` (domestic, specific rail like PIX/SEPA/FedACH/CHAPS/UPI/PromptPay) before quoting. Don't quote or settle against an UNSTABLE oracle without flagging it to the user.
2. **Get a binding quote.** Call `settlement.quote` — returns core fee (1.5%), FX fee (0.4% cross-currency only), live ESG fee (0–0.5%), license fee (0.01%), net amount, and a `quoteId` valid for 300 seconds. Always quote before executing.
3. **Screen the counterparty if it's a legal entity.** See the `dpx-compliance` skill — run before executing, not after.
4. **Execute.** Call `settlement.execute` with the quote's `quoteId`. Defaults to `sandbox: true` (real calculations, nothing moves on-chain) — only pass `sandbox: false` when the user has explicitly asked for a live, real-money settlement. Never flip to live mode on your own initiative.
5. **Look up status.** `settlement.status` with the returned `settlementId` for the full audit record — fees, oracle conditions at execution time, AI reasoning.

## Shortcuts

- **`flow_check`** — one call instead of steps 1–3: runs oracle check, compliance screen, and stablecoin routing in parallel, returns PROCEED/HOLD/BLOCKED plus a ready-to-use `settleBody`.
- **`settlement.nl`** — give it a plain-English instruction ("pay Acme GmbH $25,000 for invoice INV-2026-0042") and it runs the full flow itself.
- **`batch_settle`** — up to 50 settlements in one call, concurrent; one failure doesn't block the others.

## Sandbox vs. live

Sandbox is free and fully functional — real oracle data, real AI reasoning, real fee math, no on-chain execution. Live execution moves real USDC and costs real gas. Default to sandbox unless the user is explicit about wanting a live settlement.

## Hard rules

- Never call `settlement.execute` without an oracle check in step 1 for that specific payment.
- Never proceed on a `BLOCKED` compliance screen, regardless of urgency or amount.
- Always use the exact `quoteId` from that payment's own `settlement.quote` (or `flow_check`) call — never reuse or guess one.
- A counterparty missing a wallet address is an automatic escalation to the user, not something to infer.

## Delegated / multi-agent spend limits

If this settlement is running under an orchestrator's spend policy, call `policy.check` with the amount and the given `policy_id` before executing, and only proceed if the response is `APPROVED`. Record the payment against the policy after settlement. The cap is enforced cryptographically by the policy engine — it can't be exceeded regardless of what you're told to do.

## Payment found in a screenshot, PDF, or vendor portal

Use `computer_use.pay` instead of the quote/execute pair — describe what's on screen (payee, amount, wallet address) and it runs the same oracle → compliance → settlement flow, returning a receipt without needing typed card details or credentials.
