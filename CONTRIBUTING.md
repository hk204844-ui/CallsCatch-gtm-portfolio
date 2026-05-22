# Contributing (portfolio / import guide)

This repository is a **public showcase**. The runnable automation lives in n8n Cloud with credentials configured in the UI.

## If you are evaluating this project

1. Read [README.md](README.md) and [PORTFOLIO.md](PORTFOLIO.md).  
2. Review [docs/architecture.md](docs/architecture.md).  
3. In your own n8n instance: import sanitized `workflows/*.json` from the private repo (when shared), replace `CONFIGURE_ME` / `PASTE_*` placeholders, and attach credentials.  
4. Copy `sheets/*-template.csv` into a new Google Sheet — do not use production sheet IDs from exports.  

## If you are the maintainer (Habib)

- Never commit `.env`, live sheet IDs, Retell/Meta tokens, or exports with embedded credential IDs.  
- Re-export workflows from templates after credential rotation.  
- Add screenshots under `docs/images/` with secrets blurred.  
