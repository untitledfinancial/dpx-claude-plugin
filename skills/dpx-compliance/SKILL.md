---
description: Use before settling with a legal-entity counterparty, or when asked about AML, sanctions, PEP, UBO, or ESG risk for a payment or counterparty via DPX.
---

# DPX Compliance & ESG Screening

Run these before `settlement.execute`, not after — DPX's fee logic factors the ESG score into the settlement itself.

## AML / sanctions / beneficial ownership

- **`compliance.ubo_chain`** — traces beneficial ownership up to 3 levels and sanctions-screens each node. Required before any settlement where the counterparty is a legal entity, above the FATF travel-rule threshold.
- **`compliance.pep_screen`** — checks an individual against the politically-exposed-persons dataset. Returns `isPep`, risk level, and whether enhanced due diligence is triggered (FATF R.12/13).
- **`compliance.regulatory_calendar`** — check for a pending regulatory deadline (MiCA, SFDR, CSRD, GENIUS Act, FATF) affecting the corridor or counterparty type before proceeding.

## ESG

- **`esg.score`** — live E/S/G score for a wallet address or LEI, with SFDR PAI indicators. Feeds directly into the settlement fee (0–0.5%, live from the oracle).
- **`esg.lookup`** — resolve a company name/domain/ticker to a LEI via GLEIF and get the ESG score in one call — use this when you don't already have an LEI.
- **`esg.portfolio`** / **`esg.batch`** — score up to 200 / 50 entities at once for portfolio-level screening.

## Agent identity (KYA)

If the counterparty or the calling agent needs an identity tier: `agent.kya_register` (ANONYMOUS/REGISTERED/VERIFIED — VERIFIED via GLEIF LEI, no documents), `agent.mandate_create` for AP2-compatible spend mandates, `agent.kya_verify` for a signed credential to attach to settlement requests.
