# DPX for Claude Code

Cross-border stablecoin settlement, AML/compliance screening, ESG scoring, and macro intelligence for AI agents — as a Claude Code plugin.

This plugin connects Claude to the live [DPX](https://untitledfinancial.com) MCP server (83 tools) and adds three Skills that teach Claude how to use them well: the settlement flow, compliance/ESG screening order of operations, and FX/stablecoin routing.

## Install

```
/plugin marketplace add untitledfinancial/dpx-claude-plugin
/plugin install dpx@dpx-tools
```

## What you get

- **MCP connection** to `mcp.untitledfinancial.com` — settlement, oracle, compliance, ESG, FX, Mercury banking, Ramp, and market intelligence tools. Full reference: [docs.untitledfinancial.com/integrations/mcp](https://docs.untitledfinancial.com/integrations/mcp)
- **`dpx-settlement`** — the settlement flow: oracle check → quote → compliance screen → execute, plus shortcuts (`flow_check`, `settlement.nl`, `batch_settle`)
- **`dpx-compliance`** — AML/sanctions/UBO/PEP screening and ESG scoring, in the right order relative to settlement
- **`dpx-fx-routing`** — stablecoin routing and FX corridor intelligence
- **`dpx-intelligence`** — macro, climate, commodity, systemic risk, and geopolitical intelligence tools; what to call for any forward-looking signal question, with free vs. paid guidance

## Free vs. paid tools

Most tools (oracle status, FX rates, fee schedules, market intelligence, compliance checks) work with no credential. A handful of paid tools require an API key — contact [case@untitledfinancial.com](mailto:case@untitledfinancial.com), then add it as a header on the `dpx` server in your `.mcp.json`:

```json
"headers": { "Authorization": "Bearer <your-key>" }
```

## Sandbox by default

`settlement.execute` defaults to sandbox mode — real oracle data and fee math, nothing moves on-chain. Live settlements require the user to explicitly ask for it.

## License

MIT
