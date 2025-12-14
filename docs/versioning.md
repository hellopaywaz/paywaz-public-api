# Paywaz API Versioning & Compatibility

## Version format
Paywaz uses date-based API versions: `YYYY-MM-DD` (example: `2025-01-01`).

## Request versioning
Clients SHOULD send:

`Paywaz-Version: YYYY-MM-DD`

If omitted:
- The API serves the **default stable version** (documented in release notes).
- The response MUST include the served version header.

## Response headers
Every response includes:

- `Paywaz-Version: YYYY-MM-DD` (the version actually used to process the request)

When a version is being deprecated, responses MAY include:

- `Deprecation: true`
- `Sunset: <RFC 1123 date>` (the date the version stops being served)
- `Link: <...>; rel="deprecation"` (points to the deprecation policy)

## Backwards compatibility rules
Within the same `Paywaz-Version`, changes are **additive only**:
- ✅ Add new fields (optional)
- ✅ Add new endpoints
- ✅ Add new event types
- ✅ Expand enum values (clients must be tolerant)

Breaking changes require a **new Paywaz-Version**:
- ❌ Removing/renaming fields
- ❌ Changing meaning or required-ness of fields
- ❌ Changing signature format
- ❌ Changing webhook payload structure in a non-additive way

## Deprecation policy
- Paywaz announces deprecations with at least **90 days notice**
- Deprecated versions continue to work until the `Sunset` date
- After sunset, requests for that version return an error indicating upgrade path

## Webhook versioning
Webhook payloads include:
- `event_version` (date-based, same format)
- `type`, `id`, `created`, `data`

Rules:
- Within an `event_version`, payload changes are additive only
- Breaking webhook changes require a new `event_version`
- Signature verification algorithm remains stable across versions whenever possible

## Recommended client behavior
- Always pin `Paywaz-Version`
- Always implement tolerant parsing (ignore unknown fields)
- Always verify webhook signatures using the raw request body
