# Paywaz API Versioning & Compatibility

Paywaz uses date-based API versions: `YYYY-MM-DD` (example: `2025-01-01`).

## Request versioning
Clients SHOULD send:

`Paywaz-Version: YYYY-MM-DD`

If omitted:
- Paywaz serves the account’s pinned default version.

## Response versioning
Responses include:

`Paywaz-Version: YYYY-MM-DD`

This is the version actually used to process the request.

## Backwards compatibility rules
Within a given `Paywaz-Version`, changes are **additive only**:
- ✅ Add new optional fields
- ✅ Add new endpoints
- ✅ Add new event types
- ✅ Add new enum values (clients must tolerate unknown values)

Breaking changes require a **new Paywaz-Version**:
- ❌ Remove/rename fields
- ❌ Make optional fields required
- ❌ Change meaning of fields
- ❌ Non-additive changes to webhook payloads

## Deprecation policy
Paywaz may deprecate older versions using:
- `Deprecation: true`
- `Sunset: <RFC 1123 date>`
- `Link: <...>; rel="deprecation"`

Deprecations will provide at least **90 days notice** before sunset whenever possible.

## Webhook versioning
Webhook payloads include:
- `eventVersion` (date-based)

Rules:
- Within an `eventVersion`, webhook schema changes are additive only
- Breaking webhook changes require a new `eventVersion`
- Clients must ignore unknown fields
