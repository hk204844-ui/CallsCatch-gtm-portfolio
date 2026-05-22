# CallsCatch — Automation (n8n)

**End-to-end GTM automation** for [CallsCatch](https://callscatch.com) — 24/7 AI phone reception for Australian service businesses — built with **n8n Cloud**, **OpenAI**, **Retell AI**, and **Google Sheets** as a lightweight CRM.

> **Public portfolio repository** — sanitized workflow exports, prompts, and setup guides. Live credentials, sheet IDs, and customer data stay in a **private** automation repo.

## Product context

| | |
|---|---|
| **Product** | AI answering, lead qualification, SMS summaries, ~48h setup |
| **Audience** | Trades, health, professional services, hospitality, high-value services |
| **Role** | Workflow design, prompts, sheet schema, importable n8n JSON, ops docs |
| **Region** | Australia / Melbourne scheduling and compliance |

## Six integrated workflows

| # | Workflow | Purpose |
|---|----------|---------|
| 01 | Daily Lead Collection | Google Places API → lightweight site scrape (no browser) → dedupe → `leads` sheet |
| 02 | Cold Email Send | 3-step sequence (new → +2d → +5d), tradie vs health HTML, rate limits, `TEST_MODE` |
| 03 | Email Reply Handler | Gmail poll → STOP/opt-out → `hot_lead` alerts |
| 04 | Outbound Calls | Retell AI calls tradies from sheet, batching, retry rules |
| 05 | Retell Webhooks | `log_demo_interest` + post-call analysis → callbacks, sheet updates, optional Twilio SMS |
| 06 | Social Scheduler | OpenAI Agent plans segment/pillar/caption → DALL·E → Drive → draft row; manual FB/IG post (Option 1) |

## Stack

| Layer | Technologies |
|--------|----------------|
| Orchestration | n8n Cloud, LangChain AI Agent, sub-workflows as tools |
| Data | Google Sheets (`leads`, `opt_out`, `callbacks`, `social_posts`) |
| APIs | Google Places (New), Gmail, Google Drive, OpenAI (chat + images), Retell AI, Twilio (optional), Meta Graph API (optional) |
| Code | JavaScript in n8n Code nodes + `scripts/` assemblers for maintainable workflow JSON |

## Highlights

- **Hybrid AI design** — Agent for planning; deterministic sub-workflows for side effects (n8n production pattern)
- **No-code + code** — Visual workflows plus reusable JS (email extraction, HTML builder, social schema)
- **Operational safety** — `TEST_MODE`, batch limits, spacing (3 min email / 4 min calls), error workflow for social
- **Compliance-aware** — AU opt-out in emails, identity in call scripts, public-email-only scraping
- **Pragmatic ops** — SIP/termination and Meta API constraints documented → generate + manual post path for social

## Throughput (production targets)

- ~25 cold emails / weekday, ~10 outbound calls / weekday, 4 social drafts / week  
- Lead scrape without Puppeteer (faster, cheaper than browser automation)  
- Single spreadsheet as source of truth  

## Architecture

See [docs/architecture.md](docs/architecture.md) and the full case study in [PORTFOLIO.md](PORTFOLIO.md).

## Repo layout (private automation repo)

Typical structure — import via n8n UI after setting credentials:

```
workflows/*.json      # CONFIGURE_ME / PASTE_* placeholders in public exports
code/                 # Shared JS for Code nodes
scripts/              # Workflow JSON assemblers
sheets/*-template.csv # CRM templates (no PII)
retell/               # Voice + SIP docs
social/               # Meta / content ops
.env.example
TESTING.md
```

**Do not commit:** API keys, sheet IDs, Retell/Meta tokens, live credential IDs from exports, or customer PII.

## Topics

`n8n` · `automation` · `openai` · `retell-ai` · `lead-generation` · `email-marketing` · `workflow` · `google-sheets` · `voice-ai` · `saas`

## Author

**Habib Khan** · [Portfolio](https://github.com/hk204844-ui) · [LinkedIn](https://www.linkedin.com/in/habib-khan-chan/)
