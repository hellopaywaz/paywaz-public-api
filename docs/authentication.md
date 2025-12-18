# Paywaz Public API — Authentication (Preview)

This document provides an overview of how authentication will function for the
Paywaz Public API. As Paywaz is currently operating in stealth mode, the flows
and structures described here are **preliminary** and intended for planning and
integration readiness only.

Production authentication details — including key issuance, scopes, JWT
structures, and endpoint availability — will be finalized as Paywaz moves into
public release.

---

## Overview

All requests to the Paywaz Public API require authentication.

The authentication model is built around:

- **API Keys** — uniquely identifying a merchant or partner
- **JWT Tokens** — short-lived tokens used for secure, stateless request auth
- **Non-Custodial Signing** (optional) — cryptographic confirmation of requests
  originating from a merchant-controlled wallet
- **Role-Based Access Scopes** — ensuring that keys are limited to the correct
  merchant and permission set

The authentication layer is designed to be **secure, lightweight**, and
compatible with:

- Server-side applications
- Web and mobile clients
- POS devices
- Third-party ecommerce or integration platforms

---

## API Keys (Merchant Credentials)

Each merchant integrating with Paywaz receives:

- A **Public API Key** – safe to embed client-side for initializing sessions
- A **Secret API Key** – used for server-to-server calls

### Example (conceptual):
```json
{
  "publicKey": "pk_test_1234...",
  "secretKey": "sk_test_9876...",
  "scopes": ["payments:write", "payments:read"],
  "issuedAt": "2025-01-15T00:00:00Z"
}
```

Use the secret key to exchange for a short-lived JWT or to sign requests
(determined by the final production model). Never expose the secret key in
client-side code.

---

## JWT Tokens

JWTs will be used to authorize API calls and will include:

- Merchant identifier
- Allowed scopes
- Expiration (short TTL)
- Optional nonce or session context

Tokens must be sent in the `Authorization: Bearer <token>` header.

---

## Non-Custodial Signing (Optional)

For workflows that benefit from on-chain verification, requests may be signed
with a merchant-controlled wallet. The signed payload will include the request
body and timestamp to prevent replay attacks.

---

## Error handling

Authentication failures will return structured JSON errors to help you debug
issues quickly:

```json
{
  "error": {
    "code": "unauthorized",
    "message": "Missing or invalid API key.",
    "details": [
      {
        "issue": "Provide a valid X-API-Key header"
      }
    ]
  }
}
```
