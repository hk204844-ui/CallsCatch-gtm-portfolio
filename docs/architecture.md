# CallsCatch GTM — Architecture (portfolio summary)

## System flow

```
Google Places ──► scrape (HTTP) ──► Google Sheets (leads)
                                        │
          ┌─────────────────────────────┼─────────────────────────────┐
          ▼                             ▼                             ▼
   Cold email (Gmail)          Retell outbound calls          Social AI Agent
   3-step sequence             batch + spacing                 OpenAI + DALL·E
          │                             │                             │
          ▼                             ▼                             ▼
   Gmail reply handler         Retell webhooks                  social_posts sheet
   opt-out / hot_lead          callbacks + demo interest        → manual Meta post
```

## Orchestration pattern

```
┌──────────────────────────────────────┐
│  Workflow 06 — Social Scheduler      │
│  OpenAI Agent (planning)             │
│    ├── tool: sub-workflow (caption)  │
│    ├── tool: sub-workflow (image)    │
│    └── tool: write sheet row         │
└──────────────────────────────────────┘

Workflows 01–05: mostly deterministic graphs
  → fewer side effects inside the Agent loop
```

## Data model (Sheets)

| Tab | Role |
|-----|------|
| `leads` | Prospects from Places + scrape; email/call state |
| `opt_out` | STOP / unsubscribe |
| `callbacks` | Demo interest and scheduled follow-ups |
| `social_posts` | Draft captions, assets, post status |

Templates ship as `*-template.csv` in the private repo — never real PII in GitHub.

## External services

| Service | Use |
|---------|-----|
| Google Places (New) | Business discovery |
| Gmail | Outbound sequences + inbound reply poll |
| Google Drive | Social image storage |
| OpenAI | Agent reasoning, copy, DALL·E |
| Retell AI | Outbound voice + webhooks |
| Twilio | Optional SMS after calls |
| Meta Graph API | Optional; manual post path preferred |

## Security

- All secrets in n8n credential store and `.env` (not committed)  
- Scrub credential IDs if re-exporting workflows from Cloud  
- `TEST_MODE` gates live email/call side effects during development  

## Related portfolio repo

Product voice stack (Retell + Twilio marketing site): [CallsCatch-portfolio](https://github.com/hk204844-ui/CallsCatch-portfolio)
