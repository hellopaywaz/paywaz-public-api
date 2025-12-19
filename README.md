# Paywaz Public API (Preview)

Welcome to the **Paywaz Public API** — the developer gateway into our zero-fee, crypto-native payments infrastructure.

Paywaz runs on **Solana Mainnet**, leveraging high-speed, low-cost settlement rails while providing an API-first architecture for merchants, enterprises, and global platforms.

> **Note:** This is a public preview. Additional endpoints, SDKs, and documentation will be released as Paywaz transitions out of stealth.

---

## What You Can Do With the Paywaz API
- Initiate zero-fee stablecoin or multi-crypto payments  
- Auto-convert incoming tokens to hedged stablecoins (PZUSD, PZGBP, PZEUR, etc.)  
- Create and manage checkout sessions  
- Verify transaction status  
- Retrieve settlement and payout data  
- Integrate Paywaz with POS, ecommerce, mobile apps, or enterprise systems  

---

# paywaz-public-api

Public OpenAPI specification for the Paywaz API.

## Files
- `openapi.yaml` — OpenAPI 3.1 spec
- `redocly.yaml` — Redocly lint config

## Local setup
Requires Node.js **20+**.

```bash
npm ci
```

### Golden commands
These commands are wired into CI and should be used locally:

| Purpose      | Command                              |
| ------------ | ------------------------------------ |
| Lint / tests | `npm test` (runs Redocly lint)       |
| Lint only    | `npm run lint`                       |
| Bundle spec  | `npm run build` (outputs to `dist/`) |
| Preview docs | `npm start` (Redocly preview on 8080)|

> Tip: `npm start` runs `redocly preview-docs` and binds to `0.0.0.0:8080` so you can view the docs locally.
> These commands invoke Redocly via `npx` and will download the pinned CLI version if it is not already cached.


## API Specification
An OpenAPI 3.0 specification will be published here as endpoints become publicly available.

Current placeholder:
Paywaz-Version: 2025-01-01
