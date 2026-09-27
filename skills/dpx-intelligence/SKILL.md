---
description: Use when the user asks about macro conditions, FX risk, commodity markets, climate stress, systemic risk, supply chain, shipping, or any forward-looking intelligence signal — before a settlement decision, for research, or as a standalone question.
---

# DPX Intelligence

DPX provides live institutional-grade intelligence across macro, climate, commodity, systemic risk, and geopolitical domains. These tools are useful on their own — not only as part of a settlement flow.

**Access:** most tools require an API key (`X-API-Key: dpx_sub_pk_...`) or a per-call x402 USDC payment on Base. Call `intelligence.subscribe` to see subscription tiers, or ask the user if they have a key before calling a paid tool. Free tools are marked below.

---

## What to call for common questions

| User asks about | Tool |
|---|---|
| Is now a good time to settle / send money? | `oracle.stability` (free) |
| Is a specific corridor (e.g. USD→BRL) safe right now? | `stability.corridor` |
| Best time window to settle a large payment? | `stability.settlement_window` |
| Which stablecoin to use for a given currency pair? | `stability.stablecoin_route` (free) |
| Current macro stress — inflation, yields, credit | `oracle.status` (free) |
| A specific local rail (PIX, SEPA, FedACH, UPI…) | `oracle.rails` (free) |
| Commodity prices / climate outlook (WHEAT, WTI, etc.) | `forecast.commodity_outlook` |
| Which commodity regions are stressed? | `forecast.production_regions` |
| What-if scenario on a commodity portfolio | `forecast.scenario` |
| FX corridor risk — which pairs are safe to settle? | `market.fx` |
| All-in cost of an FX payment, including slippage | `fx.cost_certainty` |
| Live FX rate for any pair | `fx.rate` (free) |
| Shipping / freight / trade route stress | `market.shipping` |
| How a shock cascades through interconnected systems | `market.cascade` |
| Slow-moving structural fault lines (demographic, fiscal, geopolitical) | `intelligence.tectonic` |
| Secondary waves after a primary shock | `intelligence.aftershock` |
| Is a macro shock self-limiting or expanding? | `intelligence.contagion` |
| Are multiple macro forces amplifying each other? | `intelligence.resonance` |
| Gender risk / female LFPR → sovereign risk signal | `intelligence.gender_risk` |
| Network-level crisis formation before market data | `oracle.mycelium` |
| Governance score for a legal entity (LEI) | `oracle.governance` |

---

## Free tools — no key required

- `oracle.stability` — global settlement safety verdict (STABLE/CAUTION/UNSTABLE), score 0–100
- `oracle.status` — all 11 signal layers with AI briefing
- `oracle.rails` — live health of PIX, SEPA, FedACH, CHAPS, UPI, PromptPay
- `stability.stablecoin_route` — optimal stablecoin for a currency pair, with regulatory flags
- `fx.rate` — live mid/bid/ask, 160+ currency pairs

---

## Paid tools — API key or x402

All paid tools accept either a subscription key (`X-API-Key: dpx_sub_pk_...` header) or a per-call x402 USDC payment. If the user doesn't have a key, tell them they can get one at `https://agent.untitledfinancial.com/pay` — or suggest the sandbox via `oracle.stability` first to demonstrate value before they subscribe.

**Macro & systemic:**
- `oracle.status` — full 11-layer oracle output with AI briefing
- `stability.corridor` — corridor-specific settlement risk for a currency pair
- `stability.settlement_window` — optimal 4-hour execution windows over 72h for large payments
- `market.cascade` — shock propagation through 24 nodes across climate, geopolitical, economic, commodity
- `intelligence.tectonic` — 22 structural fault lines with years-to-rupture estimates
- `intelligence.aftershock` — three secondary waves after a primary shock (0–72h, 1–4 weeks, 1–6 months)
- `intelligence.contagion` — epidemiological spread model, R-value trajectory, superspreader nodes
- `intelligence.resonance` — detects phase-aligned macro forces amplifying each other
- `oracle.mycelium` — network topology crisis detection, 6–14 weeks ahead of market data
- `intelligence.gender_risk` — GBV → LFPR suppression → GDP drag → sovereign risk signal

**Commodity & climate:**
- `forecast.commodity_outlook` — BULLISH/BEARISH/NEUTRAL with 30/60/90d horizons for WHEAT, CORN, SOYB, COFFEE, COCOA, COTTON, SUGAR, WTI, NG, COPPER, LUMBER
- `forecast.portfolio_stress` — aggregate climate score for a multi-commodity portfolio
- `forecast.scenario` — what-if: la_nina_severe, gulf_hurricane_major, us_plains_drought_severe, and more
- `forecast.production_regions` — 40 global production regions ranked by current climate risk
- `forecast.calendar` — seasonal risk windows (hurricane season, corn pollination, Brazil frost, etc.)

**FX & markets:**
- `market.fx` — per-pair execution risk for 10 corridors, SETTLE_NOW / AVOID recommendations
- `fx.cost_certainty` — all-in CFO quote: net received, 48h cost variance, best execution window
- `fx.corridors` — full 60+ corridor risk matrix with liquidity, volatility, regulatory flags
- `market.shipping` — freight stress mapped to payment corridor risk
- `oracle.governance` — governance score for any LEI (GLEIF + World Bank WGI)

**Reports ($2–$10 USDC each) — one-shot formatted output:**
- `reports.climate` — climate physical risk report for a commodity portfolio
- `reports.macro` — macro conditions briefing: yields, FX, commodities, geopolitical
- `reports.esg` — ESG summary for a legal entity or portfolio
- `reports.compliance` — AML/sanctions/PEP findings for a counterparty
- `reports.treasury` — cross-border payment corridor analysis for a treasury team

**Webhooks & subscriptions:**
- `intelligence.subscribe` — register a URL to receive alerts when a signal crosses a threshold (stability, cascade, macro_stress, climate, fx)
- `intelligence.subscription.get` / `.delete` — manage subscriptions

---

## Sequencing guidance

**Before a settlement:** always run `oracle.stability` first (free). If CAUTION or UNSTABLE, run `stability.corridor` for the specific pair and `stability.settlement_window` to find a safer execution time before quoting.

**For a macro question:** start with `oracle.status` (free, gives full picture). If the user wants to understand propagation or systemic risk, follow with `market.cascade` → `intelligence.aftershock` or `intelligence.resonance`.

**For a commodity question:** `forecast.commodity_outlook` for a single symbol, `forecast.portfolio_stress` for a multi-position view, `forecast.scenario` for stress-testing a thesis.

**For a report:** use `reports.*` tools when the user wants a formatted, shareable document rather than raw data — treasury teams, compliance teams, ESG disclosures.

---

## If the user doesn't have an API key

Suggest the free tools first (`oracle.stability`, `oracle.status`, `fx.rate`) to demonstrate value. For paid tools, point them to: `GET https://agent.untitledfinancial.com/pay` — which returns subscription tiers and the payment flow. Do not block on this — run the free tools and flag the paid ones as requiring a key.
