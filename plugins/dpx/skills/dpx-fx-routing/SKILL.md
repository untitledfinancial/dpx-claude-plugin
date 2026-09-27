---
description: Use when choosing a settlement currency, comparing stablecoin routing options, or assessing FX corridor risk for a DPX payment.
---

# DPX FX & Stablecoin Routing

## Routing

- **`route`** (or **`stability.stablecoin_route`**) — ranks USDC, EURC, USDT (and others: BRLA, MXNC, NGNC, AEDX, PYUSD) for a given amount and currency pair. For EUR destinations, prefer EURC — it skips a cross-currency conversion the core fee would otherwise price in. Flags blocked routes (e.g. USDT under MiCA).

## FX intelligence

- **`fx.rate`** — live mid/bid/ask for any pair, sourced from central bank rates, no cost.
- **`fx.cost_certainty`** — the question a treasury user usually actually has: "if I send $X, what does the counterparty receive net of everything, and how certain is that over the next 48 hours?"
- **`fx.corridors`** — all 60+ corridors ranked OPTIMAL → ADVERSE, for comparing routes before committing to one.

## Rail health

Before a domestic settlement on a specific local rail, check **`oracle.rails`** for that region — PIX (Brazil), SEPA (Europe), FedACH (US), CHAPS (UK), UPI (India), PromptPay (Thailand). Don't settle against a rail reporting anything other than OPERATIONAL without flagging it.
