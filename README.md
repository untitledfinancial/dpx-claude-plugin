# DPX for Claude Code

Cross-border stablecoin settlement, AML/compliance screening, ESG scoring, and macro intelligence for AI agents — as two independently installable Claude Code plugins, from one marketplace.

Both connect to the same live [DPX](https://untitledfinancial.com) MCP server. They're split because they're different products for different users — settlement/compliance is for anyone paying or screening a counterparty; intelligence is a standalone research tool DPX sells separately, with its own subscription tier. Install one, the other, or both.

## Install

```
/plugin marketplace add untitledfinancial/dpx-claude-plugin
/plugin install dpx@dpx-tools
/plugin install dpx-intelligence@dpx-tools
```

## `dpx` — settlement, compliance, FX routing

- **`dpx-settlement`** — the settlement flow: oracle check → quote → compliance screen → execute, plus shortcuts (`flow_check`, `settlement.nl`, `batch_settle`)
- **`dpx-compliance`** — AML/sanctions/UBO/PEP screening and ESG scoring, in the right order relative to settlement
- **`dpx-fx-routing`** — stablecoin routing and FX corridor intelligence

## `dpx-intelligence` — standalone research

- **`dpx-intelligence`** — macro, climate, commodity, systemic risk, and geopolitical intelligence tools; what to call for any forward-looking signal question, with free vs. paid guidance. Useful on its own, not only ahead of a settlement.

## Free vs. paid tools

Most tools (oracle status, FX rates, fee schedules, compliance checks) work with no credential. Paid tools — mostly in `dpx-intelligence` — take either a subscription key or a per-call x402 USDC payment; see that skill for which is which. Getting a subscription key is currently a manual request to [case@untitledfinancial.com](mailto:case@untitledfinancial.com) — self-serve key issuance via Stripe is in progress, not live yet.

## Sandbox by default

`settlement.execute` defaults to sandbox mode — real oracle data and fee math, nothing moves on-chain. Live settlements require the user to explicitly ask for it.

## License

MIT
